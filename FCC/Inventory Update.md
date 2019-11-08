Inventory Update  
依照一个存着新进货物的二维数组，更新存着现有库存(在 arr1 中)的二维数组. 如果货物已存在则更新数量 . 如果没有对应货物则把其加入到数组中，更新最新的数量. 返回当前的库存数组，且按货物名称的字母顺序排列.  

当你遇到困难的时候，记得查看错误提示、阅读文档、搜索、提问。  

这是一些对你有帮助的资源:  

[Global Array Object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)  

updateInventory() 应该返回一个数组.  
updateInventory([[21, "Bowling Ball"], [2, "Dirty Sock"], [1, "Hair Pin"], [5, "Microphone"]], [[2, "Hair Pin"], [3, "Half-Eaten Apple"], [67, "Bowling Ball"], [7, "Toothpaste"]]).length 应该返回一个长度为6的数组.  
updateInventory([[21, "Bowling Ball"], [2, "Dirty Sock"], [1, "Hair Pin"], [5, "Microphone"]], [[2, "Hair Pin"], [3, "Half-Eaten Apple"], [67, "Bowling Ball"], [7, "Toothpaste"]]) 应该返回 [[88, "Bowling Ball"], [2, "Dirty Sock"], [3, "Hair Pin"], [3, "Half-Eaten Apple"], [5, "Microphone"], [7, "Toothpaste"]]. 
updateInventory([[21, "Bowling Ball"], [2, "Dirty Sock"], [1, "Hair Pin"], [5, "Microphone"]], []) 应该返回 [[21, "Bowling Ball"], [2, "Dirty Sock"], [1, "Hair Pin"], [5, "Microphone"]].  
updateInventory([], [[2, "Hair Pin"], [3, "Half-Eaten Apple"], [67, "Bowling Ball"], [7, "Toothpaste"]]) 应该返回 [[67, "Bowling Ball"], [2, "Hair Pin"], [3, "Half-Eaten Apple"], [7, "Toothpaste"]].  
updateInventory([[0, "Bowling Ball"], [0, "Dirty Sock"], [0, "Hair Pin"], [0, "Microphone"]], [[1, "Hair Pin"], [1, "Half-Eaten Apple"], [1, "Bowling Ball"], [1, "Toothpaste"]]) 应该返回 [[1, "Bowling Ball"], [0, "Dirty Sock"], [1, "Hair Pin"], [1, "Half-Eaten Apple"], [0, "Microphone"], [1, "Toothpaste"]].  



```
function updateInventory(arr1, arr2) {
    // 请保证你的代码考虑到所有情况
  var arr = arr1;
  //console.log(arr2);
  if(arr1.length == 0){
    arr = arr2;
  }else if(arr2.length == 0){
    arr = arr1;
  }else{
     for(var i=0; i<arr2.length;i++){
      var f = true;
      for(var j=0;j<arr.length;j++){
        if(arr2[i][1] == arr[j][1]){
          arr[j][0]+=arr2[i][0];
          f = false;
          break;
        }
      }
      if(f){
        arr.push(arr2[i]);
      }
    }
  }
return arr.sort(function(a,b){
      return a[1].charCodeAt(0)-b[1].charCodeAt(0);
  });
}
/*
刚开始的时候排序用的a[1][0]>b[1][0]?1:0但是没有起作用，后来看到人家的代码改成了charCodeAt(0)
*/
// 仓库库存示例
var curInv = [];

var newInv = [[2, "Hair Pin"], [3, "Half-Eaten Apple"], [67, "Bowling Ball"], [7, "Toothpaste"]];

updateInventory(curInv, newInv);




网上借鉴代码

function updateInventory(arr1, arr2) {
    // All inventory must be accounted for or you're fired!
  
    for (var i = 0; i < arr2.length; i++) {
      for (var j = 0; j < arr1.length; j++) {
        if (arr1[j][1] === arr2[i][1]) {
          arr1[j][0] += arr2[i][0];
          break;
        }
      }
      
      if (j == arr1.length) {
        arr1.push (arr2[i]);
      }
    }
  
    return arr1.sort(function(a, b) {
      return a[1].charCodeAt(0) - b[1].charCodeAt(0);
    });
}

// Example inventory lists
var curInv = [
    [21, "Bowling Ball"],
    [2, "Dirty Sock"],
    [1, "Hair Pin"],
    [5, "Microphone"]
];

var newInv = [
    [2, "Hair Pin"],
    [3, "Half-Eaten Apple"],
    [67, "Bowling Ball"],
    [7, "Toothpaste"]
];

updateInventory(curInv, newInv);

```