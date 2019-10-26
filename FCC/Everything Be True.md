所有的东西都是真的！

完善编辑器中的every函数，如果集合(collection)中的所有对象都存在对应的属性(pre)，并且属性(pre)对应的值为真。函数返回ture。反之，返回false。

记住：你只能通过中括号来访问对象的变量属性(pre)。

提示：你可以有多种实现方式，最简洁的方式莫过于Array.prototype.every()。

every([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy", "sex": "male"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex") 应该返回 true。

every([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex") 应该返回 false。

every([{"user": "Tinky-Winky", "sex": "male", "age": 0}, {"user": "Dipsy", "sex": "male", "age": 3}, {"user": "Laa-Laa", "sex": "female", "age": 5}, {"user": "Po", "sex": "female", "age": 4}], "age") 应该返回 false。

every([{"name": "Pete", "onBoat": true}, {"name": "Repeat", "onBoat": true}, {"name": "FastFoward", "onBoat": null}], "onBoat") 应该返回 false

every([{"name": "Pete", "onBoat": true}, {"name": "Repeat", "onBoat": true, "alias": "Repete"}, {"name": "FastFoward", "onBoat": true}], "onBoat") 应该返回 true

every([{"single": "yes"}], "single") 应该返回 true

every([{"single": ""}, {"single": "double"}], "single") 应该返回 false

every([{"single": "double"}, {"single": undefined}], "single") 应该返回 false

every([{"single": "double"}, {"single": NaN}], "single") 应该返回 false



```
思路： 我能想到的是数组循环，如果存在一个len+1.当len==collection.length则为true
function every(collection, pre) {
  // Is everyone being true?
  var result = false;
  var len = 0;
  collection.map((x)=>{
    if(x[pre]){
      len+=1;
    }
  });
  if(len == collection.length){
    result = true;
  }else{
    result = false;
  }
  return result;
}

every([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy", "sex": "male"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex");


2、用下面这个方法比较简单，只要有一个不存在则返回false否则为true
function every(collection, pre) {
  // Is everyone being true?

  for(var i in collection){
    if(!collection[i][pre]){
      return false;
    }
  }
  return true;
}

every([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy", "sex": "male"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex");

```
