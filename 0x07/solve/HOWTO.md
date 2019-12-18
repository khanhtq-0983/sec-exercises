## Bài 1:
* Mở sourcecode lên ta nhận được 
```html
<html>
  <head>
    <title>ERALF nO 7102</title>
  </head>
  <body>
    <input type="text" name="flag" id="flag" value="Enter the flag" />
    <input type="button" id="prompt" value="Click to check the flag" />
    <script type="text/javascript">
      document.getElementById("prompt").onclick = function() {
        var flag = document.getElementById("flag").value;
        var rotFlag = flag.replace(/[a-zA-Z]/g, function(c) {
          return String.fromCharCode(
            (c <= "Z" ? 90 : 122) >= (c = c.charCodeAt(0) + 13) ? c : c - 26
          );
        });

        if ("PyvragFvqrYbtvafNerRnfl@syner-ba.pbz" == rotFlag) {
          alert("Correct flag!");
        } else {
          alert("Incorrect flag, rot again");
        }
      };
    </script>
  </body>
</html>
```
* Đọc đoạn mã javascript , ta nhận thấy flag là đoạn flPyvragFvqrYbtvafNerRnfl@syner-ba.pbz nhưng đã được mã hóa bằng rot
* Trong hàm charCode , ta nhận thấy với các giá trị 13 ,26 ,.. sẽ được thay thế bằng các giá trị từ c -> z (90:122) 
* Decode bằng rot13,ta thu được flag  ClientSideLoginsAreEasy@flare-on.com

