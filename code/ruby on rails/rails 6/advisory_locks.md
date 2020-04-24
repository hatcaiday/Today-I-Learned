## Rails 6 add support for disabling database advisory locks
### 1. Advisory Lock là gì?

Databases cung cấp lock modes đa dạng để điều khiển truy cập đồng thời vào các bảng và data.

Advisory Lock cung cấp một cách thuận tiện để có được một khóa, ứng dụng hoàn toàn được thực thi và sẽ không block các thao tác ghi vào bảng.

### 2. Lock database là gì?

Khi một tiến trình application khởi động, chúng ta có thể có được một khóa trên một resource và sau đó giải phóng nó khi thoát chương trình. Bằng cách này, chúng ta đảm bảo rằng chương trình không chạy song song, đồng thời không thực sự chặn ứng dụng truy cập database.

Lợi ích của việc này là các bảng không bao giờ thực sự bị khóa để viết. Ứng dụng chính sẽ hoạt dộng bình thường và người dùng sẽ không bao giờ nhận thấy bất cứ điều gì xảy ra trong background.

Thêm chi tiết về Advisory Lock có sẵn trong [tài liệu](https://www.postgresql.org/docs/9.4/explicit-locking.html) Postgresql

**Trước Rails 6**

Mặc định, Active Record sử dụng các tính năng database như các câu lệnh prepare và advisory locks.

Rails sử dụng advisory lock khi cố gắng chạy một migration. Điều này đảm bảo rằng việc migrations đồng thời không kết thúc trên cùng một database.

Điều này tạo ra một số vấn đề khi sử dụng transaction được sử dụng để giảm tải cho các PostgreSQL servers bằng cách sử dụng shared connections.

Advisory locks không được chia sẻ trên các transactions, dẫn đến các vấn đề khi sử dụng các nhóm connection như PgBouncer trong chế độ tổng hợp transaction. Khi Rails kết thúc, điều này dẫn đến một `ActiveRecord::ConcurrentMigrationError` khi thử chạy database migrations khi sủ dụng PgBouncer.

**Trong Rails 6**

Một cách đơn giản để fix là disabling advisory lock. Điều này cho phép có quyền kiểm soát tốt hơn đối với bất kỳ connection nào ở bên ngoài mà chúng ta có thể muốn sử dụng như PgBouncer.

Để disable advisory lock, những gì chúng ta cần làm là chuyển đổi `advisory_locks` trong `database.yml` sang `false`
```
# database.yml
production:
  adapter: postgresql
  advisory_locks: false
```
Mặc định, advisory_locks được set là `true` và được sử dụng trong các phần của application khi chạy migrations.
