# JavaScript

## 基本

### 構文

#### for

繰り返しの処理を行なう。
初期化、条件式、インクリメントの3つからなる。

```js
var sum = 0;

for (var i = 0; i < 10; i++) {
  sum += i;
}

sum; //=> 45
```

#### for-in

オブジェクトのプロパティに対して反復処理を行なう。

```js
var a = { a: 1, b: 2, c: 3 };

for (key in a) {
  a[key]; //=> 1 2 3
}
```

#### while

条件文の評価が`true`の間、コードブロックが実行され続ける。

```js
var i = 1;

while (i < 10) {
  i++;
}

i; //=> 10
```

#### switch

式を評価し、その式の値が`case`のラベルと一致する場合、それに関連づけられた文を実行する。

- 各`case`に`break`をつける
- オプションで`default`節をつけることができる

```js
var a = 1,
    b;

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

b; //=> foo
```

#### function

関数を宣言する。

- 明示的に`return`を書かなければ`undefined`が返る。
- 引数の数が合わない場合：
  - 足りなければ、残りの引数は`undefined`がセットされる
  - 多ければ無視される

```js
function sum(a, b) {
  return a + b;
}

sum(1, 2); //=> 3
```

##### arguments変数

関数内では、引数が自動的に変数`arguments`にセットされる。

```js
function sum() {
  var sum = 0;

  for (key in arguments) {
    sum += arguments[key];
  }

  return sum;
}

sum(1, 2, 3); //=> 6
```

### その他の基本

#### falseガード

変数が未定義または`false`の場合に値を代入する。

```js
var a = a || 1;

a; //=> 1
```

#### 三項演算子

条件式に基づいて2つの値のうち1つを選択する。

```js
var a = true ? 1 : 2;

a; //=> 1
```

## プリミティブデータ型

JavaScriptには、以下のデータ型がある：

| データ型 | 説明 |
| --- | --- |
| Number | 数値。整数と浮動小数点を含む |
| String | 文字列 |
| Boolean | `true`と`false` |
| undefined | 存在していない変数。または初期化していない変数にアクセスした場合に得られるもの |
| null | なにもない、を表現するもの |

以上に属さない値はオブジェクトとなる（ただし、`null`は「なにもない」を表すオブジェクトである）。

### 型を判別する

データの型は`typeof`演算子により判別する。

```js
typeof(null); //=> object
```

### 等価比較、等価比較および型比較

`==`演算子は、比較前に同じ型に変換される。
変換を意図しない場合は`===`を用いる。

```js
var a = 1,
    b = '1';

a == b;  //=> true
a === b; //=> false
```

## Number

### Number()

`new`を使わず関数のように使うと、`parseInt()`や`parseFloat()`と同じ結果が得られる。

```js
Number('12.12'); //=> 12.12
```

### インクリメント/デクリメント

インクリメント/デクリメントには後置、前置の2種類がある：

```js
// 後置
var a = 1;
var b = a++;
var c = b--;
b; //=> 1
c; //=> 2

// 前置
var a = 1;
var b = ++a;
var c = --b;
b; //=> 2
c; //=> 1
```

## Boolean

### Boolean()

`new`を使わず関数のように使うと、Boolean型に変換できる。

```js
Boolean(true); //=> true
Boolean(0);    //=> false
Boolean(NaN);  //=> false
```

### 二重否定

`Boolean()`の別の書き方として、`!!`を用いる方法がある。

```js
!!true; //=> true
```

## Array

### 定義・追加・削除

```js
var a = [1, 2, 3];
// または var a = new Array(1, 2, 3);

a[4] = 5;
a;    //=> [1, 2, 3, undefined, 5]
a[3]; //=> undefined

delete(a[1]);
a; //=> [1, undefined, 3, undefined, 5]
```

## Function

### データとしての関数

以下の2通りの定義方法はまったく同じ結果を得る。

```js
function sum(a, b) {
  return a + b;
}

var sum = function(a, b) { return a + b; }

sum(1, 2); //=> 3
```

### 無名関数

無名関数とは、名前づけされずに定義された関数のこと。

#### コールバック関数

コールバック関数とは、引数として渡す関数のこと。
以下のメリットがある：

- グローバル変数を減らすことができる
- 関数呼び出しの責任を委譲できる

```js
function sum(a, b, callback) {
  return callback(a + b);
}

sum(1, 2, function(c) { return c + 1 }); //=> 4
```

#### 自己実行可能関数

自己実行可能関数とは、定義と呼び出しを同時に行なう関数のこと。
一度だけ実行される処理（初期化など）に適している。

```js
(function(name) {
  return name;
})('taro'); //=> taro
```

#### プライベート関数

グローバルの名前空間を汚染しないために、プライベート関数を定義することができる。
以下の例では、トップレベルから`b()`は見えない。

```js
function a(x) {
  function b(y) {
    return Math.pow(y, 2);
  }

  return b(x);
}

a(2); //=> 4
```

