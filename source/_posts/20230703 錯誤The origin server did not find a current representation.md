---
title: 百百種錯誤訊息之 The origin server did not find a current representation for the target resource or ....
date: 2023-07-03 19:54:08
tags: [JAVA, Eclipse, Tomcat]
---

太長了標題放不下，全部的錯誤訊息是這樣：

```
The origin server did not find a current representation for the target resource or is not willing to disclose that one exists.
```

這個訊息在我學習 servlet 拜訪網址的時候出現過，有以下幾種可能

<font color="red"> 1. web.xml 文件標籤錯字導致的文法錯誤</font>
<font color="red"> 2. 拜訪的網址有錯字</font>
<font color="red"> 3. 新增或是修改 servlet 網址之後沒有重開 tomcat(本次問題)</font>
<font color="red"> 4. 網址名稱不能和 servlet 的名字一樣(本次問題)</font>

基本上這個錯誤訊息都是各種錯字造成的，請大家要仔細檢查自己打的有沒有錯啊~另外，網址名稱不能和 Servlet 的名字一樣這一點不知道是不是巧合，當我的網址改成和 Servlet 名稱不同的網址就能順利拜訪，希望有知道原理的大大可以告訴我(跪

參考資料裡面還有幾個解決方式，但具體為甚麼會有關聯沒有說得很清楚，也許有朝一日我也會用到?

---

## 關於伺服器設定的部分

![](https://hackmd.io/_uploads/Bkx8YelK3.png)

第二篇參考文章中提到這個錯誤有可能會與伺服器設置有關，而參考文章第一篇的問題三中也有和伺服器設定有關的解決方法，我照著設置結果 tomcat 直接開不起來，顯示的錯誤訊息和路徑錯誤有關，重新新增伺服器之後發現一切正常，而我的電腦預設 Server Locations 選項是選`Use workspace metadata`，發現不一定要和文中說的一樣選擇`Use Tomcat installation`這個選項，但如果要對應問題六的畫面，就必定要選這個選項才會有自己的專案資料夾生成在 tomcat 的資料夾中(依照 Deploy path 位置生成，我這邊會佈署到`wtpwebapps`資料夾)，否則就會跑進`workspace`的`.metadata`資料夾，所以在 tomcat 找不到專案資料夾的話，可以去檢查 tomcat 伺服器設定，看看它究竟把專案佈署到哪裡去囉~

![](https://hackmd.io/_uploads/HJV5jexK2.png)

## 參考資料

[Web 开发：关于 Tomcat 出现 The origin server did not find a current representation for the target resourc...的问题](https://blog.csdn.net/DBC_121/article/details/79204340)

["404: The origin server did not find a current representation for the target resource or is not willing to disclose that one exists" with Tomcat](https://stackoverflow.com/questions/71680405/404-the-origin-server-did-not-find-a-current-representation-for-the-target-res)
