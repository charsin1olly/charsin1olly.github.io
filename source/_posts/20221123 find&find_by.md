---
title: 20221123
date: 2022-11-23 12:08:33
tags: [學習筆記,Ruby on Rails]
---
# find 與 find_by 是差在哪裡啦！
在rails裡撈資料一下用find、一下用find_by，該用哪個才好呢？
先來比較一下它們兩個的不同吧！


現在我們建立了一個WishList的Model，建立1個wishlist項目，在rails console裡是這樣的
![](https://i.imgur.com/Y0Wiqqe.png)
現在看看全部的WishList，現在id編號只有排到7
![](https://i.imgur.com/aLVDOHN.png)



---

其實就是...嚴格程度不同
現在我們來尋找id編號為999的實體資料，

### 用find尋找實體
用find尋找```@wish_list=WishList.find(params[:id])```，會直接顯示**ActiveRecord::RecordNotFound**
![](https://i.imgur.com/LHgkuhg.png)
換成大家熟悉的畫面是這樣
![](https://i.imgur.com/SO2gcdF.png)


### 用find_by尋找實體
如果是換成用find_by```@wish_list=WishList.find_by(id: params[:id])```，則會顯示這是**nil**
![](https://i.imgur.com/rE8lbc5.png)
換成網頁版
![](https://i.imgur.com/2M9u4sS.png)

其實find_by有一個兄弟，叫做```find_by!```它擁有find_by的外表以及find的功能，找不到這筆資料的時候會直接顯示**ActiveRecord::RecordNotFound**
![](https://i.imgur.com/rQW14pK.png)



### 該用find還是find_by?
如果我們不需要**顯示畫面**到那筆不存在的資料，那就使用find（例如：這個id所屬的這個頁面不存在，直接讓rails報錯再直接轉去404頁面顯示這個頁面不存在）；如果需要**比對**這筆資料存不存在，會需要利用這個空集合作計算或判斷的話，就使用find_by(例如：會員登入所輸入的帳號是否註冊過？如果他是一個nill就可以被塞到實體變數而不是報錯)

結論就是：選擇find或find_by就是取決於自己要獲得的結果是錯誤訊息還是一個nil值。
