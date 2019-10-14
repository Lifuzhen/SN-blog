将字符串中的字符 &、<、>、" （双引号）, 以及 ' （单引号）转换为它们对应的 HTML 实体。

如果你被卡住了，记得开大招 Read-Search-Ask。尝试与他人结伴编程、编写你自己的代码。

这是一些对你有帮助的资源:

[RegExp](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)

[HTML Entities](https://dev.w3.org/html5/html-author/charref)

convert("Dolce & Gabbana") 应该返回 Dolce &​amp; Gabbana。

convert("Hamburgers < Pizza < Tacos") 应该返回 Hamburgers &​lt; Pizza &​lt; Tacos。

convert("Sixty > twelve") 应该返回 Sixty &​gt; twelve。

convert('Stuff in "quotation marks"') 应该返回 Stuff in &​quot;quotation marks&​quot;。

convert("Shindler's List") 应该返回 Shindler&​apos;s List。

convert("<>") 应该返回 &​lt;&​gt;。

convert("abc") 应该返回 abc。



```
function convert(str) {
  // &colon;&rpar;
  //正则表达式数组
  var arr=[/&/,/</,/>/,/"/,/'/];
  //对应的替换的html元素
  var duiarr=["&amp;","&lt;","&gt;",'&quot;',"&apos;"];
   for(var i=0;i<arr.length;i++){
     for(var j=0;j<str.length;j++){
       if(arr[i].test(str[j])){
         str= str.replace(str[j],duiarr[i]);
       }
     }
   }
  return str;
}
convert("Dolce & Gabbana");
```
