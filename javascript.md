後置インクリメント/デクリメント

```js
var a = 1;
b = a++;
console.log(b); //=> 1
c = b--;
console.log(c); //=> 2
```

前置インクリメント/デクリメント

```js
var a = 1;
b = ++a;
console.log(b); //=> 2
c = --b;
console.log(c); //=> 1
```

プリミティブデータ型

- Number: 数値。整数と浮動小数点数を含む。
- String: 文字列。
- Boolean: `true`と`false`。
- undefined: 存在していない変数、または初期化していない変数にアクセスした場合に得られるもの。
- null: 何もない、を表現するもの。

以上に属さない値はオブジェクトとなる。
ただし、`null`は「何もない」を表すオブジェクト。

変数の型を知る

`typeof`演算子は`number`、`string`、`boolean`、`undefined`、`object`、`function`のいずれかの文字列を返す。

```js
console.log(typeof(null)); //=> object
```

二重否定

Boolean型に変換する簡単な方法として、`!!`を用いる方法がある。

```js
console.log(!!true); //=> true
console.log(!!0);    //=> false
console.log(!!NaN);  //=> false
```

変数が未定義または`false`なら代入

```js
var a = a || 1;
console.log(a); //=> 1
```

等価比較、等価比較および型比較

`==`演算子は比較前に同じ方に変換される。
変換しない場合は`===`を用いる。

```js
var a = 1;
var b = '1';

console.log(a == b);  //=> true
console.log(a === b); //=> false
```

配列の定義・追加・削除

配列は`[]`で定義する。
新しい要素を追加する際はインデックスを指定する。
このとき、既存の要素との間に隙間があると`undefined`が割り当てられる。
要素の削除は`delete()`で行なう。

```js
var a = [1, 2, 3];

a[4] = 5;
console.log(a);    //=> [ 1, 2, 3, , 5 ]
console.log(a[3]); //=> undefined

delete(a[1]);
console.log(a); //=> [ 1, , 3, , 5 ]
```

三項演算子

```js
var a = true ? 1 : 2;
console.log(a); //=> 1
```

switch文

- 各`case`に`break`をつける
- オプションで`default`節をつけることができる

```js
var a = 1;
var b = '';
switch(a) {
  case 1:
    b = 'foo';
    break;
  case 2:
    b = 'bar';
    break;
  default:
    b = 'baz';
}
console.log(b); //=> foo
```

while文

条件文の評価が`true`の間、コードブロックが実行され続ける。

```js
var i = 1;
while (i < 10) {
  i++;
}
console.log(i); //=> 10
```

for文

初期化、条件式、インクリメントの3つからなる。

```js
var sum = 0;
for (var i = 0; i < 10; i++) {
  sum += i;
}
console.log(sum); //=> 45
```

for-in文

```js
var a = { a: 1, b: 2, c: 3 };
for (key in a) {
  console.log(a[key]); //=> 1 2 3
}
```
