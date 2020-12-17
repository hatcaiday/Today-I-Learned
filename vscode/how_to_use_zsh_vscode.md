# Làm thế nào để sử dụng zsh trên VSCode

B1: Tìm thư mục install zsh
```
which zsh
```
B2: Vào phần user setting > features > terminal > Chọn edit settings.json. Thêm đoạn dưới để VS code nhận biết shell nó sẽ sử dụng là zsh
```
"terminal.integrated.shell.linux": "/usr/bin/zsh"
```

B3: Tắt VSCode, bật lại và thưởng thức :v
