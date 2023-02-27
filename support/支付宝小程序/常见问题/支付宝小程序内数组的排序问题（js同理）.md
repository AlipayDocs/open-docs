```
const arr1 = [  { x: 0, y: 0, key: "0" },
  { x: 0, y: 0, key: "1" },  { x: 0, y: 0, key: "1" }, 
  { x: 1, y: 1, key: "2" },  { x: 1, y: 2, key: "3" }, 
  { x: 2, y: 1, key: "4" }]; 
const arr2 = [  { x: 0, y: 0, key: "0" },
  { x: 0, y: 0, key: "1" },  
  { x: 0, y: 0, key: "2" },  
  { x: 0, y: 0, key: "3" },  
  { x: 0, y: 0, key: "4" },  
  { x: 0, y: 0, key: "5" }, 
  { x: 0, y: 0, key: "6" },  
  { x: 0, y: 0, key: "7" }, 
  { x: 0, y: 0, key: "8" }, 
  { x: 0, y: 0, key: "9" },  
  { x: 1, y: 1, key: "10" },  
  { x: 1, y: 2, key: "11" },  
  { x: 2, y: 1, key: "12" }]; 
//解决超过10数据后排序异常问题
1.增加第三个参数的判断。
(compare === 1时 a.x > b.x || (a.x === b.x && a.y > b.y)|| (a.x === b.x&& a.key > b.key && a.y === b.y))（compare === 0时 a.x === b.x && a.y === b.y&& a.key === b.key）)
//2.可以按照 compare === 0 的时候 直接返回 a.key - b.keyconst compare = (a, b) => {  if (a.x > b.x || (a.x === b.x && a.y > b.y)|| (a.x === b.x && a.key > b.key && a.y === b.y)) {    console.log("1a.x:"+a.x+" ,b.x:"+b.x);    console.log("1a.y:"+a.y+" ,b.y:"+b.y);    return 1;//第一个参数比第二个大  }  if (a.x === b.x && a.y === b.y && a.key === b.key) {     console.log("0a.x:"+a.x+" ,b.x:"+b.x);    console.log("0a.y:"+a.y+" ,b.y:"+b.y);    return 0;//两个参数相等  }   console.log("-1a.x:"+a.x+" ,b.x:"+b.x);
    console.log("-1a.y:"+a.y+" ,b.y:"+b.y);
      return -1;//第一个参数比第二个小}; 
  const sort = arr => {  return [...arr].sort(compare);}; 
  console.log(sort(arr1));
console.log(sort(arr2));
```

