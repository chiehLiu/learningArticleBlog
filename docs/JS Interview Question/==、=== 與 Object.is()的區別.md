在這邊介紹以下三種 JavaScript 中比較相等與否的方式：

* `===` (嚴格比較)
* `==` (鬆散比較)
* `Object.is` (同值比較)

## `==` (鬆散比較)
`==` 在比較值之前，會先強制轉換型別與值，然後再進行比較。這意味著如果兩個值的型別不同，JavaScript 會嘗試將它們轉換為相同的型別。

這邊舉例：
```
console.log(1 == "1"); // true
console.log(0 == false); // true
console.log(undefined == null); // true
```

## `===` 嚴格比較 (strict equality)
`===` 在比較值時，不會進行型別轉換。只有當兩個值的型別和內容都相同時，才會返回 `true`。
這意味著如果兩個值的型別不同，則會返回 `false`。

有兩個情況例外：
```
+0 === -0; // true
NaN === NaN; // false
```

## `Object.is` 同值比較 (same-value equality)
`Object.is` 是一個用來比較兩個值是否相等的方法。它的行為類似於 `===`，但有一些細微的差異。
`Object.is` 在比較時不會進行型別轉換，並且對於 `NaN` 和 `-0` 的處理方式與 `===` 不同。  

雖然它是 Object 開頭，但比較的可以是任意的兩個值。

```
console.log(Object.is(1, 1)); // true
console.log(Object.is(1, "1")); // false
```

因為不會轉型的緣故，上面提到在嚴格比較出現的例外就可以在這邊被辨識出來
```
console.log(Object.is(+0, -0)); // false
console.log(Object.is(NaN, NaN)); // true
```

如果真的要有效辨別 NaN 的話，也可以使用 `Number.isNaN()` 方法：
``` 
console.log(Number.isNaN(NaN)); // true
console.log(Number.isNaN("NaN")); // false
console.log(Number.isNaN(1)); // false
console.log(Number.isNaN(undefined)); // false
console.log(Number.isNaN(null)); // false
console.log(Number.isNaN("1")); // false
console.log(Number.isNaN("1" / 0)); // false
```

## 總結
* `==` 會進行型別轉換，可能會導致意外的結果。
* `===` 嚴格比較，不會進行型別轉換，只有當兩個值的型別和內容都相同時才返回 `true`。
* `Object.is` 同值比較，與 `===` 類似，但對於 `NaN` 和 `-0` 的處理方式不同。
* 在比較時，建議使用 `===` 或 `Object.is` 來避免意外的型別轉換。
* `Object.is` 可以用來比較任意兩個值，並且在處理 `NaN` 和 `-0` 時有更一致的行為。
* `Number.isNaN()` 可以用來有效辨別 `NaN`，並且不會對其他非數字類型的值進行轉換。