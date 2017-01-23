# resource 和 resources 的差別

從字面上來看 resouce 是單數而 resources 是複數，也就是說如果你想要列出某種類 model 的列表. 你應該選用 resources 來符合 rails 的 convention. 而兩者預設產生出來的 routes 差別在於有沒有 index action 和對應的 path / url

```ruby
# 假設每個使用者只有一組 profile 可以設定

resource :profile # in routes.rb

rails routes

 new_profile GET    /profile/new(.:format)  profiles#new
edit_profile GET    /profile/edit(.:format) profiles#edit
     profile GET    /profile(.:format)      profiles#show
             PATCH  /profile(.:format)      profiles#update
             PUT    /profile(.:format)      profiles#update
             DELETE /profile(.:format)      profiles#destroy
             POST   /profile(.:format)      profiles#create
             
# 可以發現並沒有建立 index action 的 route
```
```ruby
# 假設每個使用者可以設定多組 profile

resources :profiles # in routes.rb

rails routes

    profiles GET    /profiles(.:format)          profiles#index
 new_profile GET    /profiles/new(.:format)      profiles#new
edit_profile GET    /profiles/:id/edit(.:format) profiles#edit
     profile GET    /profiles/:id(.:format)      profiles#show
             PATCH  /profiles/:id(.:format)      profiles#update
             PUT    /profiles/:id(.:format)      profiles#update
             DELETE /profiles/:id(.:format)      profiles#destroy
             POST   /profiles(.:format)          profiles#create
             
# 這個情況下就有 profiles 列表的存在，且針對某一 profile 的操作需要 pass id 以找到特定記錄
```