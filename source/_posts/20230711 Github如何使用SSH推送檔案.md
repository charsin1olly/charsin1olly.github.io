---
title: Github如何使用SSH推送檔案
date: 2023-07-11 02:09:28
tags: [git]
---
最近桌機換新，終於可以用比較大的螢幕寫Code了(灑花)，但當我要push到github的時候，一直跳出SSH是不合法的(大概這個意思，忘了截圖)，才突然想到之前上課的時候有設定用SSH的方式上傳檔案，翻出這個簡略的筆記檔，照做卻卡關!是時候把它完善一下了，步驟開始~

## 先產出電腦的SSH KEY
### 1. 在終端機輸入```ssh-keygen``` 建立新的ssh key
```
Generating public/private rsa key pair.
Enter file in which to save the key (C:\User\(使用者)/.ssh/id_rsa):
```
這邊會顯示等等ssh key存放的位置，如果有設定過的會顯示：
```
C:\Users\(使用者)/.ssh/id_rsa already exists.
Overwrite (y/n)?
```
這邊可以選擇要不要覆寫之前創建的ssh檔案，如果要覆寫就輸入y繼續創建流程，不要的話就輸入n。

### 2. 設定上傳密碼
```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
承上一步驟，輸入y之後會顯示Enter passphrase選項，這是用來設定上傳密碼的，如果想要每次上傳都輸入密碼的話可以設定，沒有要設定的話就直接Enter到下一步。下面的選項就是重複輸入密碼而已，不設定密碼的話一樣Enter進入下一步。

### 3. 成功產生檔案(可以備份到隨身碟帶著走）
成功產出ssh key檔案之後會出現以下訊息
```
Your identification has been saved in C:\Users\(使用者)/.ssh/id_rsa
Your public key has been saved in C:\Users\(使用者)/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:(一大串密鑰) xx@xxxxx
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|                 |
| .               |
|+   .   .        |
|                 |
|=                |
|                 |
|                 |
|                 |
+----[SHA256]-----+
```

## 上傳到Github囉~
### 1. 讀取SSH key
注意!!這很重要!!特別是Windows的朋友!!我卡在這裡!!如果前面操作都是用cmd在操作的朋友，
**這邊要換成PowerShell**、**這邊要換成PowerShell**、**這邊要換成PowerShell**，因為cat是Linux Bash，在cmd使用這個指令會一直不斷地跳```'cat' 不是內部或外部命令、可執行的程式或批次檔```。

cd到.ssh資料夾下可以下這個指令，```cat id_rsa.pub```把公鑰內容印出來；或是直接點出資料夾，把資料夾的路徑複製過來，也就是```cat "C:\Users\(使用者)\.ssh\id_rsa.pub"```這樣也能讀取，讀出來的資料格式像是下面這樣，把這一大串複製起來備用
```
ssh-rsa (一大串密鑰)= xxx@xxxxxx
```

### 2. Github帳戶設定
a. 帳戶設定中找到Settings
![](https://hackmd.io/_uploads/Sk0aEaYtn.png)

b. 找到SSH and GPG keys選項，點選New SSH key新增SSH key
![](https://hackmd.io/_uploads/rkflBatKn.png)

c. Title可以取一個方便辨識的名字就行了，Key欄位就貼上剛才我們cat出來複製的那一大串key，按下Add SSH key就完成新增
![](https://hackmd.io/_uploads/BkzbIaYth.png)

### 3. 終於，SSH可以用了
在Github新建一個repository(步驟不贅述啦)，這邊我們就可以使用SSH的方式上傳檔案了
![](https://hackmd.io/_uploads/Sk_A86FFn.png)

搬運一下Github的步驟說明，這裡我們remote的分支就是用SSH上傳啦~
```
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:charsin1olly/JSP-from-zero.git
git push -u origin main
```