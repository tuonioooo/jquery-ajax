# ajax使用FormData提交普通表单

* ## **前端H5页面**

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org" lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax使用FormData提交普通表单</title>
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no-cache">
    <meta http-equiv="expires" content="0">
    <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
    <meta http-equiv="description" content="This is my page">
    <script src="http://libs.baidu.com/jquery/1.8.3/jquery.js"></script>
</head>
<body>
<script type="text/javascript">

    $(function(){
        $("#formdataId").click(function(){
            var formData = new FormData($("#form1"));
            alert(formData);
            $.ajax({
                url : '/ajax1',
                type : 'post',
                data : formData,
                processData : false, //告诉jQuery不要去处理发送的数据
                contentType: false,//告诉jQuery不要去设置Content-Type请求头
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
    <input type="button" value="ajax使用FormData提交普通表单" id="formdataId"/>
</form>
<em id="zs_currvip"></em>

</body>
</html>
```

> note：
>
> 1.var formData = new FormData\($\("\#form1"\)\);  拿到表单里的值，封装到formData对象中
>
> 2.切记使用FormData时，ajax里的Type一定要是POST，GET不支持，如果使用GET，后台获取不到参数
>
> 3.除了使用new FormData\($\("\#form1"\)\);可以添加值，还可以使用
>
> var formData = new FormData\(\);
>
> formData.append\("name","allen"\);
>
> formData.append\("passwd",123456\);
>
> 自定义参数
>
> 4.一定要设置下面的参数，否则Jquery会自动处理
>
> processData : false, //告诉jQuery不要去处理发送的数据
>
> contentType 默认值为 application/x-www-form-urlencoded".在默认情况下，内容编码类型满足大多数情况。
>
> contentType = false，是防止jQuery对其进行处理,formData 会自动把类型填充为multipart/form-data

* ## Java后台Controller

```
@Controller
@RequestMapping("/")
public class AjaxController {

    @PostMapping("/ajax1")
    @ResponseBody
    public String ajax1(String name, String passwd){
        return "name={" + name + "}, passwd={"+passwd+"}";
    }
}
```



