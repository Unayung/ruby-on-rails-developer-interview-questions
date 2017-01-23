# Polymorphic Association 多型關聯

使用場景例如，你的網站上有圖片 (Image) 和影片 (Video) 兩種 model，而 PM 告訴你，他想要讓這兩種 model 都可以留言 (Comment)

如果不使用 Polymorphic 的話，那你可能會產生 ImageComment 和 VideoComment 兩種 model 。而這兩者的行為又完全相同，這就違反了 DRY 的原則。

我們可以使用 Polymorphic Association 來解決這樣的需求

```ruby
rails g model comment content:text commentable_id:integer commentable_type

會產生這樣的 migration 檔案

class CreateComments < ActiveRecord::Migration
  def change
    create_table :comments do |t|
      t.text :content
      t.integer :commentable_id
      t.string :commentable_type

      t.timestamps
    end
  end
end

或是可以寫成這樣

class CreateComments < ActiveRecord::Migration
  def change
    create_table :comments do |t|
      t.text :content
      t.belongs_to :commentable, :polymorphic => true

      t.timestamps
    end
  end
end

中間 t.belongs_to :commentable, :polymorphic => true
則會自動產生 commentable_id 和 commentable_type 這兩個欄位
```

而在 Model 的部份，只要這樣設定即可

```ruby
class Comment < ActiveRecord::Base
  belongs_to :commentable, :polymorphic => true
end

class Video < ActiveRecord::Base
  has_many :comments, :as => :commentable
end

class Image < ActiveRecord::Base
  has_many :comments, :as => :commentable
end
```

這樣一來就算之後還有第三、四、N 種 Model 可以被 Comment。也只要加入上述的 relation 就可以搞定了。