## undefined 與 null 的區別 ?

undefined 與 null 使用上有意義上的區別，意思是：

1. `undefined` 是尚未被賦值的變數，這邊有尚未的含義在，所以在一段時間之後他是有可能被賦值。

2. `null` 是明確的賦值給變數，表示這個變數沒有值。

舉例：

這邊 user 的大頭照有可能沒有值，所以可以使用 null 當作 fallback 值。

而 users 的型別為 `UserDTO[] | undefined` 表示有可能該變數尚未取得資料，但一旦取得資料後就會是 `UserDTO[]` 的型別。

```javascript
type UserData = {
  id: string,
  firstName: string,
  lastName: string,
  profilePicture: string | null,
};

const users: UserData[] | undefined = await fetchUsers();
```

## undefined 與 undeclared 的區別 ?

* undeclared 是指連宣告都還沒有。
* undefined 是指已經宣告了，但沒有賦值。

```javascript
let a; // undeclared
console.log(a); // undefined
let b = undefined; // declared but undefined
console.log(b); // undefined
```
一般來說，undeclared 會報錯長這樣：

```javascript
console.log(x); // Uncaught ReferenceError: x is not defined
```