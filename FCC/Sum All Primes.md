求小于等于给定数值的质数之和。

只有 1 和它本身两个约数的数叫质数。例如，2 是质数，因为它只能被 1 和 2 整除。1 不是质数，因为它只能被自身整除。

给定的数不一定是质数。

如果你被卡住了，记得开大招 Read-Search-Ask。尝试与他人结伴编程、编写你自己的代码。

这是一些对你有帮助的资源:

[For Loops](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for)

[Array.push()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

sumPrimes(10) 应该返回一个数字。

sumPrimes(10) 应该返回 17。

sumPrimes(977) 应该返回 73156。

```
function sumPrimes(num) {
  var arr =[];
  for(var i=2; i<=num; i++){
    var tmp = true;
     for(var j=2; j<i; j++){
      if(i%j === 0){tmp = false;break;}
    }
    if(tmp){
      arr.push(i);
    }
  }
  console.log(arr);
  return arr.reduce((a,b)=>{
    return a+b;
  });
};

sumPrimes(977);

```