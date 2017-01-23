# Proc 和 lambda 的差別

簡單來說 Proc 無視傳入的參數是否與 Proc 內定義的參數個數相同，而 lambda 在參數個數不同時會噴錯

```ruby
p = Proc.new{|x,y,z| x+y+z}
p.call(1,2,3)
=> 6
p.call(1,2,3,4)
=> 6 #第四個參數被無視了

l = lambda{|x,y,z| x+y+z}
l.call(1,2,3)
=> 6
l.call(1,2,3,4)
=> ArgumentError: wrong number of arguments (given 4, expected 3) #噴錯了
```



