# Redis Cli

```
redis-cli
```

## Redis monitor
```
redis-cli -h <hostname> -p <port> -a <password> -n <db> monitor >> out.txt
```

- `-h <hostname>`: Server hostname (default: 127.0.0.1)
- `-p <port>`: Server port (default: 6379)
- `-a <password>`: Password chúng ta sử dụng để connect đến server.
- `-n <db>`: Số thứ tự Database được định nghĩa sẽ chứa key & value của redis. (0,1, 2, ...)
- `monitor`: Log lại các hành động khi thao tác trên redis.
- `>> out.txt`: Lưu các hành động trên vào file out.txt (tên thay đổi tùy ý)

Ví dụ:
```
redis-cli -h 127.0.0.1 -p 6379 -a rd_password -n 1 monitor >> out.txt
```

Xem thêm các options hỗ trợ redis-cli: `redis-cli --help`
