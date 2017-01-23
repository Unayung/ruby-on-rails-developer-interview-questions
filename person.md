# 如何讓 Person model 可以指定另一個 person 為 parent

```ruby
irb(main):001:0> john = Person.create(name: "John")
irb(main):002:0> jim = Person.create(name: "Jim", parent: john)
irb(main):003:0> bob = Person.create(name: "Bob", parent: john)
irb(main):004:0> john.children.map(&:name)
=> ["Jim", "Bob"]
```
如何達成這樣的關連呢？首先我們要知道 association 的 target class 是可以另外指定的，而外鍵的欄位也是可以自己定義

```ruby
rails g migration add_parent_id_to_person
# 先增加一個整數欄位 parent_id 到 person table

class Person < ActiveRecord::Base
  belongs_to :parent, class: Person
  has_many :children, class: Person, foreign_key: :parent_id
end
```

這個問題還可以延伸下去，如果我想達成這樣的效果，需要怎麼實作呢？
```ruby
irb(main):001:0> sally = Person.create(name: "Sally")
irb(main):002:0> sue = Person.create(name: "Sue", parent: sally)
irb(main):003:0> kate = Person.create(name: "Kate", parent: sally)
irb(main):004:0> lisa = Person.create(name: "Lisa", parent: sue)
irb(main):005:0> robin = Person.create(name: "Robin", parent: kate)
irb(main):006:0> donna = Person.create(name: "Donna", parent: kate)
irb(main):007:0> sally.grandchildren.map(&:name)
=> ["Lisa", "Robin", "Donna"]
```

這邊考的是 has_many ... :through => 這個概念

```ruby
class Person < ActiveRecord::Base
  belongs_to :parent, class: Person
  has_many :children, class: Person, foreign_key: :parent_id
  has_many :grandchildren, class: Person, through: :children, source: :children
end
```

這個範例解釋得很好
```ruby
Say you have these models:

Car
Engine
Piston

A car has_one :engine
An engine belongs_to :car
An engine has_many :pistons
Piston belongs_to :engine

A car has_many :pistons, through: :engine
Piston has_one :car, through: :engine

Essentially you are delegating a model relationship to another
model, so instead of having to call car.engine.pistons, you can
just do car.pistons
```