Validate US Telephone Numbers
如果传入字符串是一个有效的美国电话号码，则返回 true.

用户可以在表单中填入一个任意有效美国电话号码. 下面是一些有效号码的例子(还有下面测试时用到的一些变体写法):

555-555-5555
(555)555-5555
(555) 555-5555
555 555 5555
5555555555
1 555 555 5555
在本节中你会看见如 800-692-7753 or 8oo-six427676;laskdjf这样的字符串. 你的任务就是验证前面给出的字符串是否是有效的美国电话号码. 区号是必须有的. 如果字符串中给出了国家代码, 你必须验证其是 1. 如果号码有效就返回 true ; 否则返回 false.

当你遇到困难的时候，记得查看错误提示、阅读文档、搜索、提问。

这是一些对你有帮助的资源:

[RegExp](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)

telephoneCheck("555-555-5555") 应该返回一个布尔值.

telephoneCheck("1 555-555-5555") 应该返回 true.

telephoneCheck("1 (555) 555-5555") 应该返回 true.

telephoneCheck("5555555555") 应该返回 true.

telephoneCheck("555-555-5555") 应该返回 true.

telephoneCheck("(555)555-5555") 应该返回 true.

telephoneCheck("1(555)555-5555") 应该返回 true.

telephoneCheck("1 555)555-5555") 应该返回 false.

telephoneCheck("1 555 555 5555") 应该返回 true.

telephoneCheck("1 456 789 4444") 应该返回 true.

telephoneCheck("123**&!!asdf#") 应该返回 false.

telephoneCheck("55555555") 应该返回 false.

telephoneCheck("(6505552368)") 应该返回 false

telephoneCheck("2 (757) 622-7382") 应该返回 false.

telephoneCheck("0 (757) 622-7382") 应该返回 false.

telephoneCheck("-1 (757) 622-7382") 应该返回 false

telephoneCheck("2 757 622-7382") 应该返回 false.

telephoneCheck("10 (757) 622-7382") 应该返回 false.

telephoneCheck("27576227382") 应该返回 false.

telephoneCheck("(275)76227382") 应该返回 false.

telephoneCheck("2(757)6227382") 应该返回 false.

telephoneCheck("2(757)622-7382") 应该返回 false.

telephoneCheck("555)-555-5555") 应该返回 false.

telephoneCheck("(555-555-5555") 应该返回 false.


```
function telephoneCheck(str) {
  // 祝你好运
  var regStr = /^1? ?(\d{3}|\(\d{3}\))[ -]?\d{3}[ -]?\d{4}$/;
  return regStr.test(str);
}

telephoneCheck("555-555-5555");

```