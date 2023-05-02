---
title: 如何跳過Microsoft Authenticator驗證程序
date: 2023-05-02 20:16:24
tags: [Microsoft, 工作筆記]
---
最近公司在幫同仁電腦裝Microsoft 365，總有一個煩躁的步驟:**Microsoft Authenticator驗證**。原本想說全部跳過應該沒關係，後來發現規定14天內要驗證，否則無法使用，硬著頭皮拿著同事手機跟著步驟照做，下載app、掃QRcode......好幾台電腦會發瘋吧......
於是，我開始尋找如何跳過這個步驟的方法:

## 方法一: 官方說法
Microsoft Authenticator驗證是Microsoft的雙步驟驗證的一環，在不信任的裝置使用app，但是不想留下手機信箱之類個人資訊的狀況下，也能對帳號進行保護的一種機制，也可以選擇不要囉(公司的電腦應該不會怎樣吧...?)~
這個方法也是最多搜尋結果跳出來的解方，雖然無法解決我想直接跳過的問題(剛開始點進去的時候已經全部都停用了)，還是記錄一下以備不時之需:
1. 先找到admin center，也就是系統管理
![](https://i.imgur.com/d5dz3LN.png)

2. 左側功能欄/使用者/作用中使用者
![](https://i.imgur.com/mXmy5Qi.png)

3. 點選畫面中的多重要素驗證

4. 勾選想要停用多重要素驗證的帳戶 / 停用
![](https://i.imgur.com/amw8DBF.png)

## 方法二(解決問題):
翻了好一段時間，這個辦法才有效解決我想跳過驗證程序的問題(太好了QQ)
1. 一樣在左側功能欄 / 找到 Azure Active Directory 點下去
![](https://i.imgur.com/NXsc3ns.png)

2. 概觀 / 屬性(也可以在搜尋打關鍵字「屬性」，找到租用戶屬性，這樣也會有一樣的操作介面)
![](https://i.imgur.com/kHcKcrH.png)

3. 拉到最下面 / 管理安全性預設值 / 停用
![](https://i.imgur.com/sZ3aRT0.png)

附上第一次不知道怎麼點出來、和參考文章介面一樣的這個面板(再操作一次的時候找不到...orz)
![](https://i.imgur.com/wYKFWiE.png)

4.完成以上步驟之後，打開Microsoft 365登入就不需要經過驗證囉~不過官方說明寫這樣比較容易被攻擊這個可能要多考慮一下。

## 參考

1. [開啟或關閉 Microsoft 帳戶的雙步驟驗證](https://support.microsoft.com/zh-tw/account-billing/%E9%96%8B%E5%95%9F%E6%88%96%E9%97%9C%E9%96%89-microsoft-%E5%B8%B3%E6%88%B6%E7%9A%84%E9%9B%99%E6%AD%A5%E9%A9%9F%E9%A9%97%E8%AD%89-b1a56fc2-caf3-a5a1-f7e3-4309e99987ca)
2. [Office365强制Microsoft Authenticator验证登录如何关闭](https://blog.csdn.net/robinooo/article/details/125058722)