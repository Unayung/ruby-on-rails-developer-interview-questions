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



