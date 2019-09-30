
之前碰到过在pc端的微信打开一个页面，告诉我只能在手机端的微信内置浏览器中打开。

效果如下所示：

![](../assets/判断页面是在手机端还是在PC端打开/01.png)

navigator.userAgent : 浏览器用于 HTTP 请求的用户代理头的值，通过UserAgent可以取得浏览器类别、版本，客户端操作系统等信息。

本地输出一下，如下显示：
```
console.log(navigator.userAgent);
//Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.90 Mobile Safari/537.36
```

```
<html>
    <title>判断是页面是在手机端还是PC端打开</title>
    <head>
        <link href="https://cdn.bootcss.com/weui/2.1.2/style/weui.min.css" rel="stylesheet">
    </head>
    <body>
        <script>
            const sUserAgent = navigator.userAgent.toLowerCase();
            const pad = sUserAgent.match(/ipad/i) == "ipad";//是否是ipad设备
            const iphone = sUserAgent.match(/iphone os/i) == "iphone os";//是否是iphone设备
            const android = sUserAgent.match(/android/i) == "android";//是否是安卓设备
            const ce = sUserAgent.match(/windows ce/i) == "windows ce";
            const wm = sUserAgent.match(/windows mobile/i) == "windows mobile";
            const wcBrowser = sUserAgent.match(/MicroMessenger/i)=="micromessenger";//判断当前是否是微信环境
            
            if (pad || iphone || android || ce || wm) {
                console.log("手机端");
                if(wcBrowser){
                    console.log("手机端微信内置浏览器")
                }else{
                    console.log("手机端但不是微信内置浏览器")
                    document.body.innerHTML = '<div class="weui_msg"><div class="weui_icon_area"><i class="weui_icon_info weui_icon_msg"></i></div><div class="weui_text_area"><h4 class="weui_msg_title">请在微信内置浏览器打开链接</h4></div></div>';
                }
            } else {
                console.log("")
                document.body.innerHTML = '<div class="weui_msg"><div class="weui_icon_area"><i class="weui_icon_info weui_icon_msg"></i></div><div class="weui_text_area"><h4 class="weui_msg_title">请在移动端微信打开链接</h4></div></div>';
            }
        </script>
    </body>
</html>
```

![](../assets/判断页面是在手机端还是在PC端打开/04.png)
![](../assets/判断页面是在手机端还是在PC端打开/04.jpg)

最终的显示效果（限制用户只能在移动端的微信内置浏览器中打开）：

![](../assets/判断页面是在手机端还是在PC端打开/02.png)
