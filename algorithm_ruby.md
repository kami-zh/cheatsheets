# Rubyによるアルゴリズム

汎用的な考え方を身につけるため、いわゆるRuby的な記法は用いない（例えば`a, b = b, a`など）。

## ソート

### バブルソート

すべての要素に関して、隣接する要素と比較し順序が逆であれば入れ替える。
これを要素数-1回繰り返す。

```ruby
def bubble_sort(a)
  size = a.size

  (size - 1).times do
    i = 0
    while i < (size - 1)
      if a[i] > a[i + 1]
        tmp = a[i]
        a[i] = a[i + 1]
        a[i + 1] = tmp
      end

      i += 1
    end
  end

  a
end

a = [5, 3, 7, 2, 8, 1, 9, 4, 6]

p bubble_sort(a) #=> [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
