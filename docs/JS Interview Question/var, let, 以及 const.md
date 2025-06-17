「在 JavaScript 中用 var, let, 以及 const 有什麼差別？」 算是蠻常見的面試題目之一。這三個關鍵字都用來宣告變數，但它們在作用域、提升（hoisting）、以及可變性方面有著不同的行為。

var, let, 以及 const 都是在 JavaScript 用來做變數宣告的保留字，在 JavaScript 早期只有 var，直到 ES2015 (ES6) 時才加入了 let 與 const 。

表格比較：
| 特性       | var                     | let                     | const                   |
|------------|-------------------------|-------------------------|-------------------------|
| scope     | 函數作用域或全局作用域   | 塊級作用域           | 塊級作用域           |
| Hoisting   | 會提升到函數或全局作用域的頂部 | 會提升到塊級作用域的頂部 | 會提升到塊級作用域的頂部 |
| 可變性     | 可以重新賦值和重新宣告   | 可以重新賦值，但不能重新宣告 | 不能重新賦值或重新宣告 |
| 初始化     | 可以在宣告前使用，但值為 undefined | 必須在宣告時初始化，否則報錯 | 必須在宣告時初始化，否則報錯 |

## 解釋表格以及一些範例

1. scope 

* var 宣告在全域
用 var 宣告在全域作用域的變數，可以在整個程式中存取，換句話說就會成為 window 物件的屬性。 

```javascript
var globalVar = "I am a global variable";
console.log(window.globalVar); // "I am a global variable"
```

* let, const 宣告在全域
用 let 或 const 宣告在全域作用域的變數，則不會成為 window 物件的屬性。

```javascript 
let globalLet = "I am a global let variable";
const globalConst = "I am a global const variable";
console.log(window.globalLet); // undefined
console.log(window.globalConst); // undefined
```

* 如果在函式內宣告的變數（不論 var、let、const），都只屬於該函式的區域作用域（scope），外部無法直接存取。

2. Hoisting
* var 的提升
在使用 var 宣告的變數時，JavaScript 會將其提升到函式或全域作用域的頂部，但變數的值仍然是 undefined，直到賦值為止。

```javascript
console.log(varVar); // undefined
var varVar = "I am a var variable";
console.log(varVar); // "I am a var variable"
```

* let 和 const 的提升
let 和 const 也會被提升到塊級作用域的頂部，但在使用之前不能存取，否則會拋出 ReferenceError。
```javascript
console.log(letVar); // ReferenceError: Cannot access 'letVar' before initialization
let letVar = "I am a let variable";
console.log(constVar); // ReferenceError: Cannot access 'constVar' before initialization
const constVar = "I am a const variable";
```

3. 可變性
* var 可以重新賦值和重新宣告
```javascript
var varVar = "I can be changed";
varVar = "I have been changed";
console.log(varVar); // "I have been changed"
var varVar = "I can be redeclared";
console.log(varVar); // "I can be redeclared"
```

* let 可以重新賦值，但不能重新宣告
```javascript
let letVar
letVar = "I can be changed";
console.log(letVar); // "I can be changed"
// let letVar = "I can be redeclared"; // SyntaxError: Identifier 'letVar' has already been declared
``` 

* const 不能重新賦值或重新宣告
```javascript
const constVar = "I cannot be changed";
// constVar = "I have been changed"; // TypeError: Assignment to constant variable
// const constVar = "I can be redeclared"; // SyntaxError: Identifier 'constVar' has already been declared
console.log(constVar); // "I cannot be changed"
```

4. 初始化
* var 可以在宣告前使用，但值為 undefined
```javascript
console.log(varVar); // undefined
var varVar = "I am a var variable";
console.log(varVar); // "I am a var variable"
```

* let 和 const 必須在宣告時初始化，否則會報錯

```javascript
// console.log(letVar); // ReferenceError: Cannot access 'letVar' before initialization
let letVar = "I am a let variable";
console.log(letVar); // "I am a let variable"
// console.log(constVar); // ReferenceError: Cannot access 'constVar' before initialization
const constVar = "I am a const variable";
console.log(constVar); // "I am a const variable"
```
補充：

如何在 Console 看到 TDZ 的錯誤？
你可以一次貼上多行，讓它們在同一個 script context 執行，例如：
```javascript
{
  console.log(a);
  let a = 10;
}
```
在瀏覽器的 console 中會需要這樣執行是因為，在瀏覽器 Console 裡，每按一次 Enter 執行的就是一個新的 Script 執行單位。所以跟 JS script 檔案的行為不同。所以這邊必須匡住一個區塊，讓它們在同一個 script context 執行。
這樣就可以看到 TDZ 的錯誤了。

## 總結
var、let 和 const 都是用來宣告變數的關鍵字，但它們在作用域、提升和可變性方面有著不同的行為。一般來說，建議在現代 JavaScript 開發中使用 let 和 const，因為它們提供了更嚴格的作用域控制和更清晰的代碼意圖。具體使用哪一個取決於你的需求：
- 如果需要一個可以重新賦值的變數，使用 let。
- 如果需要一個不可變的常量，使用 const。
- 如果需要向後兼容或處理全局變數，則可以使用 var，但應該謹慎使用，因為它可能導致意外的行為。
這樣可以提高代碼的可讀性和可維護性，並減少錯誤的可能性。