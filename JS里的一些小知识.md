## 页面重新定向

demo1

```
<html>
   <head>
      <script type = "text/javascript">
         <!--
            function Redirect() {
               window.location = "https://www.tutorialspoint.com";
            }
         //-->
      </script>
   </head>
   
   <body>
      <p>Click the following button, you will be redirected to home page.</p>
      
      <form>
         <input type = "button" value = "Redirect Me" onclick = "Redirect();" />
      </form>
      
   </body>
</html>
```

demo2<br>
以下示例说明如何根据浏览器将网站访问者重定向到其他网页。

```
<html>
   <head>     
      <script type = "text/javascript">
         <!--
            var browsername = navigator.appName;
            if( browsername == "Netscape" ) {
               window.location = "http://www.location.com/ns.htm";
            } else if ( browsername =="Microsoft Internet Explorer") {
               window.location = "http://www.location.com/ie.htm";
            } else {
               window.location = "http://www.location.com/other.htm";
            }
         //-->
      </script>      
   </head>
   
   <body>
   </body>
</html>
```

## 注释

用于不支持js的浏览器，如果你想在不支持js的浏览器里保留你的js代码<br>

```
<html>
<head>
<script>
  <!--
    alert('hello');
  //-->
</script>
</head>
<body>
  
</body>
</html>
```

## 打印页面（不推荐）

```
<input type = "button" value = "Print" onclick = "window.print()" />
```

