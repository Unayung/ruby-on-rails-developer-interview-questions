# N+1 Query 的處理方向

Post 有很多 Comments 而有時我們會遇到這種情境

```ruby
def users_comments
  posts = Post.all
  comments = posts.map(&:comments).flatten
  @user_comments = comments.select do |comment|
    comment.author.username == params[:username]
  end
end
```
這邊在取出每一個 post 之後，又對每一個 post 去 query 關連的 comments。就造成所謂的 N+1 Query 效能問題

解決方法最直觀就是用
```ruby
posts = Post.includes(comments: [:author]).all
```
來取代原本的 posts = Post.all

可以使用 [bullet](https://github.com/flyerhzm/bullet) 來偵測 N+1 Query