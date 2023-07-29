---
title: java 執行class時出現 java.lang.NoClassDefFoundError
date: 2023-07-29 17:11:04
tags: [JAVA]
---
一如往常想要補一下JAVA基本功，正常的```javac Page_31.java```編譯之後，再輸入```java Page_31```竟然出現了這個 ：
```
ＸＸＸ@charsin  ~/(...)/ch2/exercise java Page31
Error: Could not find or load main class Page31
Caused by: java.lang.NoClassDefFoundError: exercise/Page31 (wrong name: Page31)
```
檢查路徑沒有問題，這個檔案我是塞在exercise下沒錯，當前資料夾位置也對，怎麼會出現錯誤呢？

先看看檔案
```JAVA
package exercise;

public class Page31 {
  public static void main(String[] args){
    String name = "Charsin";
    
    System.out.println(name);
  }
}
```
錯誤訊息告訴我們沒有找到這個class，檔案所在的路徑為：```.../ch2/exercise/Page31.java```，仔細觀察一下，發現原來是因為這個檔案在exercise的package裡面，所以在執行的時候要退回到ch2那一層，輸入
```JAVA
java exercise.Page31
```
才能正常執行，為了不用一直切換位置，所以我們可以把終端機的座標停在ch2那一層資料夾，編譯可以這樣寫
```JAVA
javac exercise/Page31.java
```

###### 我覺得再過幾個月都會覺得現在的自己一定是卡到Ｘ才會錯在這種地方......這問題遇過兩次還不記得怎麼處理，欠記錄rrrr