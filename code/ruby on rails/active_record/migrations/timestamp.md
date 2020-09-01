Every migration file that Rails generates has a timestamp that is present in file name is important and is used by Rails to confirm whether a migration has run or not.

Ex: File name `20202012103635_create_users.rb`

Why Rails add it?
Every time a migration is generated using the `rails g migration` command, Rails generates the migration file with a unique timestamp. The timestamp is in the format `YYYYMMDDHHMMSS`. Whenever a migration is run, Rails inserts the migration timestamp into an internal table `schema_migrations`. This table is created by Rails when we run our first migration. The table only has the column version, which is also its primary key. This is the structure of the schema_migrations table.

Ex:
```
schema.rb:
`ActiveRecord::Schema.define(version: 2020_20_12_103635) do`
```
Chạy lệnh migration trên command:
Ex: `rails model users name:string`
Sau khi chạy lệnh này nó sẽ sinh ra một file với tên:
`20202012103635_create_users.rb`

Nhìn 2 giá trị `2020_20_12_103635` và `20202012103635`

Điều này có nghĩa là khi có một file migration mới, Rails sẽ check trong file schema.rb xem time version có < time khi migration file mới tạo hay không. nếu có nó sẽ yêu cầu bạn chạy lệnh để migrate db.

Nếu chạy thêm lần nữa, Rails sẽ check trong file schema và báo file đã được migrate rồi. Trừ khi bạn xóa database sau đó chạy lại =))

`t.timestamp`
Được thêm từ Rails 5 trở đi, sẽ tạo ra 2 trường là created_at và updated_at rất quan trọng trong việc check khi record được create hay update.

Note: Update_all thì không. nó sử dụng raw sql nên sẽ truy vấn trực tiếp vào trong đó, và sẽ update theo column nên trường updated_at không thay đổi.



