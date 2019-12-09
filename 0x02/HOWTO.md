<!DOCTYPE html>
<html>
  <head>
    <title>Simple Auth</title>
  </head>
  <body>
    <div>
<?php
$password = 'FLAG_????????????????';
if (isset($_POST['password']))
    if (strcasecmp($_POST['password'], $password) == 0)
        echo "Congratulations! The flag is $password";
    else
        echo "incorrect...";
?>
    </div>
    <form method="POST">
      <input type="password" name="password">
      <input type="submit">
    </form>
  </body>
</html>

bài náy sử dụng code php
trong đó, ta nhận ra password nhập vào và password được so sánh với nhau bằng hàm string case compare
hàm này so sánh từng giá trị trong chuỗi và so sánh độ dài với nhau 
nếu trả về 0 thì sẽ in ra flag
để làm được bài này,ta sử dụng string case compare vulnerabilities 
nếu chúng ta nhập vào password thay vì giá trị string mà là array :
it will gives a warning (‘WARNING strcmp() expects parameter 2 to be string, array given on line number …!’
 but the compare result return 0.
 sử dụng burpsuite để bắt gói tin thay giá trị password=xxx thành password[]=xxx thì sẽ hiện ra flag = FLAG_VQcTWEK7zZYzvLhX 