#### 関数を返す関数

```js
function a(x) {
  return function(y) {
    return x + y;
  }
}

a(1)(2); //=> 3
```

#### 自分自身を書き換える関数

一度しか実行させたくない処理などに適している。

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

### スコープ

スコープとは、変数や関数にアクセスできる範囲のこと。

- `var`で定義すると、それより下位のブロックからアクセスできる
- `var`を省略して定義すると、グローバルスコープとして作成される

```js
var a = 1;

function foo() {
  var b = 2;
  c = 3;
  return a;
}

foo(); //=> 1
b;     //=> ReferenceError: b is not defined
c;     //=> 3
```

関数の中でネストされた関数を定義すると、ネストされた関数は親のスコープの変数にもアクセスできる（スコープチェーン）。

#### レキシカルスコープ

レキシカルスコープとは、関数の定義時にスコープがつくられる性質のこと。

```js
function a() {
  var c = 1;
  return b();
}

function b() {
  return c;
}

a(); //=> ReferenceError: c is not defined

var c = 2;

a(); //=> 2
```

### クロージャ

クロージャとは、外側のスコープ内の変数を参照する、内側の関数のこと。
クロージャにより、「状態を保持する関数を定義する」ことができる。

次の例では、`increment()`内の無名関数がクロージャとなる。

```js
function increment() {
  var x = 0;

  return function() {
    return ++x;
  }
}

var f = increment();

f(); //=> 1
f(); //=> 2
f(); //=> 3
```

#### ゲッター・セッター

クロージャにより、変数を関数内部に保持しつつ、取得・書き換えを行なうことができる。

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
  }
})();

getName();       //=> undefined
setName('taro');
getName();       //=> taro
```

#### イテレータ

クロージャにより、イテレータを定義できる。

```js
function setup(x) {
  var i = 0;

  return function() {
    return x[i++];
  };
}

var f = setup([1, 2, 3]);

f(); //=> 1
f(); //=> 2
f(); //=> 3
```

## オブジェクト

オブジェクトとは、あるものを表現するために、いくつかのプロパティやメソッドを持ったもの。

オブジェクトの属性には基本的にドット記法でアクセスする。
動的にアクセスする場合や、キーにクォートが必要な場合のみ`[]`でアクセスする。

```js
var object = {
  a: 1,
  b: function() {
    return this.a;
  }
}

object.a;    //=> 1
object['a']; //=> 1
object.b();  //=> 1
```

### コンストラクタ関数

コンストラクタ関数によりオブジェクトを定義すると、`new`によりそのインスタンスを生成できる。

```js
function Hero(name) {
  this.name = name;

  this.attack = function() {
    return 'attacked';
  }
}

var hero = new Hero('taro');

hero.name;     //=> taro
hero.attack(); //=> attacked
```

### 別のオブジェクトを返す関数

```js
function Hero(name) {
  this.name = name;

  return {
    attack: function() {
      return 'attacked';
    }
  }
}

var hero = new Hero('taro');

hero.name;     //=> undefined
hero.attack(); //=> attacked
```

---

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

組み込み関数

| 関数 | 説明 |
| --- | --- |
| parseInt() | 数値表現を返す |
| parseFloat() | 浮動小数点の表現を返す |
| isNaN() | 数値でない場合に`true`を返す |
| encodeURI() | URLエンコードする |
| decodeURI() | `encodeURI()`の逆の処理を行なう |
| eval() | 文字列をコードとして実行する |

Objectコンストラクタのメンバー

| メンバー | 説明 |
| --- | --- |
| Object.prototype | すべてのオブジェクトのプロトタイプ |

Objectオブジェクトのメンバー

| メンバー | 説明 |
| --- | --- |
| constructor | Objectコンストラクタ関数への参照 |
| toString() | 文字列表現を返す |
| hasOwnProperty() | そのオブジェクト自身のプロパティであれば`true`を返す |
| isPrototypeOf() | プロトタイプとして使用されている場合に`true`を返す |

Arrayオブジェクトのメンバー

| メンバー | 説明 |
| --- | --- |
| length | 配列の要素数を返す |
| concat() | 複数の配列をマージする |
| join() | 配列を文字列に変換する。引数はセパレータで、デフォルトはカンマ |
| shift() | 配列の最初の要素を削除し、それを返す |
| pop() | 配列の最後の要素を削除し、それを返す |
| unshift() | 要素を配列の先頭に追加し、追加後の配列の長さを返す |
| push() | 要素を配列の末尾に追加し、追加後の配列の長さを返す |
| reverse() | 配列を逆順に並べ替える |
| slice() | 配列の一部の要素を抜き出して返す |
| sort() | 配列をソートする |

Functionオブジェクトのメンバー

| メンバー | 説明 |
| --- | --- |
| apply() | 関数の`this`を書き換えた上で呼び出す |
| call() | 引数を配列ではなく1つずつ受け取る以外は`apply()`と同じ |

```js
function foo() {
  return this.toString();
};

