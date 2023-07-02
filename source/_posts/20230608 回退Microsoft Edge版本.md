---
title: 回退Microsoft Edge版本
date: 2023-06-08 20:02:56
tags: [Microsoft, Edge]
---
為了設定IE相容性，解決公司系統網站無法正常使用問題，發現IE開啟之後會自動變成Edge開啟(系統來還沒升級RRR)，找了很多文章都說要把```Microsoft Edge中以Internet Explorer開啟網站面板```改永不，但問題來了，我的Edge版本113.0.1774.57這個面板似乎不見了，前輩的110.0.1587.46版本是有的，我想說把版本降到一致再來設定，雖然說真正解決這個問題的辦法不是降版本，但是摸了好幾天不記錄太對不起自己了~

## 下載&安裝
### 最新版本的範本檔
到[Microsoft官網](https://www.microsoft.com/zh-tw/edge/business/download?form=MA13FJ)下載範本檔，安裝方式之前我有[文章](https://hackmd.io/@diXi7OUmRKqIgmAxMuHz9A/SyuZyGXrh)寫過，不過這次要把```msedgeupdate.admx```和```msedgeupdate.adml```都複製過去，不然會少一個Edge更新的資料夾選項，這是我卡了好幾天的原因QQ

## 方法1: 使用 MSI 手動啟用復原
這個方法可以直接停用更新，手動變更版本到下載的版本，也不用怕自動更新把把它升級回去。

1. 找到 ```電腦設定/系統管理範本/Microsoft Edge 更新/應用程式/Microsoft Edge```編輯原則設定:
     * [更新原則覆寫] 點兩下，改成```已啟用```，左下方輸入欄改成```停用更新```，描述:「指定 Microsoft Edge Update 如何從 Microsoft Edge 處理可用更新」

2. 安裝指定版本的edge
    a. 上面提到的官網連結，可以下載指定版本的edge，會獲得一個```MicrosoftEdgeEnterpriseX64.msi```檔案，別急著按，雖然按了也沒事，只會跳出一個訊息框告訴你:你的電腦已經有安裝更新的版本。

    b. 把這個檔案放到桌面或是其他找的到的地方，然後在開始工具列搜尋```cmd```，***用系統管理員身分執行***，這很重要，如果沒用系統管理員，後面的步驟可能會無法執行(對...我又被這個卡了好久)
    ![](https://hackmd.io/_uploads/ByGfF9ar3.png)

    c. 打開cmd之後先找到剛才放msi檔的地方，像我是放在桌面一個臨時的資料夾，先把現在位置切換到存放安裝檔的資料夾，例如:```cd C:\Users\Administrator\Desktop\123\edge```。
    如果不知道路徑的話，打開剛才存放msi的資料夾，複製資料夾上方的網址，在cmd輸入```cd (你剛才複製的網址)```是一樣的效果。
    ![](https://hackmd.io/_uploads/ByCnqqTSn.png)

    d. 在cmd輸入```msiexec /I MicrosoftEdgeEnterpriseX64.msi /qn ALLOWDOWNGRADE=1```按下enter，看起來沒反應，打開工作管理員會看到edgeUpdate就代表有在降版本了(如果沒看到相關程序可能就是沒開系統管理員)，這時候我直接關掉edge等更新。

    * 如果發現怎麼搞都沒反應，可以試試看系統管理員打開Windows PowerShell輸入cmd，再重複d步驟
    * 如果之前有關掉Edge Update要記得打開，不然會卡在Edge正在更新，請等幾分鐘。


    e. EdgeUpdate跑完之後重開Edge就會發現版本被降回去了(如果發現Edge Update消失，馬上重開也有可能是降版本前的版本，可以過幾分鐘再開開看)

## 方法2: 使用 Microsoft Edge Update 和管理範本啟用復原
這個方法是利用自動更新設定指定版本，再怎麼樣更新，也還是同一個版本。

1. 按下```Win+R```輸入```gpedit.msc```叫出管理範本設定。
2. 找到 ```電腦設定/系統管理範本/Microsoft Edge 更新/應用程式/Microsoft Edge```編輯原則設定:
     a. **[目標版本複寫]** 點兩下，改成```已啟用```左下方輸入欄輸入想要的指定版本(例如:110.0.1587.46)，簡單來說就是指定版本用的選項。
     
     b. **[復原至目標版本]** 點兩下，改成```已啟用```
     這個選項就可以讓update降回當前版本，但前提是「除非設定 '目標版本覆寫' **且**將 '更新原則覆寫' 設定為開啟狀態 (永遠允許更新、僅限無訊息自動更新、僅限手動更新)，否則此原則不會生效。」，和方法1的步驟衝突，要用的時候要留意~

    
## 我自己的設定
我採用方法1降版本，但是多設定方法2的目標版本複寫打開，預防哪天更新不小心被打開版本被升上去，而關閉更新跟公司的管理習慣比較一致，方法2比較傾向拿來恢復成最新版本。

## 參考資料
[【心得】分享Edge降版的方法](https://forum.gamer.com.tw/C.php?bsn=60030&snA=621392)
[如何將 Microsoft Edge 復原到舊版-Mircrosoft Learn](https://learn.microsoft.com/zh-tw/deployedge/edge-learnmore-rollback)
[Microsoft Edge版本回退方法](https://blog.csdn.net/weixin_41963310/article/details/113827270)