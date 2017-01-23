# Hash 和 HashWithIndifferentAccess 的差別

Hash 在 Ruby 內部實作是用 == 來比對 key. 換句話說在 irb (或純 ruby)的情況下會發生這種情形
```ruby
irb(main):001:0> h = Hash.new
=> {}
irb(main):002:0> h[:v] = '123'
=> "123"
irb(main):003:0> h[:v]
=> "123"
irb(main):004:0> h['v']
=> nil
```
而在 ActiveSupport 的 HashWithIndifferentAccess 的幫忙之下，我們可以用 :symbol 或 'string' 來取得 Hash 裡的值
```ruby
irb(main):001:0> hh = HashWithIndifferentAccess.new
=> {}
irb(main):002:0> hh[:v] = '456'
=> "456"
irb(main):003:0> hh[:v]
=> "456"
irb(main):004:0> hh['v']
=> "456"
```