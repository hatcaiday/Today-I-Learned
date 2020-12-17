Vào một ngày đẹp trời, bỗng dưng chạy rubocop báo
```
Error: The `Layout/Tab` cop has been renamed to `Layout/IndentationStyle`.
(obsolete configuration found in .rubocop_enabled.yml, please update it)
```
Ơ mà mình có thay đổi gì đâu nhỉ? Gemfile.lock vẫn không thay đổi mà. M.n sao vẫn pass mà không thấy có lỗi giống mình. Thì cũng đừng quá căng thẳng, bạn chỉ đang có version gem rubocop trong máy local hơi khác thôi.

Và để fix nó, bạn chỉ cần làm vài lệnh đơn giản như sau:

**Bước 1: Tìm list gem trong local xem có những version khác lạ.**
```
gem list | grep rubocop
# Có thể thay rubocop bằng gem khác bạn muốn kiểm tra

=>>
rubocop (1.2.0, 0.80.1)
rubocop-ast (1.1.1)
rubocop-checkstyle_formatter (0.4.0)
rubocop-performance (1.8.1, 1.5.2)
rubocop-rails (2.8.1, 2.4.2)
rubocop-rspec (2.0.0)
```

**Bước 2: Uninstall gem version**
```
# Ở đây mình chọn uninstall version 1.2.0
gem uninstall rubocop --version 1.2.0
```

Chạy thử xem được chưa nhé!

**Một số lệnh remove gem version**

```
# remove all old versions of the gem
gem cleanup gem_name

# choose which ones you want to remove
gem uninstall gem_name

# remove version 1.1.9 only
gem uninstall gem_name --version 1.1.9

# remove all versions less than 1.3.4
gem uninstall gem_name --version '<1.3.4'
```

