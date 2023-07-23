---
title: 在JAVA Web的JSP檔案使用Bootstrap
date: 2023-07-20 20:15:49
tags: [JAVA, CSS, Eclipse]
---
發現公司系統的專案都是寫原生CSS，開發切版花了很多時間，不如來用一下之前學過的Bootstrap加速一下~
先貼上一段bootstrap的程式碼，還沒成功引入bootstrap的畫面
![](https://hackmd.io/_uploads/HkOPgNU9n.png)

預期會變成這樣，它是一個可以展開、摺疊的摺頁，這樣就需要引入bootstrap的CSS和JavaScript控制的這兩個部分
![](https://hackmd.io/_uploads/Byiix48ch.png)


## 最簡單粗暴的-線上導入
在head標籤中加入這串，這樣就能導入css部分的程式碼：
```htmlembedded
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">		
```

別忘了還有負責動態效果的JavaScript，
```htmlembedded
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
```

## 使用下載版本的Bootstrap
1. 先到[載點](https://getbootstrap.com/docs/5.0/getting-started/download/)下載CSS以及JS的檔案，這裡下載完會獲得一個壓縮檔
![](https://hackmd.io/_uploads/Sk8WxILc3.png)

2. 在專案的WebContent資料夾裡新建一個Bootstrap資料夾(或是其他名字也可以)，把剛才下載的壓縮檔裡的CSS、JS資料夾塞進去，像這樣(js資料夾的錯誤還沒搞清楚是怎麼一回事，但目前用起來沒什麼問題)
![](https://hackmd.io/_uploads/HJBEW8U93.png)

3. 和上一種方法相同，將這段程式碼貼在head標籤內，將路徑位置改成資料夾的位置就可以正常使用了
```htmlembedded
<link href="Bootstrap/css/bootstrap.min.css" rel="stylesheet" type="text/css"  >
<script src="Bootstrap/js/bootstrap.min.js"></script>
```



## 參考資料
[bootstrap-Download](https://getbootstrap.com/docs/5.0/getting-started/download/)
[How to Get Started with Bootstrap (UI) & Eclipse](https://vitalflux.com/get-started-bootstrap-ui-eclipse/)
[Add Bootstrap to JSP Page](https://www.javaguides.net/2020/01/add-bootstrap-to-jsp-page.html)