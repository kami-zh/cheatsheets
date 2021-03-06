# Rubyによるアルゴリズム

汎用的な考え方を身につけるため、いわゆるRuby的な記法は用いない（例えば`a, b = b, a`など）。

ソートの対象となる配列は、以下のような`random_array()`にて生成する。

```ruby
def random_array(n, max = 100)
  a = []
  n.times { |i| a[i] = rand(max + 1) }
  a
end

random_array(100) #=> [89, 75, 85, 3, 91, 19, 61, 0, 65, 1, 97, 44, 45, 69, 91, 73, 61, 6, 27, 76, 52, 57, ...]
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

### 挿入ソート

i番目とi+1番目の要素を比較し、順序が逆であれば入れ替える。
また、i+1番目だった要素を適切な位置まで入れ替え続ける（挿入する）。

```ruby
def insertion_sort(a)
  n = a.size - 1

  for i in 1..n
    if a[i] < a[i - 1]
      j = i
      x = a[j]
      while (j > 0) && (a[j - 1] > x)
        if a[j] < a[j - 1]
          tmp = a[j]
          a[j] = a[j - 1]
          a[j - 1] = tmp
        end

        j -= 1
      end
    end
  end

  a
end
```

### ヒープソート

まず二分ヒープを作成する（親要素が子要素より大きいか等しい二分木）。
作成したヒープに対して、ルートから要素を取り出し最後尾に追加していく。
これを要素数分繰り返す。

```ruby
def heap_sort(a)
  n = a.size - 1

  # Create heap
  a = heapize(a, n)

  # Sorting
  for i in 0..n
    tmp = a[0]
    a[0] = a[n - i]
    a[n - i] = tmp

    # Create heap directed at unsorted array
    a = heapize(a, n - 1 - i)
  end

  a
end

# Create heap
#
# @param [Array] a Array creating heap
# @param [Integer] n Size of creating heap
# @return [Array] Heapized array
def heapize(a, n)
  for i in 0..n
    j = i
    while j > 0
      jp = pi(j)

      if a[j] > a[jp]
        tmp = a[j]
        a[j] = a[jp]
        a[jp] = tmp
      end

      j = jp
    end
  end

  a
end

# Get parent node index from child node index
#
# @param [Integer] ci Index of child node
# @return [Integer] Index of parent node
def pi(ci)
  (ci % 2 == 0) ? (ci / 2 - 1) : ((ci - 1) / 2)
end
```