var myObject = {};

foo.apply();         //=> [object Window]
foo.apply(myObject); //=> [object Object]
```

Numberコンストラクタのメンバー

| メンバー | 説明 |
| --- | --- |
| Number.NaN | 数値ではないことを表すオブジェクト |

Stringオブジェクトのメンバー

| メンバー | 説明 |
| --- | --- |
| length | 文字列の文字数を返す |
| charAt() | 指定された位置の文字を返す |
| concat() | 入力された文字列をつなげた新しい文字列を返す |
| indexOf() | 文字列の一部とマッチした場合、その位置を返す |
| match() | マッチした要素の配列を返す |
| replace() | マッチした文字列を他の文字列に置き換える |
| search() | 最初にマッチした位置を返す |
| slice() | 指定された部分文字列を返す |
| split() | 文字列を配列にする |
| toLowerCase() | 文字を小文字に変換する |
| toUpperCase() | 文字を大文字に変換する |

Dateコンストラクタのメンバー

| メンバー | 説明 |
| --- | --- |
| Date.parse() | 日付の値を返す |

```js
Date.parse('May 4, 2008') //=> 1209826800000
```

Dateオブジェクトのメンバー

| メンバー | 説明 |
| --- | --- |
| getFullYear() | 西暦の年を取得する |
| setFullYear() | 西暦の年を設定する |
| getMonth() | 月を取得する |
| setMonth() | 月を設定する |
| getDate() | 日を取得する |
| setDate() | 日を設定する |

その他にも、時間、分、秒、ミリ秒、曜日などを取得・設定できる。

Mathオブジェクトのメンバー

| メンバー | 説明 |
| --- | --- |
| Math.round() | 最も近い整数を返す |
| Math.floor() | 切り捨てを行ない整数を返す |
| Math.ceil() | 切り上げを行ない整数を返す |
| Math.max() | 最も大きい数値を返す |
| Math.min() | 最も小さい数値を返す |
| Math.random() | 0から1の間のランダムな数値を返す |

エラー処理

エラーが表示される=予期していないエラーが発生した、ということ。
予期しているエラーは`try`/`catch`で捕捉する。

```js
try {
  iDontExist();
} catch (e) {
}
```

Errorオブジェクトの種類

- Error
- EvalError
- RangeError
- ReferenceError
- SyntaxError
- TypeError
- URIError

正規表現

正規表現のプロパティには次の3つがある：

- `g`: global
  - マッチするものをすべて見つける
- `i`: ignoreCase
  - 大文字小文字を無視する
- `m`: multiline
  - 行をまたいでマッチする

| パターン | 説明 |
| --- | --- |
| [abc] | 文字クラス |
| [a-z] | 範囲で指定された文字クラス |
| [^abc] | 文字クラスに含まれない、すべての文字にマッチする |
| a&#124;b | aかbにマッチする |
| a(?=b) | aの条件に合い、後ろにbが続く文字列にマッチする |
| a(?!b) | aの条件に合い、後ろにbが続かない文字列にマッチする |
| \s | 半角スペース、またはいくつかのエスケープ文字（`\n`など）にマッチする |
| \w | すべてのアルファベット、数字、アンダースコアにマッチする |
| \d | 数値にマッチする |
| ^ | 文字列の先頭にマッチする |
| $ | 文字列の末尾にマッチする |
| . | 改行以外のすべての文字にマッチする |
| * | この記号の前のパターンが0個以上続く文字列にマッチする |
| ? | この記号の前のパターンが0個もしくは1つある場合にマッチする |
| + | この記号の前のパターンが1つ以上続く文字列にマッチする |
| {n} | この記号の前のパターンがn回続く文字列にマッチする |

```js
var string = 'Hello, World!';

string.match(/[elo]/g);            //=> ["e", "l", "l", "o", "o", "l"]
string.match(/[A-Z]/g);            //=> ["H", "W"]
string.match(/[^a-z]/g);           //=> ["H", ",", " ", "W", "!"]
string.match(/H|W/g);              //=> ["H", "W"]
string.match(/H(?=ello)/g);        //=> ["H"]
string.match(/H(?!orld)/g);        //=> ["H"]
string.match(/\s/g);               //=> [" "]
string.match(/\w/g);               //=> ["H", "e", "l", "l", "o", "W", "o", "r", "l", "d"]
string.match(/\d/g);               //=> null
string.match(/^Hello/g);           //=> ["Hello"]
string.match(/World!$/g);          //=> ["World!"]
string.match(/./g);                //=> ["H", "e", "l", "l", "o", ",", " ", "W", "o", "r", "l", "d", "!"]
string.match(/e.*d/g);             //=> ["ello, World"]
string.match(/H?ello, A?World!/g); //=> ["Hello, World!"]
string.match(/l+/g);               //=> ["ll", "l"]
string.match(/l{2}/g);             //=> ["ll"]
```
