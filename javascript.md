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

以下は同じ意味。

```js
var a = [];
var a = new Array();
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

関数

- 明示的に`return`を書かなければ`undefined`が返る。
- 引数の数が合わない場合：
  - 足りなければ、残りの引数は`undefined`がセットされる
  - 多ければ無視される

```js
function sum(a, b) {
  return a + b;
}
console.log(sum(1, 2)); //=> 3
```

arguments変数

関数内で、引数は自動的に`arguments`に格納される。
ただし、引数があることが分かりづらくなるため、使用には注意が必要。

```js
function sum() {
  var sum = 0;
  for (key in arguments) {
    sum += arguments[key];
  }
  return sum;
}
console.log(sum(1, 2, 3)); //=> 6
```

定義済み関数

parseInt() / parseFload()

数値への変換を試みる。
最初に未知の文字が現れた時点で変換を諦める。

```js
console.log(parseInt('123'));    //=> 123
console.log(parseInt('abc123')); //=> NaN
console.log(parseInt('1abc23')); //=> 1
console.log(parseInt('123abc')); //=> 123
console.log(parseFloat('123'));        //=> 123
console.log(parseFloat('1.23'));       //=> 1.23
console.log(parseFloat('1.23abc.00')); //=> 1.23
console.log(parseFloat('a.bc1.23'));   //=> NaN
```

isNaN()

NaNかどうかをチェックする。

```js
console.log(isNaN(NaN)); //=> true
console.log(isNaN(123)); //=> false
console.log(isNaN(parseInt('abc123'))); //=> true
```

encodeURI()

URIをエスケープする。

```js
console.log(encodeURI('http://www.example.com/?q=this and that'));
//=> http://www.example.com/?q=this%20and%20that
```

変数のスコープ

- `var`で定義すると、それより下位のブロックからアクセスできる
- `var`を省略して定義すると、自動的にグローバルスコープとして作成される

```js
var a = 1;
function foo() {
  var b = 2;
  c = 3;
  return a;
}
console.log(foo()); //=> 1
console.log(b);     //=> ReferenceError: b is not defined
console.log(c);     //=> 3
```

関数もデータ

以下の2通りの定義方法はまったく同じ結果を得る。

```js
function sum(a, b) {
  return a + b;
}
var sum = function(a, b) { return a + b; }
sum(1, 2); //=> 3
```

無名関数

コールバック関数

- グローバル変数を減らすことができる
- 関数呼び出しの責任を委譲できる

```js
function sum(a, b, callback) {
  var sum = a + b;
  return callback(sum);
}
sum(10, 20, function(sum) { return sum + 1 }) //=> 31
```

自己実行可能関数

一度だけ実行される処理（初期化など）に適している。

```js
(
  function(name) {
    return name;
  }
)('taro') //=> taro
```

プライベート関数

- グローバルの名前空間を汚染しない（グローバルでは`b()`は見えない）

```js
function a(x) {
  function b(y) {
    return Math.pow(y, 2);
  }

  return b(x);
}
a(2);
```

関数を返す関数

```js
function a() {
  return function() {
    return 1;
  }
}
a()();
```

自分自身を書き換える関数

一度しか実行させたくない関数を定義する場合に有用。

```js
function increment() {
  var x = 0;
  increment = function() {
    return x;
  }
  return ++x;
}
increment(); //=> 1
increment(); //=> 1
```

スコープ

- 関数`b()`の中では、`a`と`c`の両方が見える
- 関数`b()`の外では、`a`は見えるが`c`は見えない

```js
var a = 'foo';
function b() {
  var c = 'bar';
  return a;
};
b(); //=> foo
c;   //=> c is not defined
```

また、関数の中でネストされた関数を定義すると、ネストされた関数は親のスコープの変数にもアクセスできる（スコープチェーン）。

レキシカルスコープ

関数の定義時にスコープが作られる。
以下の場合、最初の`a()`実行時には`b()`から`c`は見えない。

```js
function a() {
  var c = 1;
  return b();
}
function b() {
  return c;
}
a(); //=> c is not defined
var c = 2;
a(); //=> 2
```

クロージャ

クロージャとは、外側のスコープ内の変数を参照する、内側の関数のこと。
次の例では、`increment()`内の無名関数がクロージャ。
クロージャにより、「状態を保持する関数を定義する」ことができる。

```js
function increment() {
  var x = 0;
  return function() {
    return ++x;
  };
};
f = increment();
f(); //=> 1
f(); //=> 2
f(); //=> 3
```

ゲッター/セッター

クロージャにより、変数`myName`を関数内部に保持しつつ、取得・書き換えを行なうことができる。

```js
var getName;
var setName;
(function() {
  var myName;
  getName = function() {
    return myName;
  };
  setName = function(name) {
    myName = name;
  };
})()
getName();       //=> undefined
setName('taro');
getName();       //=> taro
```

イテレータ

クロージャにより、イテレータを定義できる。

```js
function setup(x) {
  var i = 0;
  return function() {
    return x[i++];
  }
}
var f = setup(['a', 'b', 'c']);
f(); //=> a
f(); //=> b
f(); //=> c
```

オブジェクト

基本的にドット記法でアクセスする。
動的にアクセスする場合や、キーにクォートが必要な場合のみ`[]`でアクセスする。

```js
var object = {
  a: 1,
  b: function() {
    return 2;
  }
}
object.a    //=> 1
object['a'] //=> 1
object.b()  //=> 2
typeof(object) //=> object
```

以下は同じ意味。

```js
var o = {};
var o = new Object();
```

thisによるアクセス

```js
var human = {
  name: 'taro',
  say: function() {
    return this.name;
  }
}
human.say(); //=> taro
```

コンストラクタ関数

```js
function Hero(name) {
  this.name = name;
  this.attack = function() {
    return 'attacked';
  };
};
var hero = new Hero('taro');
hero.name;     //=> taro
hero.attack(); //=> attacked
```

instanceof演算子

```js
hero instanceof Hero //=> true
```

別のオブジェクトを返す関数

関数の返り値として別のオブジェクトを定義した場合、関数自身のオブジェクトは返らない。

```js
function Hero(name) {
  this.name = name;
  return {
    attack: function() {
      return 'attacked';
    }
  }
};
var hero = new Hero('taro');
hero.name;     //=> undefined
hero.attack(); //=> attacked
```

組み込みオブジェクト

- データラッパーオブジェクト
  - Object
  - Array
  - Function
  - Boolean
  - Number
  - String
- ユーティリティオブジェクト
  - Math
  - Date
  - RegExp
- エラーオブジェクト
  - Error

[ToDo] 組み込みオブジェクトの使い方をまとめる（メンバーを含む）

Boolean

`new`を使わず関数のように使うと、`!!`と同じ結果が得られる。

```js
Boolean('foo');      //=> true
Boolean('undefined') //=> false
```

Number

`new`を使わず関数のように使うと、`parseInt()`や`parseFloat()`と同じ結果が得られる。

```js
Number('12.12'); //=> 12.12
```

プロトタイプ

関数を定義すると、同時に`prototype`プロパティが生成される。
これはコンストラクタとして利用した場合のみ使われ、元の関数`Foo()`自身にはなにも影響を与えない。

```js
function Foo() {
  this.say = function() {
    return this.name;
  }
};

