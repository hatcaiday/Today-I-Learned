## Rails 6 add `rails notes` command and `Rails::Command::NotesCommand`
`rails notes` được sử dụng để tìm những comment bắt đầu với keyword đặc biệt.

Rails 6 thêm `Rails::Command::NotesCommand` theo pattern cho Rails::Commands và cũng giới thiệu một số thay đổi hữu ích cho `rails notes` API.

Cách sử dụng `rake notes` cũ đã được sửa đổi để gọi command mới hơn với cảnh báo khi gọi API cũ.

**Trước Rails 6**

Trước đây, người ta phải sử dụng biến môi trường để tìm bình luận bắt đầu bằng custom keywords. Chẳng hạn như, để tìm comment bắt đầu bằng `frozen_string_literal`

```
rails notes:custom ANNOTATION=frozen_string_literal
app/channels/application_cable/channel.rb:
  * [1] true

app/channels/application_cable/connection.rb:
  * [1] true
```
Ngoài ra, chúng ta có thể sử dụng các certain tags trực tiếp. Chẳng hạn như, để tìm comments bắt đầu bằng TODO
```
rails notes:todo

app/controllers/user_controller.rb:
  * [ 56] nhungdt-1833 Pass varialbe to this function
```
**Rails 6**

Với Rails 6, chúng ta có thể sử dụng --annotations argument để search default tags hoặc pass chú thích đặc biệt.

Mặc định, để tìm comments bắt đầu với các default tags (`FIXME`, `OPTIMIZE`, `TODO`)
```
rollers/admin/users_controller.rb:
  * [ 40] [TODO] move business logic to model
  * [144] [FIXME] needs urgent attention for next deployment

lib/school.rb:
  * [ 18] [OPTIMIZE] refactor to a faster sql query
```
Và để tìm chú thích với các custom tags.
```
rails notes --annotations REFACTOR FIXME
app/controllers/products_controller.rb:
  * [ 55] [REFACTOR] need to refactor this controller code

app/controllers/admin/users_controller.rb:
  * [144] [FIXME] needs urgent attention for next deployment
```
Note: `rails notes:custom`, `rails notes:fixme`, `rails notes:todo`, `rails notes:optimize` đã được đánh dấu là không dùng nữa.

Gọi bất kỳ notes command với `rake` thay vì `rails` cũng không được chấp nhận.
