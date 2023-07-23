---
title: Thunderbird，關於資料備份匯入
date: 2023-07-21 21:48:31
tags: [工作筆記]
---
公司信箱用的是Thunderbird，遇到某些狀況需要重裝，同事的資料都需要備份(之前有一次忘記備份差點被追殺orz)，可是Thunderbird的資料夾功能可能因為本人覺得不是那麼好理解，來簡單說說怎麼備份~

相關的檔案在```C:\Users\(使用者名稱 )\AppData\Roaming\Thunderbird\Profiles\(亂數).default-release```這一層資料夾裡，而亂數名稱的資料夾則是一個亂數對應一個帳號，例如現在我有新增一個A信箱的帳號，就會產生一個像是lyh99o1n之類的亂數名稱資料夾，再新增一個B信箱的話，就會再產生另一個新的亂數名稱hqk49oc9資料夾，就可以得知關於這個帳號的資料都在這個資料夾裡，整個資料夾複製到找的到的地方，但我自己習慣整個Thunderbird資料夾都複製，以免有遺漏。

## 信件備份匯入
亂數資料夾點開之後會看到非常多的資料夾以及檔案，找到Mail資料夾，他是用來存放信件的。

打開重新安裝的Thunderbird同樣找到```C:\Users\(使用者名稱)\AppData\Roaming\Thunderbird\Profiles\```資料夾，就會看見多了一個新的亂數資料夾，點進去，把剛才複製的Mail資料夾貼上並且覆蓋即可。

小提醒:如果沒有要定期自動刪郵件，重裝之後也要自己在```帳號設定/伺服器設定```那邊勾選不刪除伺服器上的郵件，這樣可以避免下次要重裝結果有信件遺失的意外。

## 通訊錄匯入
亂碼資料夾下有三個檔案關於通訊錄資料，分別是
* 個人通訊錄：abook.mab
* 收集到的E-mail：history.mab
* 群組：impab.mab

原本我以為只要複製貼上到相對應位置就可以成功，結果怎麼試都沒用，突然想起剛才研究匯出檔案類型時路過的匯入檔案按鈕，巧了，mab檔案可以匯入:
![](https://hackmd.io/_uploads/r1XIfjv53.png)

這樣就選擇使用mab檔匯入資料，下一步選擇檔案，把剛才備份、也就是舊資料夾的```abook.mab```、```history.mab```、```impad.mab```這三個檔案依次匯入，通訊錄資料就可以回復囉~


## 參考資料
[Thunderbird通訊錄手動還原](http://dennisliao.blogspot.com/2012/09/thunderbird.html)