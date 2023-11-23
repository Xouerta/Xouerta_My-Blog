# HTML BOM and DOM
## DOM tree
通过 DOM，可访问 HTML 文档中的每个节点

通过使用 getElementById() 和 getElementsByTagName() 方法 
通过使用一个元素节点的 parentNode、firstChild 以及 lastChild 属性

 ``` html
 <!Doctype html>
 <html lang='en'>
    <head>
        <meta charset='UTF-8'>
        ...
    </head> 
    <body>
      <div id="..">

        </div>
        <p>Genshi Impact start!</p>
        <a href="balabla.com">bala</a>
        <table>
         <tr>
           <td></td>
           <td></td>
         </tr>
        </table>
     </body>   
     <style>
        //balabala
        </style>
 <script>
document.getElementByid("index");
document.getElementById("p");
</script> 
</html>
 ```
getElementByid(id)
appendChild(node)
removeChild(node)

innerHTML 文本值
parentNode父节点
chilidNode子节点
attribues 

