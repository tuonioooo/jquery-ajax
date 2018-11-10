# ajax使用FormData提交带文件表单（传递方式用JOSN格式）

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
</head>
<body>
<h1>ajax使用FormData提交带文件表单（传递方式用JOSN格式）</h1>
<script type="text/javascript">

    $(function(){
        $("#formdataId").click(function(){
            var form=document.querySelector("#form1");
            var form3 = document.getElementById("form1");
            var formData = new FormData(form3);
            alert(formData.get("name")+"=="+formData.get("passwd")+"=="+formData.get("file"));
            $.ajax({
                url : '/ajax_upload_json_1',
                type : 'post',
                data : JSON.stringify(formData),//将formData对象转换成JSON对象
                dataType: 'json',//采用json方式传递表单
                cache: false,
                processData : false, //告诉jQuery不要去处理发送的数据
                contentType: "application/json; charset=utf-8",//告诉jQuery不要去设置Content-Type请求头
                success : function(responseStr) {
                    alert("response：" + responseStr);
                },
                error : function(responseStr) {
                    alert("失败:" + JSON.stringify(responseStr));//将    json对象    转成    json字符串。
                }
            });

        })
    });
</script>
<form action="" id="form1">
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



