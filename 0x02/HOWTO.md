## Bài 2
``` html
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
```

  - Bài náy sử dụng code php trong đó, ta nhận ra password nhập vào và password được so sánh với nhau bằng hàm string case compare hàm này so sánh từng giá trị trong chuỗi và so sánh độ dài với nhau nếu trả về 0 thì sẽ in ra flag
để làm được bài này,ta sử dụng string case compare vulnerabilities nếu chúng ta nhập vào password thay vì giá trị string mà là array :
  - it will gives a warning (‘WARNING strcmp() expects parameter 2 to be string, array given on line number …!’
 but the compare result return 0.
  - Sử dụng burpsuite để bắt gói tin thay giá trị password=xxx thành password[]=xxx thì sẽ hiện ra flag = FLAG_VQcTWEK7zZYzvLhX 

## Bài 4
``` php
if ($_POST['id']!=='' or $_POST['password']!=='')
{
    $try = true;
    $db = new PDO('sqlite:database.db');
    $s = $db->prepare('SELECT * FROM user WHERE id=? AND password=?');
    $s->execute(array($_POST['id'], $_POST['password']));
    $ok = $s->fetch() !== false;
}
``` 
 - Thông qua source code , ta có thể thấy có site database.db
 - Truy cập http://ksnctf.sweetduet.info/problem/35/database.db và ta down được file database về
 - Sử dụng tool https://inloop.github.io/sqlite-viewer/ ta có thể lấy ra được câu lệnh sql và các bảng
 - SELECT * FROM 'user2' LIMIT 0,30

* id	password
* root	GLDmNFJimveAAxyg_wSNp
 - Tuy nhiên ta thay ngược lại thì vẫn không login vào được 
 - Thử đổi user2 sang user và ta sẽ nhận đc flag 
* id	password
* root	FLAG_iySDmApNegJvwmxN

## Bài 3 
- Bài này sử dụng hàm random để lấy ra shipname
- Nếu lấy ra được yamato thì sẽ được flag 
- Tuy nhiên
- hàm này chỉ cho random để lấy ra đến giá trị thứ 10 trong dãy
       * $ship[] = mt_rand(0, count($shipname)-2);
-Tức là ko thể lấy ra được giá trị yamato
-Ta sử dụng burpsuite để bắt gói tin random  và nhận ra rằng mỗi lần send request to server thì giá trị trả về bao gồm ship=x và signature=xxx trong đó signature sử dụng hàm hash để mã hóa 
- Ta sử dụng tool hashbump để lấy ra được giá trị signature mới forward giá trị signature mới và ta thu được flag :FLAG_uc8qVFa8Sr6DwYVP
