# use strict 是什麼？

use strict 是 JS 中的一種嚴格模式。它告訴 JS 引擎在執行代碼時要採用更嚴格的解析和執行方式。這有助於捕捉一些常見的錯誤，並提高代碼的安全性和性能。

## 使用 use strict 的方式

1. 在 JS script 的頂部

在這種方式下，整個內文都會採用嚴格模式。

```javascript
"use strict";
function myFunction() {
  // 在這裡，所有代碼都會採用嚴格模式
  var x = 3.14; // 正確
  y = 3.14; // 錯誤，y 未定義
}
myFunction();

...
...
...
```


2. 在函數內部
在這種方式下，只有函數內部的代碼會採用嚴格模式。

```javascript
function myFunction() {
  "use strict";
  var x = 3.14; // 正確
  y = 3.14; // 錯誤，y 未定義
}
myFunction();
``` 

## 嚴格模式的目的

嚴格模式的目的是為了提高 JavaScript 程式碼的安全性和可讀性。它可以幫助開發者捕捉一些常見的錯誤，並防止一些不安全的操作。


### 一些實際範例

1. 禁止使用未經聲明的變數

```javascript
"use strict";
function myFunction() {
  x = 3.14; // 錯誤，x 未聲明
  // Uncaught ReferenceError: x is not defined
}
myFunction();
``` 

2. 禁止重複定義變數

```javascript
"use strict";
function myFunction() {
  var x = 3.14;
  var x = 2.71; // 錯誤，x 已經被定義
  // Uncaught SyntaxError: Duplicate parameter name not allowed in this context
}
myFunction();
``` 

3. 禁止刪除不可刪除的屬性

```javascript
"use strict";

var y = 20;
delete y;
// Uncaught SyntaxError: Delete of an unqualified identifier in strict mode.
```

4. 禁止使用 with 語句

```javascript
"use strict";
function myFunction() {
  var obj = { a: 1, b: 2 };
  with (obj) {
    console.log(a); // 錯誤，with 語句在嚴格模式下被禁止
  }
  // Uncaught SyntaxError: Strict mode code may not include a with statement
}
myFunction();
``` 

5. 禁止使用 eval 來定義變數

嚴格模式下，eval 仍然可以宣告變數，但這些變數只存在於 eval 的區塊作用域內，不會污染外部作用域。

```javascript
"use strict";
eval("var x = 3.14;");
console.log(typeof x); // undefined，x 不會被加到外部作用域
``` 

6. 禁止使用 arguments.callee

```javascript
"use strict";
function myFunction() {
  console.log(arguments.callee); // 錯誤，arguments.callee 在嚴格模式下被禁止
  // Uncaught TypeError: Cannot read properties of undefined
}
myFunction();
```

7. 禁止使用 this 關鍵字指向全局對象

```javascript
"use strict";
function myFunction() {
  console.log(this); // 在嚴格模式下，this 不會指向全局對象
  // 在瀏覽器中，this 會是 undefined
}
myFunction();
```

8. 禁止使用八進位字面量

```javascript
"use strict";
var x = 010; // 錯誤，八進位字面量
// Uncaught SyntaxError: Octal literals are not allowed in strict mode.
```

9. 禁止使用 getter 和 setter 的重複定義

```javascript
"use strict";
var obj = {
  get x() {
    return 10;
  },
  set x(value) {
    console.log(value);
  },
  get x() { // 錯誤，getter 重複定義
    return 20;
  }
};
// Uncaught SyntaxError: Duplicate data property in object literal not allowed in strict mode
``` 

10. 禁止使用 eval 來定義函數

```javascript
"use strict";
eval("function myFunction() {}"); // 錯誤，eval 在嚴格模式下不能定義函數
// Uncaught SyntaxError: Using eval in strict mode
``` 

## 總結
use strict 是 JavaScript 中的一種嚴格模式，它可以幫助開發者捕捉一些常見的錯誤，並提高代碼的安全性和性能。使用嚴格模式可以避免一些不安全的操作，並使代碼更加可讀和易於維護。建議在開發 JavaScript 應用時，始終使用嚴格模式，以提高代碼的質量和安全性。

不過現代前端框架和工具（如 Babel、Webpack）通常會自動加上嚴格模式摟！

