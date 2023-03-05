1. Tạo cơ sở dữ liệu: Tạo cơ sở dữ liệu để lưu trữ thông tin người dùng. Bạn có thể sử dụng MySQL hoặc các hệ quản trị cơ sở dữ liệu khác. Trong trường hợp này, tôi sẽ tạo cơ sở dữ liệu MySQL có tên là "my_database" với bảng "User" chứa thông tin người dùng.  

    ``` html
<form action="register.php" method="post">
  <input type="text" name="username" placeholder="Tên đăng nhập" required>
  <input type="password" name="password" placeholder="Mật khẩu" required>
  <input type="text" name="fullname" placeholder="Họ và tên" required>
  <input type="email" name="email" placeholder="Email" required>
  <button type="submit">Đăng kí</button>
</form>
```
