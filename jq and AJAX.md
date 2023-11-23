# 前端第二课之 jquery和AJAX

## jquery

jQuery，简称jq

jquery 是一个轻量级的js库

对HTML更深一层的控制操作选取，css的选择

jQuery下载和使用
可以从官网下，也可以利用CDN（内容分发网络）来直接使用jQuery

jquery语法

```javascript
美元符号定义 jQuery
选择符（selector）"查询"和"查找" HTML 元素
jQuery 的 action() 执行对元素的操作
实例:
$(this).hide() - 隐藏当前元素
$("p").hide() - 隐藏所有 <p> 元素
$("p.test").hide() - 隐藏所有 class="test" 的 <p> 元素
$("#test").hide() - 隐藏 id="test" 的元素
```
<p id="test"></p>


## AJAX

### 什么是Ajax？
1. AJAX :异步JavaScript和XML
2. AJAX的用途：
+ 运用 XHTML+CSS 来表达资讯；

+ 运用 JavaScript 操作 DOM（Document Object Model）来执行动态效果；

+ 运用 XML 和 XSLT 操作资料;

+ 运用 XMLHttpRequest 或新的 Fetch API 与网页服务器进行异步资料交换；

 注意：AJAX 与 Flash、Silverlight 和 Java Applet 等 RIA 技术是有区分的

3. AJAX 是一种用于创建快速动态网页的技术。

通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

传统的网页（不使用 AJAX）如果需要更新内容，必需重载整个网页面。

AJAX减轻服务器负担，按需要获得数据
无刷新更新页面，减少用户实际和心理的等待时间
只更新部分页面，有效利用带宽

### AJAX 的HTTPrequest

（1）创建异步对象。即 XMLHttpRequest 对象。

（2）设置请求的参数。包括：请求的方法、请求的url。

（3）发送请求。

（4）注册事件。onreadystatechange事件，状态改变时就会调用。如果要在数据完整请求回来的时候才调用，我们需要手动写一些判断的逻辑。

（5）获取返回的数据。

var xmlhttp=new XMLHttpRequest();

xmlhttprequest的方法

+ open(method,url,async)	
  
  规定请求的类型、URL 以及是否异步处理请求	

  - method：请求的方式，GET或POST；url：请求路径；async：true（异步）或 false（同步）

+ send(string)	将请求发送到服务器	string：请求参数，仅用于POST请求。格式：名1=值1&名2=值2
```javascript
xmlhttp.open("POST","DemoAJAXServlet",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("name=tom&age=20");
```
获得服务器响应
```javascript
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```

+ onreadystatechange	

状态改变事件触发器，每当readyState属性改变时，就会调用该函数

+ readyState	

存有XMLHttpRequest的状态。从0到4发生变化。0: 请求未初始化；1: 服务器连接已建立；2: 请求已接收；3: 请求处理中；4: 请求已完成，且响应已就绪


+ status	响应状态码。200: 成功；404: 未找到页面

```javascript
xmlhttp.onreadystatechange=function()
{
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
```
来一个实例

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script>
function loadXMLDoc()
{
	var xmlhttp;
	if (window.XMLHttpRequest)
	{
		//  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
		xmlhttp=new XMLHttpRequest();
	}
	else
	{
		// IE6, IE5 浏览器执行代码
		xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
	}
	xmlhttp.onreadystatechange=function()
	{
		if (xmlhttp.readyState==4 && xmlhttp.status==200)
		{
			document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
		}
	}
	xmlhttp.open("GET","/try/ajax/ajax_info.txt",true);
	xmlhttp.send();
}
</script>
</head>
<body>

<div id="myDiv"><h2>使用 AJAX 修改该文本内容</h2></div>
<button type="button" onclick="loadXMLDoc()">修改内容</button>

</body>
</html>
```


该参数规定AJAX请求的一个或多个名称/值对。下面的表格中列出了可能的名称/值：

|名称|值|函数|
|--|--|--|
|async|Boolean	|表示请求是否异步处理。默认true|
|beforeSend(xhr)|	Function| 发送请求前运行的函数。|
|cache	|Boolean	|表示浏览器是否缓存被请求页面。默认true
|complete(xhr,status)	|Function	|请求完成时运行的函数（在请求成功或失败之后均调用，即在success和error函数之后）
|contentType	|String	|发送数据到服务器时所使用的内容类型。默认是：”application/x-www-form-urlencoded”
|context	|Object	|为所有AJAX相关的回调函数规定 “this” 值
|data	|Object,String	|规定要发送到服务器的数据
|dataFilter(data,type)	|Function	|用于处理XMLHttpRequest原始响应数据的函数
|dataType	|String|	预期的服务器响应的数据类型。text：返回纯文本字符串；json：返回JSON数据
|error(xhr,status,error)	|Function	|如果请求失败要运行的函数
|global|	Boolean	|规定是否为请求触发全局AJAX事件处理程序。默认true
|ifModified	|Boolean	|规定是否仅在最后一次请求以来响应发生改变时才请求成功。 默认false
|jsonp	|String	|在一个jsonp中重写回调函数的字符串
|jsonpCallback	|String	|在一个jsonp中规定回调函数的名称
|password|	String	|规定在HTTP访问认证请求中使用的密码
|processData	|Boolean	|规定通过请求发送的数据是否转换为查询字符串。默认true
|scriptCharset	|String	|规定请求的字符集
|success(result,status,xhr)|	Function,Array	|当请求成功时运行的函数
|timeout	|Number	|设置本地的请求超时时间（以毫秒计）
|traditional	|Boolean	|规定是否使用参数序列化的传统样式
|type	|String	|规定请求的类型（GET或POST）
|url	|String	|规定发送请求的URL。默认是当前页面
|username|	String|	规定在HTTP访问认证请求中使用的用户名
|xhr	|Function|	用于创建XMLHttpRequest对象的函数

比如
```javascript
$.ajax({
  url : "checkUsername",
  type : "post",
  dataType : "text",
  data : "username="+$("#username").val(),
  beforeSend : function(){
    if($("#username").val()==""){
      alert("用户名不能为空");
      return false;
    }
    return true;
  },
  success : function(data){
    alert(data);
  }
});
```

数组（Array）用方括号(“[]”)表示。

对象（0bject）用大括号(“{}”)表示。

名称/值对(name/value）组合成数组和对象。

名称(name）置于双引号中，值（value）有字符串、数值、布尔值、null、对象和数组。

并列的数据之间用逗号(“,”）分隔