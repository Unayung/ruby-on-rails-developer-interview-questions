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

# Mixin 中 include 和 Extend 的差別

```
基本
include module 會讓 module 內定義的 method 成為 instance method
extend module 會讓 module 內定義的 method 成為 class method

進階
當 Klazz.extend(Mod) 時, Klazz 會擁有 Mod 的 method, 視為 class method
當 obj.extend(Mod) 時, obj 會擁有 Mod 的 method, 視為 instance method, 並只有此 obj 可以呼叫.
其它同 class 生出來的 object 是不能呼叫的.
```

# instance\_eval 和 class\_eval 的差別

```
先講結論
instance_eval 可以定義 instance method 但不能被同 class 的其它 instance 呼叫,
也可以定義 class method 因為 class 也是 Class 的一個 instance

class_eval 可以定義 instance method 並且可以被同 class 的其它物件呼叫
是不是聽起來有點玄妙？
我們來看底下的例子
```

```ruby
class MyClass
  def initialize(num)
    @num = num
  end
end

a = MyClass.new(1)
b = MyClass.new(2)
```
當我們想要檢視 a,b 物件內的 num 值時，我們會用 a.num 來試試看
```ruby
a.num
=> NoMethodError: undefined method `num' for #<MyClass:0x007fba5c02c858 @num="1">
```
噴錯了，因為我們沒有 def num 這個 method
那我們用 instance_eval 來試試看吧
```ruby
a.instance_eval do
  def num
    puts @num
  end
end

a.num
=> 1
b.num
=> NoMethodError: undefined method `num' for #<MyClass:0x007fa721827e20 @num="2">
```
又噴錯了，因為我們只有針對 a 這個物件去寫 instance_eval, 但 b 是看不到 num 這個 method

那如果我們針對 MyClass 用 instance_eval 會發生什麼事呢?
```ruby
MyClass.instance_eval do
  def num
    @num
  end
end

b.num
=> NoMethodError: undefined method `num' for #<MyClass:0x007fa721827e20 @num="2">
```
又噴錯了，因為我們是對 MyClass 這個 Class 的 instance 去寫 instance_eval
上面的 code 執行起來是這樣
```ruby
MyClass.num
=> nil # 因為我們沒有給值丟進 num 裡就直接 call num 這個變數. 自然是 nil
```
那麼正確讓 a.num / b.num 都可以回傳正確值的作法是什麼呢?
```ruby
MyClass.class_eval do
  def num
    @num
  end
end

a.num
=> 1
b.num
=> 2
```
事實上我們可以把上面 class_eval 的例子視為平常在寫 instance method 的寫法，如下面所示
```ruby
class MyClass
  def num
    @num
  end
end
```



