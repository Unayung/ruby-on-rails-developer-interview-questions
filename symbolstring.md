# Symbol 和 String 的不同

Symbol 是 immutable 物件而 String 是 mutable 物件。而每次呼叫 Symbol 時可由觀察 object_id 得知，是同一個 object，反觀 string 則是不同一個物件。

適當使用 Symbol 可以避免 Server 端的記憶體問題，且在物件的比較上來說，使用 Symbol 比較快速。
```ruby
irb(main):026:0> :a
=> :a
irb(main):027:0> :a.object_id
=> 722588
irb(main):028:0> :a.object_id
=> 722588
irb(main):029:0> :a.object_id
=> 722588
irb(main):030:0> 'a'
=> "a"
irb(main):031:0> 'a'.object_id
=> 70321956133380
irb(main):032:0> 'a'.object_id
=> 70321987377060
irb(main):033:0> 'a'.object_id
=> 70321987372240
irb(main):041:0> 'a'.equal?('a')
=> false
irb(main):042:0> :a.equal?(:a)
=> true
```