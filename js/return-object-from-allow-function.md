# アロー関数でオブジェクトを返す
アロー関数でそのままオブジェクトを返す時に、今までは下のように書いていた。
```js
const createObj = () => {
    return {
        foo: 'bar'
    }
}
```

次のように書くとreturnが不要になるらしい。
```js
const createObj = () => ({ foo: 'bar'})
```

## 参考
- [javascript - ECMAScript 6 arrow function that returns an object - Stack Overflow](https://stackoverflow.com/questions/28770415/ecmascript-6-arrow-function-that-returns-an-object)