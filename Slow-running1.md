**Windows運行慢的解決方法(一)**

1、內存佔用異常高，一般是85%以上，然而用戶並沒有運行較為佔用內存的應用程序。

- 調出任務管理器（組合鍵Ctrl+Alt+Del），默認是在進程選項卡下，此時選中『顯示所有用戶進程』，就能看到svchost進程之一佔用近2G內存了（特別注意標示的內容）。

<img src="http://oltn18dzj.bkt.clouddn.com/image/jpg/sr/r1.jpg">

- 右鍵佔用內存最大的『svchost.exe』，點擊『轉到服務』。

<img src="http://oltn18dzj.bkt.clouddn.com/image/jpg/sr/r2.jpg">

- 這個頁面可以看到有幾個PID都是1056的進程，點擊右下角的『服務』（這是個飛機票，直接送你到系統服務頁面）。

<img src="http://oltn18dzj.bkt.clouddn.com/image/jpg/sr/r3.jpg">

- 找到下圖裡的服務右擊它點擊『屬性』，將其服務狀態置為【停止】然後將其啟動類型設置為『禁止』。請注意，這裡的問題是系統更新引起的。

<img src="http://oltn18dzj.bkt.clouddn.com/image/jpg/sr/r4.jpg">

`假如你的PC忽然將變得極其的緩慢且內存異常佔用高就可以用類似方法參考處理解決`
