# ajax使用Form提交带文件表单

* ## **前端H5页面方式**

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org" lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax使用Form提交带文件表单</title>
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no-cache">
    <meta http-equiv="expires" content="0">
    <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
    <meta http-equiv="description" content="This is my page">
    <script src="http://libs.baidu.com/jquery/1.8.3/jquery.js"></script>
</head>
<body>
<h1>ajax使用Form提交带文件表单</h1>
<script type="text/javascript">

    $(function(){
        $("#formdataId").click(function(){
            document.getElementById("form1").submit();
        })
    });
</script>
<form action="/ajax_upload_2" method="post" id="form1" enctype="multipart/form-data">
    <input type="text" name="name" value="allen"/>
    <input type="text" name="passwd" value="123456"/>
    <input type="file" name="file" id="upload"/>
    <input type="button" value="ajax提交表单" id="formdataId"/>
</form>
<em id="zs_currvip"></em>

</body>
</html>
```

* ## Java后台Controller

```
@PostMapping("/ajax_upload_2")
    @ResponseBody
    public String ajaxUpload2(String name, String passwd, MultipartFile file){
        return "name={" + name + "}, passwd={"+passwd+"}," + file.getOriginalFilename();
    }
```



