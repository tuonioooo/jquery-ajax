# ajax使用Form提交普通表单（GET、POST）

* ## **前端H5页面POST方式**

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org" lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax使用Form提交普通表单</title>
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no-cache">
    <meta http-equiv="expires" content="0">
    <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
    <meta http-equiv="description" content="This is my page">
    <script src="http://libs.baidu.com/jquery/1.8.3/jquery.js"></script>
</head>
<body>
<h1>ajax使用Form提交普通表单</h1>
<script type="text/javascript">

    $(function(){
        $("#formdataId").click(function(){
            var data = $("#form2").serialize();
            alert(data);
            $.ajax({
                url : '/ajax2Post',
                type : 'post',
                data : data,
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
<form action="" id="form2">
    <input type="text" name="name" value="allen"/>
    <input type="text" name="passwd" value="123456"/>
    <input type="button" value="ajax提交表单" id="formdataId"/>
</form>
<em id="zs_currvip"></em>

</body>
</html>
```

* ## **前端H5页面GET方式**

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org" lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax使用Form提交普通表单</title>
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no-cache">
    <meta http-equiv="expires" content="0">
    <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
    <meta http-equiv="description" content="This is my page">
    <script src="http://libs.baidu.com/jquery/1.8.3/jquery.js"></script>
</head>
<body>
<h1>ajax使用Form提交普通表单</h1>
<script type="text/javascript">

    $(function(){
        $("#formdataId").click(function(){
            var data = $("#form2").serialize();
            alert(data);
            $.ajax({
                url : '/ajax2Get',
                type : 'get',
                data : data,
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
<form action="" id="form2">
    <input type="text" name="name" value="allen"/>
    <input type="text" name="passwd" value="123456"/>
    <input type="button" value="ajax提交表单" id="formdataId"/>
</form>
<em id="zs_currvip"></em>

</body>
</html>
```

> note：
>
> 1.var data = $\("\#form2"\).serialize\(\);  拿到form表单对象，将表单内容序列化成一个字符串：name=allen&passwd=123456
>
> 2.serializeArray\(\)方法，将页面表单序列化成一个JSON结构的对象。注意不是JSON字符串
>
> \[{"name":"lihui", "age":"20"},{...}\]

* ## Java后台Controller

```
@Controller
@RequestMapping("/")
public class AjaxController {

    @PostMapping("/ajax2Post")
    @ResponseBody
    public String ajax2Post(String name, String passwd){
        return "name={" + name + "}, passwd={"+passwd+"}";
    }

    @GetMapping("/ajax2Get")
    @ResponseBody
    public String ajax2Get(String name, String passwd){
        return "name={" + name + "}, passwd={"+passwd+"}";
    }


}
```



