# DOCKER-PRACTICE
### Devops for Todo App

Trong Docker, "Persist the DB" có nghĩa là duy trì (lưu trữ) cơ sở dữ liệu (DB) sau mỗi lần khởi động container. Trong đoạn văn mà bạn đưa ra, nói về việc mỗi khi bạn khởi chạy container, danh sách công việc (todo list) lại trống rỗng. Nguyên nhân là do mỗi lần container chạy, nó sử dụng các layer từ image để tạo nên hệ thống tệp tin của mình. Mỗi container cũng có không gian riêng gọi là "scratch space" để tạo, cập nhật hoặc xóa các tệp tin. Những thay đổi này không được thấy trong các container khác, thậm chí khi chúng sử dụng cùng một image.

Để minh họa điều này, bạn thử khởi chạy hai container và tạo một tệp tin trong mỗi container. Bạn sẽ thấy rằng các tệp tin được tạo trong một container không khả dụng trong container khác.

Sau đó, bài hướng dẫn đề cập đến việc sử dụng volumes để giải quyết vấn đề này. Volume là một cách để kết nối đường dẫn trong hệ thống tệp tin của container với máy chủ (host) của bạn. Nếu bạn mount một thư mục trong container, những thay đổi trong thư mục đó cũng sẽ được thấy trên máy chủ. Khi mount cùng một thư mục qua các lần khởi động container, bạn sẽ thấy những tệp tin giống nhau.

Để giữ lại dữ liệu của ứng dụng todo, bạn cần tạo một volume và gắn (mount) nó với thư mục nơi bạn lưu trữ dữ liệu. Khi container viết vào tệp todo.db, dữ liệu sẽ được lưu trữ trên máy chủ thông qua volume.

Sử dụng volume mount, xem nó như một "hộp đen" dữ liệu. Docker quản lý toàn bộ volume, bao gồm cả vị trí lưu trữ trên đĩa. Bạn chỉ cần nhớ tên của volume.

### Command for project
**Run this project:**

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

### Docker compose and Dockerfile
| Tính Chất                                       | Dockerfile cho Frontend và Backend                  | Docker Compose cho Database                         |
|--------------------------------------------------|----------------------------------------------------|----------------------------------------------------|
| **Tính Độc Lập và Quản Lý Dễ Dàng**              | Dockerfile giúp xây dựng môi trường chạy ứng dụng một cách độc lập và dễ dàng. Đảm bảo mọi người làm việc trên dự án có thể chia sẻ cùng một môi trường phát triển, tránh được các vấn đề liên quan đến sự khác biệt giữa môi trường phát triển và môi trường triển khai. | Docker Compose giúp quản lý nhiều container cùng một lúc, hữu ích khi muốn chạy và quản lý frontend, backend và database trong môi trường phát triển hoặc triển khai. |
| **Dễ Di Động và Chia Sẻ**                        | Docker images có thể xây dựng một lần và chia sẻ hoặc triển khai trên nhiều máy tính một cách dễ dàng. | Giúp định nghĩa cấu hình của database và dịch vụ liên quan trong một tệp duy nhất, dễ di chuyển và chia sẻ.         |
| **Quản Lý Phụ Thuộc và Kết Nối**                 | Định nghĩa các phụ thuộc cụ thể và môi trường thực thi cho frontend và backend. | Định nghĩa cách các dịch vụ kết nối với nhau, giúp quản lý mối quan hệ và cấu hình mạng giữa frontend, backend và database. |

Đương nhiên, bạn có thể thực hiện việc đảo ngược và đặt frontend, backend trong Docker Compose và database trong Dockerfile nếu dự án của bạn yêu cầu. Quyết định này có thể phụ thuộc vào cấu trúc của dự án, yêu cầu kỹ thuật cụ thể, và sự thuận tiện trong việc triển khai và quản lý môi trường.


# REFERENCES
[1]. https://github.com/docker/getting-started-app