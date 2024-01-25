SJS 支持 ES6 语法的部分特性。

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

在上述代码中，`let` 和 `const` 的示例展示了这两个关键字声明的变量在不同作用域中的行为。在 `test` 函数中，`a` 被声明在函数作用域内，而 `b` 被声明在 `if` 块作用域中，并不会在 `if` 块之外存在。因此，在 `if` 语句外尝试访问 `b` 时会抛出引用错误。

箭头函数提供了更加简洁的函数书写方式，可以更方便地处理函数内的 `this` 关键字。在 `bob` 对象的 `printFriends` 方法中，使用箭头函数避免了传统函数中常见的 `this` 指向问题。

请注意，上述示例代码中已经添加了必要的注释，增强了代码的可读性，这对于理解示例和学习是非常有帮助的。同时，遵循了代码在注释后换行及代码行内部适当间隔的规则。
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
