将字符串转换为 spinal case。Spinal case 是 all-lowercase-words-joined-by-dashes 这种形式的，也就是以连字符连接所有小写单词。

如果你被卡住了，记得开大招 Read-Search-Ask。尝试与他人结伴编程、编写你自己的代码。

这是一些对你有帮助的资源:

[RegExp](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)

[String.replace()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

spinalCase("This Is Spinal Tap") 应该返回 "this-is-spinal-tap"。

spinalCase("thisIsSpinalTap") 应该返回 "this-is-spinal-tap"。

spinalCase("The_Andy_Griffith_Show") 应该返回 "the-andy-griffith-show"。

spinalCase("Teletubbies say Eh-oh") 应该返回 "teletubbies-say-eh-oh"。

难点在“thisIsSpinalTap”这里没有空格下短划线，单独用大写字母区分了单词。所以要从大写字母入手

str.replace(/([A-Z])/g,"$1");  //在每一个大写字母前面添加一个空格

 $1:  第1个小括号捕获的内容
![](../assets/Spinal%20Tap%20Case/regExp.jpg)
执行后结果：
![](../assets/Spinal%20Tap%20Case/result01.jpg)

 str.replace(/^\s/g,"");//将第一个匹配的空白符，包括空格、制表符、换页符、换行符和其他 Unicode 空格去掉
 
 这个防止上图中首个单词前面的空格影响结果
str.replace(/_/g,"");//将_去掉

str.toLowerCase();//所有字母转换成小写

str.replace(/\s+/g,"-");//将匹配的空白符，包括空格、制表符、换页符、换行符和其他 Unicode 空格换成“-” 

串起来就是我们要的最终的结果：
![](../assets/Spinal%20Tap%20Case/result02.jpg);
```
function spinalCase(str) {
  return str.replace(/([A-Z])/g," $1").replace(/^\s/g,"").replace(/_/g,"").toLowerCase().replace(/\s+/g,"-");
}

spinalCase('thisIsSpinalTap');
```