Map the Debris  
返回一个数组，其内容是把原数组中对应元素的平均海拔转换成其对应的轨道周期.

原数组中会包含格式化的对象内容，像这样 {name: 'name', avgAlt: avgAlt}.

至于轨道周期怎么求，戳这里 on wikipedia (不想看英文的话可以自行搜索以轨道高度计算轨道周期的公式).

求得的值应该是一个与其最接近的整数，轨道是以地球为基准的.

地球半径是 6367.4447 kilometers, 地球的GM值是 398600.4418, 圆周率为Math.PI

当你遇到困难的时候，记得查看错误提示、阅读文档、搜索、提问。

这是一些对你有帮助的资源:

[Math.pow()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/pow)  

orbitalPeriod([{name : "sputnik", avgAlt : 35873.5553}]) 应该返回 [{name: "sputnik", orbitalPeriod: 86400}].  
orbitalPeriod([{name: "iss", avgAlt: 413.6}, {name: "hubble", avgAlt: 556.7}, {name: "moon", avgAlt: 378632.553}]) 应该返回 [{name : "iss", orbitalPeriod: 5557}, {name: "hubble", orbitalPeriod: 5734}, {name: "moon", orbitalPeriod: 2377399}].  

```
function orbitalPeriod(arr){ //公式GMm/R^2=mrω^2 ω=2π/T，R=r+h，所以T=2π(r+h)·sqr((r+h)/GM)。
  var GM = 398600.4418;
  var earthRadius = 6367.4447;

  arr.map((x)=>{
    var R = x.avgAlt + earthRadius;
    var T = 2*Math.PI*R*Math.sqrt(R/GM);
    delete x.avgAlt;
    x.orbitalPeriod = Math.round(T);
  });
  
  return arr;
}

orbitalPeriod([{name : "sputnik", avgAlt : 35873.5553}]);

```
