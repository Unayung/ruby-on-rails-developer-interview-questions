# 如何指定 /beer/(beer_type) 這種 route

假定我們有以下幾種 beer type
```
IPA
brown_ale
pilsner
lager
lambic
hefeweizen
```
如何用同一個 controller action 和設定 routes 來達成 /beer/(beer_type) 顯示不同啤酒的資訊，而不在清單內的則顯示 404

```ruby
kinds = %w|IPA brown_ale pilsner lager lambic hefweizen|
resources :beer, only: [:show], constraints: {id: Regexp.new(kinds.join('|'))}

rails routes

Prefix Verb URI Pattern         Controller#Action
  beer GET  /beer/:id(.:format) beer#show {:id=>/IPA|brown_ale|pilsner|lager|lambic|hefweizen/}
```
