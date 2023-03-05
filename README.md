1. Tạo cơ sở dữ liệu: Tạo cơ sở dữ liệu để lưu trữ thông tin người dùng. Bạn có thể sử dụng MySQL hoặc các hệ quản trị cơ sở dữ liệu khác. Trong trường hợp này, tôi sẽ tạo cơ sở dữ liệu MySQL có tên là "my_database" với bảng "User" chứa thông tin người dùng.  
```
CREATE DATABASE my_database;

USE my_database;

CREATE TABLE User (
  id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(30) NOT NULL,
  password VARCHAR(30) NOT NULL,
  fullname VARCHAR(50) NOT NULL,
  email VARCHAR(50) NOT NULL
);
```

2. Tạo trang đăng kí: Tạo trang đăng kí để người dùng có thể tạo tài khoản.  
```
<form action="register.php" method="post">
  <input type="text" name="username" placeholder="Tên đăng nhập" required>
  <input type="password" name="password" placeholder="Mật khẩu" required>
  <input type="text" name="fullname" placeholder="Họ và tên" required>
  <input type="email" name="email" placeholder="Email" required>
  <button type="submit">Đăng kí</button>
</form>
```
3. Viết mã PHP xử lý đăng kí: Viết mã PHP để xử lý thông tin đăng kí. Bạn cần kiểm tra xem thông tin đăng kí có hợp lệ không và thêm người dùng vào cơ sở dữ liệu.
```
<?php
// Kết nối cơ sở dữ liệu
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "my_database";

$conn = new mysqli($servername, $username, $password, $dbname);
if ($conn->connect_error) {
  die("Kết nối thất bại: " . $conn->connect_error);
}

// Xử lý đăng kí
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $username = $_POST["username"];
  $password = $_POST["password"];
  $fullname = $_POST["fullname"];
  $email = $_POST["email"];

  // Kiểm tra username đã tồn tại chưa
  $sql = "SELECT * FROM User WHERE username='$username'";
  $result = $conn->query($sql);

  if ($result->num_rows > 0) {
    echo "Tên đăng nhập đã tồn tại.";
  } else {
    // Thêm người dùng vào cơ sở dữ liệu
    $sql = "INSERT INTO User (username, password, fullname, email)
            VALUES ('$username', '$password', '$fullname', '$email')";

    if ($conn->query($sql) === TRUE) {
      echo "Đăng kí thành công.";
    } else {
      echo "Lỗi: " . $sql . "<br>" . $conn->error;
    }
  }
}

$conn->close();
?>
```
4. Tạo trang đăng nhập: Tạo trang đăng nhập để người dùng có thể đăng nhập vào tài khoản đã đăng kí.
```
<form action="login.php" method="post">
  <input type="text" name="username" placeholder="Tên đăng nhập" required>
  <input type="password" name="password" placeholder="Mật khẩu" required>
  <button type="submit">Đăng nhập</button>
</form>
```
5. Viết mã PHP xử lý đăng nhập: Viết mã PHP để xử lý thông tin đăng nhập. Bạn cần kiểm tra xem thông tin đăng nhập có chính xác không và đăng nhập người dùng vào trang web.
```
<?php
// Khởi động phiên đăng nhập
session_start();

// Kết nối cơ sở dữ liệu
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "my_database";

$conn = new mysqli($servername, $username, $password, $dbname);
if ($conn->connect_error) {
  die("Kết nối thất bại: " . $conn->connect_error);
}

// Xử lý đăng nhập
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  $username = $_POST["username"];
  $password = $_POST["password"];

  // Kiểm tra thông tin đăng nhập
  $sql = "SELECT * FROM User WHERE username='$username' AND password='$password'";
  $result = $conn->query($sql);

  if ($result->num_rows == 1) {
    // Đăng nhập thành công
    $_SESSION["username"] = $username;
    header("location: search.php");
  } else {
    echo "Tên đăng nhập hoặc mật khẩu không chính xác.";
  }
}

$conn->close();
?>
```
6. Tạo trang search ID: Tạo trang search ID để người dùng có thể tìm kiếm thông tin người dùng.
```
<form action="search.php" method="get">
  <input type="text" name="id" placeholder="ID người dùng">
  <button type="submit">Tìm kiếm</button>
</form>
```
7. Viết mã PHP xử lý search ID: Viết mã PHP để xử lý tìm kiếm thông tin người dùng. Bạn cần truy vấn cơ sở dữ liệu để lấy thông tin người dùng với ID tương ứng và hiển thị kết quả.
```
<?php
// Khởi động phiên đăng nhập
session_start();

// Kiểm tra đăng nhập
if (!isset($_SESSION["username"])) {
  header("location: login.php");
}

// Kết nối cơ sở dữ liệu
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "my_database";

$conn = new mysqli($servername, $username, $password, $dbname);
if ($conn->connect_error) {
  die("Kết nối thất bại: " . $conn->connect_error);
}

// Xử lý tìm kiếm ID
if ($_SERVER["REQUEST_METHOD"] == "GET") {
  $id = $_GET["id"];

  // Truy vấn thông tin người dùng v
```