Foo.prototype = {
  name: 'foo'
}

foo = new Foo();
foo.say(); //=> foo
```

組み込みオブジェクトの拡張

```js
String.prototype.reverse = function() {
  return Array.prototype.reverse.apply(this.split('')).join('');
}

'taro'.reverse(); //=> orat
```

継承

```js
function Shape() {};

Shape.prototype = {
  name: 'Shape',
  toString: function() {
    return this.name;
  }
};

function Triangle(side, height) {
  this.side = side;
  this.height = height;
};

// 継承
Triangle.prototype = Shape.prototype;
Triangle.prototype.constructor = Triangle;

// 拡張
Triangle.prototype.name = 'Triangle';
Triangle.prototype.getArea = function() {
  return this.side * this.height / 2;
};

var triangle = new Triangle(5, 10);

triangle.toString(); //=> Triangle
triangle.getArea;    //=> 25
```

上記の方法では、`Triangle.prototype`への変更が`Shape.prototype`にも反映されてしまう。
つまり、`Shape`を継承する他のオブジェクトがある場合、意図しない動作をしてしまうおそれがある。
これを防ぐには、以下のような`extend()`関数を定義する。

```js
function extend(Child, Parent) {
  var F = function() {};
  F.prototype = Parent.prototype;
  Child.prototype = new F();
  Child.prototype.constructor = Child;
  Child.uber = Parent.prototype;
};

// 継承
// Triangle.prototype = Shape.prototype;
// Triangle.prototype.constructor = Triangle;
extend(Triangle, Shape);
```

継承は以下の方法でもできるが、これは継承のためだけに新しいオブジェクトを生成してしまう。
また、プロトタイプだけでなく`Shape()`自体も継承してしまう。

```js
Triangle.prototype = new Shape();
```

ブラウザ環境

ページ内でのオブジェクトモデルには以下の2つがある：

- BOM: Browser Object Model
  - ブラウザとPCの画面にアクセスするためのオブジェクト群
  - `window`オブジェクト
- DOM: Document Object Model
  - ドキュメントをノードのツリーとして表す方法
  - `window.document`によりアクセスする

代表的なプロパティ

- BOM
  - `window.navigator`
  - `window.location`
  - `window.history`
  - `window.screen`
  - `window.alert()`/`window.prompt()`/`window.confirm()`
  - `window.setTimeout()`/`window.setInterval()`
  - `window.document`
- DOM
  - `document.cookie`
  - `document.title`
  - `document.referrer`
  - `document.domain`

- `addEventListener()`
  - イベントを定義する
  - jQueryでいうところの`on()`
- `preventDefault()`
  - 標準の挙動を止める

```js
var links = document.getElementsByTagName('a');

for (var i; i < links.length; i++) {
  links[i].addEventListener('click', function(e) {
    if (!confirm('Are you sure?')) {
      e.preventDefault();
    }
  });
}
```

イベントの種類

- マウス
  - `mouseup`/`mousedown`/`click`/`mouseover`/`mouseout`/`mousemove`
- キーボード
  - `keydown`/`keypress`/`keyup`
- ローディング/ウィンドウ
  - `load`/`unload`/`beforeunload`/`abort`/`resize`/`scroll`/`contextmenu`
- フォーム
  - `focus`/`blur`/`change`/`select`/`reset`/`submit`
