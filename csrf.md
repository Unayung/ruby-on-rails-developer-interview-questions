# CSRF 是什麼

CSRF - Cross-Site Request Forgery 是指攻擊者惡意在可插入程式片段的地方放入如

```html
<img src="/posts/delete_all">
```

的程式碼，等到擁有管理權限的人看到這張假圖時，送出這個 request 給 server 然後刪除所有 post

如何防範 CSRF 攻擊呢? 首先從 routes 的角度來設計。

> 所有讀取、查詢性質操作，都應該用 _GET_，而會修改或刪除到資料的，則要用 _POST_ 、 _PATCH/PUT_ 或 _DELETE_ 。這樣的設計，就可以防止上面的惡意程式碼了，因為在瀏覽器中必須用表單 _form_ 才能送出 _POST_ 請求。 from [Rails實戰聖經](https://ihower.tw/rails/security.html#sec1)

而從 Rails 架構本身的防範來說，我們可以使用 protect_from_forgery 這個 method 來阻擋攻擊

```ruby
class ApplicationController < ActionController::Base
  protect_from_forgery with: :exception
end
```
這個 method 會在所有表單自動插入一組 token 而在每次送 _POST_ 的時候去和 session 裡的 token 比對是否正確，如果不正確就阻止 _POST_ 動作的發生。而 Layout中也有一段 <%= csrf_meta_tags %> 是給 JavaScript 讀取 token 用的。

