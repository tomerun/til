# ブロックから抜ける方法

ブロック内で `next` を使うと、そのブロックを終了して、 `yield` を呼び出した位置に制御を戻す。

一方 `return`/`break` を使うと、ブロックを定義しているメソッドごとreturnすることになる。

参照 [Rubyリファレンスマニュアル：制御構造](https://docs.ruby-lang.org/ja/latest/doc/spec=2fcontrol.html)

`test.rb`
```ruby
def sub
	5.times do |i|
		puts i
		yield i
	end
end

def main
	sub() do |n|
		next if n >= 2
	end
end

def main2
	sub() do |n|
		break if n >= 2
	end
end

puts 'main'
main()
puts 'main2'
main2()
```

```
$ ruby test.rb
main
0
1
2
3
4
main2
0
1
2
```

