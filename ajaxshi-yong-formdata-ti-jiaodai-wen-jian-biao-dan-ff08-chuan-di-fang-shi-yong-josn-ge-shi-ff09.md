# ajax使用FormData提交带文件表单（JSON保存数据格式）

* ## **前端H5页面**

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org" lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax使用FormData提交带文件表单（传递方式用JOSN格式）</title>
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no-cache">
    <meta http-equiv="expires" content="0">
    <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
    <meta http-equiv="description" content="This is my page">
    <script src="http://libs.baidu.com/jquery/1.8.3/jquery.js"></script>

    <script src="https://cdn.bootcss.com/jquery.serializeJSON/2.8.1/jquery.serializejson.js"></script>

</head>
<body>
<h1>ajax使用FormData提交带文件表单（传递方式用JOSN格式）</h1>
<script type="text/javascript">

    $(function(){
        $("#formdataId").click(function(){
            var formData = new FormData();
            var data={};
            data.name="Kobe";
            data.passwd="123456";
            formData.append("data", data);
            formData.append("file", $("#upload")[0].files[0]);
            alert(formData.get("data") + "==" + formData.get("file"));
            $.ajax({
                url : '/ajax_upload_json_1',
                type : 'post',
                data : formData,
                cache: false,
                processData : false, //告诉jQuery不要去处理发送的数据
                contentType: false,
                success : function(responseStr) {
                    alert("response：" + responseStr);
                },
                error : function(responseStr) {
                    alert("失败:" + JSON.stringify(responseStr));//将json对象转成json字符串。
                }
            });

        })
    });
</script>
<form action="" id="form1" enctype="multipart/form-data">
    <input type="text" name="name" value="allen"/>
    <input type="text" name="passwd" value="123456"/>
    <input type="file" name="file" id="upload"/>
    <input type="button" value="ajax提交表单" id="formdataId"/>
</form>
<em id="zs_currvip"></em>

</body>
</html>
```

* ## **Java后端Controller**

```
@PostMapping("/ajax_upload_json_1")
@ResponseBody
public String requestJson(@RequestBody JSONObject requestParams){
        return requestParams.toJSONString();
}
```



