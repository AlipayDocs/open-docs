SJS 支持部分 ES6 语法。

# let & const

```javascript
function test() {
  let a = 5;
  if (true) {
    let b = 6;
  }
  console.log(a); // 5
  console.log(b); // ReferenceError: b is not defined 引用错误：b 未定义
}
```

# 箭头函数

```javascript
const a = [1, 2, 3];
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

# 更简洁的对象字面量（enhanced object literal）

```JavaScript
var handler = 1;
var obj = {
  handler, // 对象属性，变量名与属性名相同时可以省略属性名
  toString() { // 对象方法，使用简洁语法定义
    return "string";
  },
};
```

**注意**：不支持 `super` 关键字，不能在对象方法中使用 `super`。

# 模板字符串（template string）

```JavaScript
const h = 'hello';
const msg = `${h} alipay`;
```

**说明**：使用模板字符串，可以在字符串中嵌入变量。使用反引号(``)包裹字符串，并在变量名前添加美元符号（$）和大括号（{}）。
# 解构赋值（Destructuring）

```JavaScript
// 数组解构赋值
var [a, , b] = [1, 2, 3];
a === 1;
b === 3;

// 对象解构赋值
var { op: a, lhs: { op: b }, rhs: c }
       = getASTNode();

// 对象解构赋值简写
var { op, lhs, rhs } = getASTNode();

// 函数参数解构赋值
function g({ name: x }) {
  console.log(x);
}
g({ name: 5 });

// 解构赋值默认值
var [a = 1] = [];
a === 1;

// 函数参数解构赋值加默认值
function r({ x, y, w = 10, h = 10 }) {
  return x + y + w + h;
}
r({ x: 1, y: 2 }) === 23;
```
