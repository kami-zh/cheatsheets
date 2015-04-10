# Rubyによるアルゴリズム

汎用的な考え方を身につけるため、いわゆるRuby的な記法は用いない（例えば`a, b = b, a`など）。

ソートの対象となる配列は、以下のような`random_array()`にて生成する。

```ruby
def random_array(n, max = 100)
  array = []
  n.times do |i|
    array[i] = rand(max + 1)
  end

  array
end

a = random_array(100) #=> [89, 75, 85, 3, 91, 19, 61, 0, 65, 1, 97, 44, 45, 69, 91, 73, 61, 6, 27, 76, 52, 57, ...]
```

## ソート

### バブルソート

すべての要素に関して、隣接する要素と比較し順序が逆であれば入れ替える。
これを要素数-1回繰り返す。

```ruby
def bubble_sort(a)
  n = a.size - 1

  n.times do
    for i in 0..(n - 1)
      if a[i] > a[i + 1]
        tmp = a[i]
        a[i] = a[i + 1]
        a[i + 1] = tmp
      end
    end
  end

  a
end
```

### 選択ソート

要素の中でもっとも小さな値を探し、これをi番目の要素と入れ替える。
これを要素数回繰り返す。

```ruby
def selection_sort(a)
  n = a.length - 1

  for i in 0..n
    min = a[i]
    k = i
    for j in i..n
      if a[j] < min
        min = a[j]
        k = j
      end
    end

    a[k] = a[i]
    a[i] = min
  end

  a
end
```
