# 為什麼要有 Migration 檔案

Migration 檔案的用意在於，讓每一次資料庫修改都能夠被記錄進版本控制。以防止多人協作或開發 / 測試 / 正式環境資料庫 schema 的不一致。

而另一個較不為人知的優點是，Migration 背後針對不同類型的資料庫 ( 比方 MySQL vs PostgreSQL ) 可以進行相同的處理，減少開發者考慮在 A DB 和 B DB 進行資料庫操作的語法差異。