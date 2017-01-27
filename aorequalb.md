# 請解釋這個語法 a ||= b

當 a 有值 ( 非 nil 非 false ) 時， a 保持原值

當 a 為 nil / false 時， a = b

我們看以下的範例

```ruby
irb(main):024:0> a = nil
=> nil
irb(main):025:0> b = 10
=> 10
irb(main):026:0> a ||= b
=> 10
irb(main):027:0> a
=> 10

irb(main):028:0> a = false
=> false
irb(main):029:0> b = 20
=> 20
irb(main):030:0> a ||= b
=> 20
irb(main):031:0> a
=> 20

irb(main):032:0> a = ""
=> ""
irb(main):033:0> b = "abc"
=> "abc"
irb(main):034:0> a ||= b
=> ""
irb(main):035:0> a
=> ""

irb(main):037:0> a = 689
=> 689
irb(main):038:0> b = 633
=> 633
irb(main):039:0> a ||= b
=> 689
irb(main):040:0> a
=> 689
```