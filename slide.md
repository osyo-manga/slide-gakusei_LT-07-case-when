### 第7回 学生エンジニア限定LT大会！！！

- - -

## Ruby の case-when で遊ぼう

---

## 自己紹介
- - -

* なまえ  : おしょー
* Twitter : [@pink_bangbi](https://twitter.com/pink_bangbi)
* github  : [osyo-manga](https://github.com/osyo-manga)
* ブログ  : [Secret Garden(Instrumental)](http://secret-garden.hatenablog.com)
* 言語	: C++ / Ruby / JavaScript（+ Vue.js + Electron）

---

## Ruby の case-when で遊ぼう

---

#### Ruby の case-when とは
- - -

```ruby
def func n
	case n
	when 1
		"one"
	when 2
		"two"
	when 3
		"three"
	else
		"other"
	end
end

p func 1 # => "one"
p func 2 # => "two"
p func 3 # => "three"
p func 4 # => "other"
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="2"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="3,5,7"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="4,6,8"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="9-10"></span>

---

#### case-when の特徴
- - -

```ruby
def func n
	# if 式で記述するとこんな感じ
	_tmp = n
	if 1 === _tmp
		"one"
	elsif 2 === _tmp
		"two"
	elsif 3 === _tmp
		"three"
	else
		"other"
	end
end
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="4,6,8"></span>

---

#### Ruby の === 演算子
- - -

| obj | `obj === other` |
|:-----------:|:------------|
| デフォルト | `==` と同じ |
| Range | `other`が範囲内に含まれているかどうか |
| Regexp | `other` と正規表現マッチを行う |
| Class | そのクラスのインスタンスであるかどうか |
| Proc | `other` を引数とした `obj.call` を呼び出す |

---

## いろいろと遊んでみよう

---

#### インスタンスが任意のクラスかどうか判定
- - -

```ruby
def twice x
    case x
    # x が各クラスのインスタンスだった場合
    when Integer
        x + x
    when String
        x.to_i + x.to_i
    when Symbol
        x.to_s.to_i + x.to_s.to_i
    else
        "???"
    end
end

p twice 42        # => 84
p twice "1234"    # => 2468
p twice :"5678"   # => 11356
p twice [1, 2, 3] # => "???"
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="4,15"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="6,16"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="8,17"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="10,18"></span>

---

#### 任意の範囲に該当するかどうか判定
- - -

```ruby
def level n
    case n
    # 1〜3の範囲にマッチする場合みたいに記述することが出来る
    when (1..3)
        "low"
    when (4..6)
        "middle"
    when (7..9)
        "high"
    else
        "other"
    end
end

p level 3   # => "low"
p level 5   # => "middle"
p level 9   # => high
p level 32  # => other
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="4,15"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="6,16"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="8,17"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="10,18"></span>

---

#### `Array#===` を定義してみる
- - -

```ruby
# Array#=== を定義
# 各要素を === で比較して全て true なら true
class Array do
	def === other
		size == other.size && zip(other).all? { |a, b| a.=== b }
	end
end

# 必ず true を返す proc を返す
def _
    proc { true }
end
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="4-6"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="10-12"></span>

>>>

```ruby
def fizzbuzz n
    case [n % 3, n % 5]
    # n % 3 === 0 && n % 5 === 0
    when [0, 0]
        "FizzBuzz"
    # n % 3 === 0
    when [0, _]
        "Fizz"
    # n % 5 === 0
    when [_, 0]
        "Buzz"
    else
        n
    end
end

p (1..20).map &method(:fizzbuzz)
# => [1, 2, "Fizz", 4, "Buzz", "Fizz", 7, 8, "Fizz", "Buzz", 11, "Fizz", 13, 14, "FizzBuzz", 16, 17, "Fizz", 19, "Buzz"]
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="2"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="4"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="7"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="10"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="13"></span>

---

## まとめ
- - -

* case-when は `===` 演算子で比較を行う
* `===` を再定義することで拡張する事が出来る
* Ruby たのしいのでみんなやろう


---

## ご清聴
## ありがとうございました
