# DOCKER-PRACTICE
### Devops for Todo App

Trong Docker, "Persist the DB" có nghĩa là duy trì (lưu trữ) cơ sở dữ liệu (DB) sau mỗi lần khởi động container. Trong đoạn văn mà bạn đưa ra, nói về việc mỗi khi bạn khởi chạy container, danh sách công việc (todo list) lại trống rỗng. Nguyên nhân là do mỗi lần container chạy, nó sử dụng các layer từ image để tạo nên hệ thống tệp tin của mình. Mỗi container cũng có không gian riêng gọi là "scratch space" để tạo, cập nhật hoặc xóa các tệp tin. Những thay đổi này không được thấy trong các container khác, thậm chí khi chúng sử dụng cùng một image.

Để minh họa điều này, bạn thử khởi chạy hai container và tạo một tệp tin trong mỗi container. Bạn sẽ thấy rằng các tệp tin được tạo trong một container không khả dụng trong container khác.

Sau đó, bài hướng dẫn đề cập đến việc sử dụng volumes để giải quyết vấn đề này. Volume là một cách để kết nối đường dẫn trong hệ thống tệp tin của container với máy chủ (host) của bạn. Nếu bạn mount một thư mục trong container, những thay đổi trong thư mục đó cũng sẽ được thấy trên máy chủ. Khi mount cùng một thư mục qua các lần khởi động container, bạn sẽ thấy những tệp tin giống nhau.

Để giữ lại dữ liệu của ứng dụng todo, bạn cần tạo một volume và gắn (mount) nó với thư mục nơi bạn lưu trữ dữ liệu. Khi container viết vào tệp todo.db, dữ liệu sẽ được lưu trữ trên máy chủ thông qua volume.

Sử dụng volume mount, xem nó như một "hộp đen" dữ liệu. Docker quản lý toàn bộ volume, bao gồm cả vị trí lưu trữ trên đĩa. Bạn chỉ cần nhớ tên của volume.

### Command for project
**run this project:**
Please start docker desktop before running the following commands (for windows)
     
```
docker compose up -d
```
     
```
docker exec -it <mysql-container-id or mysql-container-name > mysql -p todos
```
     
```
select * from todo_items; (todo_items is a table of DB)
```

Some commands you can try, not from the project.
```
docker build -t getting-started .
```

```
docker run -dp 127.0.0.1:3000:3000 getting-started
```

# REFERENCES
[1]. https://github.com/docker/getting-started-app