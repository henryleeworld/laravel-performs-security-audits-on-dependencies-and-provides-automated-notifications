# Laravel 11 對依賴套件執行安全稽核並提供自動通知

引入 dgtlss 的 warden 套件來擴增對依賴套件執行安全稽核並提供自動通知，管理員就可以在偵測到使用已知安全漏洞的依賴套件時，收到電子郵件通知。

## 使用方式
- 把整個專案複製一份到你的電腦裡，這裡指的「內容」不是只有檔案，而是指所有整個專案的歷史紀錄、分支、標籤等內容都會複製一份下來。
```sh
$ git clone
```
- 將 __.env.example__ 檔案重新命名成 __.env__，如果應用程式金鑰沒有被設定的話，你的使用者 sessions 和其他加密的資料都是不安全的！
- 當你的專案中已經有 composer.lock，可以直接執行指令以讓 Composer 安裝 composer.lock 中指定的套件及版本。
```sh
$ composer install
```
- 產生 Laravel 要使用的一組 32 字元長度的隨機字串 APP_KEY 並存在 .env 內。
```sh
$ php artisan key:generate
```
- 執行 __Artisan__ 指令的 __warden:audit__ 來執行安全稽核。
```sh
$ php artisan warden:audit {--silent}
```

----

## 畫面截圖
![](https://i.imgur.com/jT8zjca.png)
> 執行安全稽核確認 Larvel 11 版本低於 11.31.0，則會顯示注入安全漏洞警告

![](https://i.imgur.com/pST3EL7.png)
> 設定的電子郵件會有注入安全漏洞通知

![](https://i.imgur.com/S6iDOmP.png)
> Larvel 11 版本更新到 11.31.0 以上，再執行安全稽核則顯示無安全漏洞警告
