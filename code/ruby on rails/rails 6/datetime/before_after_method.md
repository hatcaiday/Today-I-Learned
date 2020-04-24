## before? and after? method to Date, DateTime, Time và TimeWithZone

Rails 6 thêm `before?` and `after?` method vào `Date`, `DateTime`, `Time` và `TimeWithZone`. [Source code](https://github.com/rails/rails/pull/32185/files)

Trước đây chúng ta thường dùng toán tử `<` và `>` để so sánh nhỏ hơn và lớn hơn. Method `before?` và `after?` làm cho các so sánh date/time dễ đọc hơn.

Ví dụ:
Chúng ta sử dụng `>` và `<`
```
> Date.today > Date.yesterday
=> true
```

Dùng `before?` và `after?` method:
```
> yesterday = 1.day.ago
=> Tue, 18 Feb 2020 15:10:04 +07 +07:00

> yesterday.before? Date.current
=> true

> yesterday.after? Date.current
=> false
```
