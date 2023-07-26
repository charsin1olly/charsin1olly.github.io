---
title: 如何使用JDBC連接資料庫(mysql)
date: 2023-07-26 23:19:14
tags: [JAVA, Eclipse, SQL]
---
這邊我是連接公司的XAMPP伺服器上的MySQL，以為連接方式會跟一般MySQL不同(因為公司專案的檔案寫法跟連接SQL Server差很多，雖然看得出意思差不多......)

## 1. 產生一個Package來裝檔案
功能相近或相關的JAVA檔案通常會放在同一個Package裡，這次要接資料庫也一樣，幫它開一個包廂(X)，package的命名也有慣例，這邊就不歪樓了 ~~(實際上是自己也還搞不清楚)~~ 
在專案的```Java Resources/src```資料夾右鍵，新建一個Package(套件)，然後建立一個JAVA檔案```dbConnect.java```
![](https://hackmd.io/_uploads/B1Lv4SC92.png)

## 2. 準備套件
在JAVA使用SQL主要是依賴java.sql這個系列的(?)jar包，剛開始嘗試寫連接的code時，Eclipse的自動修正幫我import了
```java
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Connection;
import java.sql.Statement;
```
雖然要能動，import這些檔案就行了，但import一大串不太好看，萬一又要用其他sql功能可能又要再加，在網上查到很多資料都是直接引入```java.sql.*```，所以這邊我就引入整包sql的package。
```java
import java.sql.*;
```


## 3. 連接
終於可以開始連接資料庫啦~老樣子先創建一個main方法，使用try執行，我習慣在測試的時候印訊息，確保有成功啟動，搭配catch捕捉錯誤訊息比較好除錯。

a. 首先裝上第一個零件：driver，使用```Class.forName(dbDriver)```註冊驅動，如果有順利啟動就會在終端機Log看到「驅動成功啟動」的訊息
    
b. 第二個零件：資料庫登入訊息，就像上飛機要檢查機票一樣，要知道我們要去哪裡，核對身分證以及姓名，這邊DriverManager提供的```getConnection()```方法可以告訴電腦我要連去哪個資料庫(格式：```jdbc:資料庫://IP位址:port/欲連接的table```)、登入資料庫的帳號密碼(根據之前Rails開發的經驗，Java的帳號密碼資訊應該也是也要丟在其他檔案的吧，這樣直接寫在Code超可怕的耶~"~ 有空研究一下)

```java
Connection dbConn=DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "(你的帳號)", "(你的密碼)");
```
總結這個步驟3，現在code長這樣
```java
public class dbConnect{
    public static void main(String[] args) {
        try {
            Class.forName("com.mysql.jdbc.Driver");
            System.out.println("驅動成功啟動");
            
            Connection dbConn=DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "(你的帳號)", "(你的密碼)");
            System.out.println("連接成功");

        }catch(ClassNotFoundException e) {
            e.printStackTrace();
            System.out.println("找不到驅動程式");
			
        }catch(Exception e){
            e.printStackTrace();
            System.out.println("加載失敗");
        }
    }
}
```

## 4. 查詢SQL資料
在try的block繼續加上code，畢竟連接成功才能搜尋嘛~
建立一個和資料庫溝通用的Statement物件，搭配儲存結果用的ResultSet物件進行SQL查詢，再用
迴圈把結果轉出來
```java
Statement stmt = dbConn.createStatement();
String sql="SELECT *  FROM user";
ResultSet rs = stmt.executeQuery(sql);		

System.out.println("-----資料輸出開始-----");
while (rs.next()) {
    String name = rs.getString("name");
    int age = rs.getInt("age");
    String gender = rs.getString("gender");
    String email = rs.getString("email"); 
    System.out.println(name+","+age+","+gender+","+email);
}
System.out.println("-----資料輸出完畢-----");
```
呈現出來的結果
![](https://hackmd.io/_uploads/SJy0gvR5h.png)

## 5. 清除垃圾
最後，我們使用完查詢要記得關閉資料庫連接，把剛才建立的物件清乾淨，減少記憶體的負擔
```java
dbConn.close();
stmt.close();
rs.close();
```

## 6. 整理連接用的數據
全部塞在code裡面很長，把這些資料整理出來另外寫比較好維護，而把這些落落長的資料寫成變數放在方法裡也比較好理解這些方法帶入的資料代表的是什麼。
```java
private static String dbDriver="com.mysql.jdbc.Driver";
private static String dbURL="jdbc:mysql://localhost:3306/test";
                            
private static String userName="你的帳號";
private static String userPassword="你的密碼";
```


## 最後成果
```java
package com.test.dbConnect;

import java.sql.*;

public class dbConnect{
    private static String dbDriver="com.mysql.jdbc.Driver";
    private static String dbURL="jdbc:mysql://localhost:3306/test";
    private static String userName="你的帳號";
    private static String userPassword="你的密碼";
    
    public static void main(String[] args) {
        try {
            Class.forName(dbDriver);
			
            Connection dbConn=DriverManager.getConnection(dbURL, userName, userPassword);
            Statement stmt = dbConn.createStatement();
			
            String sql="SELECT *  FROM user";
            ResultSet rs = stmt.executeQuery(sql);			
            while (rs.next()) {
                String name = rs.getString("name");
                int age = rs.getInt("age");
                String gender = rs.getString("gender");
                String email = rs.getString("email");
                System.out.println(name+","+age+","+gender+","+email);
            }
                    
            dbConn.close();
            stmt.close();
            rs.close();
	        
        }catch(ClassNotFoundException e) {
            e.printStackTrace();
            System.out.println("找不到驅動程式");
			
        }catch(Exception e){
            e.printStackTrace();
            System.out.println("加載失敗");
        }
    }
}
```

## 為什麼還是連不上?
### java.lang.ClassNotFoundException: com.mysql.jdbc.Driver
出現這就代表mysql-connecter的jar包可能沒有被成功的引入到這個專案，這次的解決方法是：
a. 工作區的專案名稱按右鍵/內容
![](https://hackmd.io/_uploads/Syn9oE09h.png)

b. JAVA 建置路徑/按類別路徑/add library/Web 應用程式程式庫/下一步/完成
![](https://hackmd.io/_uploads/Hyi87SC52.png)
如果本身專案有Web應用程式庫，可以檢查看看```WEB-INF\lib```資料夾有沒有```mysql-connector-java-(版本號).jar```檔案，可能只缺它，如果沒有的話可以去[MySQL](https://dev.mysql.com/downloads/connector/j/5.0.html)下載，windows可以選擇Platform Independent版本的zip檔，解壓縮就會獲得jar檔了。

c.新增完成後就能解決這個問題~

比對了一下發現Java Resources底下的Libraries資料夾，原本直接寫好code就能動的專案，底下有個Web應用程式庫，不知道是不是new專案的時候選了什麼選項自動生成的，既然漏掉了，現在知道怎麼補救了(經驗+1)
![](https://hackmd.io/_uploads/BJvV5E05n.png)


## 參考資料
[Lesson: JDBC Introduction](https://docs.oracle.com/javase/tutorial/jdbc/overview/index.html)
[JDBC查詢資料範例](https://tw511.com/20/213/8346.html)
[JDBC快速入門教學](https://tw511.com/20/213/8321.html)
[Installing MySQL JDBC driver(下載driver教學)](https://docs.informatica.com/integration-cloud/data-integration-connectors/current-version/mysql-connector/introduction-to-mysql-connector/administration-of-mysql-connector/installing-mysql-jdbc-driver.html)
[java.lang.ClassNotFoundException: com.mysql.jdbc.Driver in Eclipse](https://stackoverflow.com/questions/17484764/java-lang-classnotfoundexception-com-mysql-jdbc-driver-in-eclipse)