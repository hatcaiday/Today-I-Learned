```
cacheClients.catboxList = [
  {
    name: 'redisCache',
    engine: CatboxRedis,
    host: REDIS_HOST,
    port: REDIS_PORT,
    password: redisPassword,
    partition: REDIS_PARTITION
  }
];
```
```
cache: {
  cache: 'redisCache',
  segment: 'category',
  expiresIn: CACHE_EXPIRES_IN,
  staleIn: cacheStaleIn,
  staleTimeout: CACHE_STALE_TIMEOUT,
  generateTimeout: false
}
```


- catbox: https://github.com/hapijs/catbox
- catbox-redis: https://github.com/hapijs/catbox-redis
---------------------------
###  `client`: Là một object cung cấp một cache abstraction level thấp.
- `name`: định nghĩa tên 1 catbox client mới. Trong trường hợp bỏ qua thuộc tính name này thì sẽ tạo 1 cache client mới thay thế default client. Tên mặc định: catbox.
https://hapi.dev/tutorials/caching/?lang=en_US#-catbox
- `engine`: là 1 object hoặc function prototype đang thực thi cache strategy.
+ ví dụ về engine là function: https://github.com/hapijs/catbox/blob/master/test/client.js#L19
+ engine là một object: https://github.com/hapijs/catbox/blob/master/test/client.js#L45
- `host`: hostname của Redis server. Default: '127.0.0.1'
- `port`: Redis server port hoặc unix domain socket path. Defaults: 6379
- `password`: Redis authentication password,
- `partition`: Phân vùng dữ liệu để tách biệt các kết quả được lưu trong bộ nhớ cache trên nhiều cliens (máy khách), là 1 string thường được thêm vào trước tất cả các item keys(prefix). Default: ‘’
- `segment`: cho phép tách biệt bộ nhớ cache trong 1 phân vùng(partition). Trong Redis, segment là 1 tiền tố bổ sung (additional prefix) với tùy chọn partition.

-
### `Policy`: là 1 object cung cấp cache interface bằng cách setting 1 global policy - cái mà sẽ tự động được ap dụng cho mỗi hành động lưu trữ nào. Các options:

- `expiresIn`: number, thời gian hết hạn được tính bằng mili giây kể từ thời điểm item được lưu trữ trong cache. Không thể sử dụng đồng thời với option `expiresAt`.
- `expiresAt`: Sử dụng local time dùng format 'HH:MM' (format trong ruby: "%H:%M"), tại thời điểm tất cả các cache records cho route hết hạn, Không thể sử dụng đồng thời với `expiresIn`
- `staleIn`: number, tính bằng mili giây, dùng để đánh dấu một item đã được lưu trong cache là cũ và cố gắng tạo lại nó nếu hàm generateFunc được cung cấp. `StaleIn` < `expiresIn`. Thường được khởi tạo và tính toán giá trị trong function(stored, ttl).
https://github.com/hapijs/catbox/blob/master/test/policy.js#L818
- `staleTimeout`: number, số mili giây chờ trước khi trả về timeout khi function generateFunc tđang tạo giá trị mới.
- `generateTimeout`: number, số mili giây chờ trước khi trả về lỗi timeout khi function generateFunc tốn quá nhiều thời gian.
  + Khi giá trị cuối cùng được trả về, nó được lưu tữ trong cache cho các request trong tương lai.
  + Đặt thành `false` để disable timeouts có thể khiến các get() request bị kẹt vĩnh viễn.
- `cache`: một client instance (đã được start)
- `generateKey`: sẽ truyền vào 2 tham số: `id` và `segment`. Giá trị trả về là 1 chuỗi key bo gồm:
“partition:segment:id”

  https://github.com/hapijs/catbox-redis/blob/master/lib/index.js#L221

  https://github.com/hapijs/catbox-redis/blob/master/test/index.js#L865
- `generateFunc` `async function(id, flags)`
  + `id`: string or object được cung cấp cho phương thức get() as-is(không được chuẩn hóa)
- (`flags`)[https://github.com/hapijs/catbox/blob/master/lib/policy.js#L242]: Một object dùng để trả lại các flags bổ sung:

  + `ttl`: Tính bằng mili giây. Đặt thành 0 để bỏ qua việc lưu trữ trong cache. Mặc định cho global policy.

Link Github Demo: https://github.com/nhungdtmr/catbox_redis_demo
