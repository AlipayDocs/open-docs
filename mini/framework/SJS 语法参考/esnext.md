SJS 支持部分 ES6 语法。

# let & const
```javascript
function test(){
  let a = 5;
  if (true) {
    let b = 6;
  }
  console.log(a); // 5
  console.log(b); // 引用错误：b 未定义
}
```

# 箭头函数
```
const a = [1,2,3];
const double = x => x * 2; // 箭头函数
console.log(a.map(double));
var bob = {
  _name: "Bob",
  _friends: [],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
};
console.log(bob.printFriends());
```

#  更简洁的对象字面量（enhanced object literal）
```
var handler = 1;
var obj = {
  handler, // 对象属性
  toString() { // 对象方法
	return "string";
  },
};
```
**注意**：不支持 super 关键字，不能在对象方法中使用 super。

# 模板字符串（template string）
```
const h = 'hello';
const msg = `${h} alipay`;
```

# 解构赋值（Destructuring）
```
// array 解构赋值
var [a, ,b] = [1,2,3];
a === 1;
b === 3;
// 对象解构赋值
var { op: a, lhs: { op: b }, rhs: c }
       = getASTNode();
// 对象解构赋值简写
var {op, lhs, rhs} = getASTNode();
// 函数参数解构赋值
function g({name: x}) {
  console.log(x);
}
g({name: 5});
// 解构赋值默认值
var [a = 1] = [];
a === 1;
// 函数参数：解构赋值 + 默认值
function r({x, y, w = 10, h = 10}) {
  return x + y + w + h;
}
r({x:1, y:2}) === 23;
```
