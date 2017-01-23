# Model.find 和 Model.find_by

如果我們有一筆記錄例如
```ruby
Student id = '4' name = 'foobar'
```
如果我們把記錄砍了，那 Student.find(4) 和 Student.find_by(:id => 4) 會發生什麼事?

```ruby
Student.find(4).delete

Student.find(4)
ActiveRecord::RecordNotFound: Couldn't find Student with 'id'=4
# 會產生錯誤

Student.find_by(:id => 4)
nil
# 只會回傳 nil
```