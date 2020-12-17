**HTML 5 cung cấp 2 cách để lưu data trên browser (trình duyệt) - localStorage và sessionStorage.**

## 1. Local Storage
localStorage lưu trữ data với thời gian không giới hạn. Điều đó cho thấy data sẽ không bao giờ bị mất khi chúng ta đóng browser và data có thể sử dụng vào ngày mai, ngày kia hay bất kỳ ngày nào sau đó.

LocalStorage lưu trữ data dưới dạng key - value.

Trong trình duyệt Chrome, ta có thể thấy nội dung của localStorage ở đây:
`Developer tools (F12) > Application > Local Storage`

Để setting và get hay delete data từ localStorage thì khá đơn giản, chỉ cần một vài dòng lệnh là xong ngay :)

VD:
```
// Save data to localStorage
localStorage.setItem('key', 'value');

// Get saved data from localStorage
localStorage.getItem('key');

// Remove saved data from localStorage
localStorage.removeItem('key');

// Remove all saved data from localStorage
localStorage.clear();
```

Value bạn có thể set ở đây có thể là string, array, hash ...

Local storage cung cấp ít nhất 5MB cho việc lưu trữ trên browser. So với cookies với dung lượng lớn nhất là 4KB thì đây quả là một món hời đúng không nào?

LocalStorage data có thể đọc bởi Javascript code. Nếu hacker có thể thực thi Javacript code trên web site của bạn thì họ có thể lấy tất cả dữ liệu trên localStorage đó, nên đừng lưu trữ những dữ liệu nhạy cảm ở đây nha.

## 2. Session Storage

Data được lưu trữ trên sessionStorage sẽ bị xóa khi session của trang web kết thúc. Vậy session của trang web kết thúc khi nào?
Một session của trang kéo dài miễn là browser của chúng ta đang mở và tồn tại qua các lần reloads và restores. Khi một tab/window kết thúc session sẽ xóa data trong sessionStorage. Tức là tắt browser thì session cũng không còn nữa.

sessionStorage lưu trữ data dưới dạng key - value.

Trong trình duyệt Chrome, ta có thể thấy nội dung của localStorage ở đây:
`Developer tools (F12) > Application > Session Storage`

Việc setting và get hay delete data từ sessionStorage thì cũng tương tự với localStorage.

```
// Save data to sessionStorage
sessionStorage.setItem('key', 'value');

// Get saved data from sessionStorage
sessionStorage.getItem('key');

// Remove saved data from sessionStorage
sessionStorage.removeItem('key');

// Remove all saved data from sessionStorage
sessionStorage.clear();
```


