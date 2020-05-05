## Negative scopes enum values
Rails 6 thêm negative scopes cho tất cả các giá trị của enum

Enum cho phép khai báo các thuộc tính, nơi mà giá trị được map với integer trong database, nhưng có thể truy vấn bằng name.

```
class User < ApplicationRecord
  enum gender: %i[male, female, other]
end
```

Trước đây nếu chúng ta muốn lấy ra User mà gender không phải là male thì sẽ dùng như sau:

```
User.where.not(gender: :male)
```

Bây giờ chúng ta chỉ cần thêm `not` vào mỗi giá trị enum:
```
User.not_male
```
