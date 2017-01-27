# 請解釋對字串使用 += 和使用 concat 方法有何差異

對字串使用 += 方法，例如 a += b。事實上是再產生了一個 a 物件並把 a+b 的結果丟進新的 a 物件。我們可以觀察 object_id 來得知這樣的行為。

```ruby
irb(main):041:0> x = "hello"
=> "hello"
irb(main):042:0> x.object_id
=> 70232477009280
irb(main):043:0> x += " world"
=> "hello world"
irb(main):044:0> x
=> "hello world"
irb(main):045:0> x.object_id
=> 70232475548960
```

而 concat 則是對同一個物件進行操作

```ruby
irb(main):049:0> x = "hello"
=> "hello"
irb(main):050:0> x.object_id
=> 70232488144300
irb(main):051:0> x.concat " world"
=> "hello world"
irb(main):052:0> x
=> "hello world"
irb(main):053:0> x.object_id
=> 70232488144300
```