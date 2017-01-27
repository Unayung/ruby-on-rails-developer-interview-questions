# redirect_to 和 render 有什麼不同

redirect_to 可以視為跳轉到別頁。包括跳轉到別的網站也是用 redirect_to 。因此使用 redirect_to 會造成 URL 的改變。

render 則是用於告訴 Rails "我要顯示什麼樣的畫面 / 資料在 browser 上" 而事實上 Rails 本身在每一個 controller action 都自動進行尋找並 render 對應的 template。所以 render 不會造成 URL 的改變。

額外一提的是 render 會把之前在 form 裡填寫的內容一併顯示。對於註冊流程或是使用者體驗上是相當方便的。

以實際例子來看

```ruby
def create
  @user=User.new(params[:user])
  if @user.save
     redirect_to :index
  else
     render :new  #you should render to fill fields after error message
  end
end

如果 @user.save 成功了，就跳轉到 index action。
如果 @user.save 失敗了，就 render "new" 這個 action 的 template
( 也就是 create 的上一步，此時可注意 URL 還是會在 create 的 path )
```