## Rails 6 add `db:seed:replant` task
### 1. Tại sao cần task?

Có rất nhiều lần chúng ta cần phải khôi phục seed data trong quá trình làm ở môi trường development hay staging và hơn thế nữa.

Điều này có thể vì những lý do khác nhau như cập nhật seed data, dữ liệu development bị lỗi, trước khi chúng ta có thể khôi phục các seed,  thông thường chúng ta sẽ xóa sạch mọi thứ trong database :D ( ví dụ: `rails db:migrate:reset`). Cách chúng ta thường làm là chạy `rails db:setup`. Điều này rebuilds cấu trúc database cho cả test và development và sau đó chạy `rails db:seed`, đó có thể là điều chúng ta không mong muốn.

Rails 6 thêm một thay thế thuận tiện hơn là: `rails db:seed:replant`.

### 2. Vậy task mới này làm gì?

Đầu tiên nó truncates tất cả các bảng cơ sở dữ liệu cho môi trường hiện tại và sau đó tải các seeds.

Xem thử ví dụ dưới đây, ta sẽ chạy task với `--trace` và xem nó làm những gì:
```
rails db:seed:replant --trace
```
```
** Invoke db:seed:replant (first_time)
** Invoke db:load_config (first_time)
** Invoke environment (first_time)
** Execute environment
** Execute db:load_config
** Invoke db:truncate_all (first_time)
** Invoke db:load_config
** Invoke db:check_protected_environments (first_time)
** Invoke db:load_config
** Execute db:check_protected_environments
** Execute db:truncate_all
** Invoke db:seed (first_time)
** Invoke db:load_config
** Execute db:seed
** Invoke db:abort_if_pending_migrations (first_time)
** Invoke db:load_config
** Execute db:abort_if_pending_migrations
** Execute db:seed:replant
```
Từ logs ở trên, chúng ta có thể thấy command thực thi theo các sub tasks theo trình tự:

**`db:load_config`**

Load cấu hình database cho môi trường hiện tại.

**`db:check_protected_environments`**

Điều này giúp bảo vệ khỏi việc vô tình chạy job trên các môi trường không phải test/development. Chẳng hạn, điều này ngăn chúng ta vô tình xóa tất cả các dữ liệu trên production. Task sẽ bị hủy bỏ nếu chúng ta cố gắng chạy trong môi trường này.
```
RAILS_ENV=production rails db:seed:replant
```
```
rails aborted!
ActiveRecord::ProtectedEnvironmentError: You are attempting to run a destructive action against your 'production' database.
If you are sure you want to continue, run the same command with the environment variable:
DISABLE_DATABASE_ENVIRONMENT_CHECK=1
/Users/puneetsutar/workspace/chat/bin/rails:9:in `<top (required)>'
/Users/puneetsutar/workspace/chat/bin/spring:15:in `<top (required)>'
bin/rails:3:in `load'
bin/rails:3:in `<main>'
Tasks: TOP => db:seed:replant => db:truncate_all => db:check_protected_environments
(See full trace by running task with --trace)
```

**`db:truncate_all`**

Đây là một rails task mới được thêm vào để hỗ trợ seed replant. Task này sẽ xóa dữ liệu khỏi tất cả các bảng cho một trường hiện tại ngoại trừ các bảng được dử dụng bên trong rails i.e
`schema_migrations` và `ar_internal_metadata`.
Command này cũng có thể được sử dụng riêng như một cách thuận tiện để truncate dữ liệu từ tất cả các bảng.

**`db:seed`**

Lệnh này để seed data.

**`db:abort_if_pending_migrations`**

Ném ra lỗi nếu có bất kỳ migrations nào đang chờ xử lý.

*Túm lại, `rails db:seed:replant` và hỗ trợ của nó `rails db:truncateall` thuận tiện để dọn dẹp development data trong Rails application.*
