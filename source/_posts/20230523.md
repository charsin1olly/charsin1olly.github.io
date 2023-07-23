---
title: JAVA Hello World!
date: 2023-05-23 19:13:35
tags: [JAVA]
---
凡是開始學一種程式語言，第一個要學的一定是Hello World～
這是JAVA的寫法：

```java
class HelloWorld{
    public static void main(String[] args){
      System.out.println("Hello, World!");  
  }
}
// 檔名 HelloWorld.java
```
比起RUBY多很多字，多寫那麼多字是為什麼呢？先來看看JAVA程式碼的執行方式 ：
a. 先用```javac （檔案全名+副檔名）```執行編譯 ：```javac HelloWorld.java```編譯HelloWorld文件
b. 再用```java (class名稱)```指令執行，就是```java HelloWorld``` 執行剛才編譯出來的class檔，輸出```Hello, World!```


---

### 1. JAVA都要有class才能執行，ＨelloWorld是他的class名

### 2. ```public static void main```
* 一個入口，每一個java檔都要有一個main方法才能運行，雖然沒有main，javac編譯能過，但是java執行的時候會顯示錯誤訊息。（我的想法：它就是一個車頭，從它帶動整個class的運作）
```java
class HelloWorld{
    public static void main1(String[] args){
    System.out.println("Hello, World!");  
  }
}

// java HelloWorld 輸出

Error: Main method not found in class HelloWorld please define the main method as:
   public static void main(String[] args)
or a JavaFX application class must extend javafx.application.Application
```
＊ 大小寫固定，例如：把public改成Public會無法編譯
```java
class HelloWorld{
    Public static void main(String[] args){
      System.out.println("Hello, World!");  
    }
}

// javac HelloWorld.java 輸出
HelloWorld.java:2: error: <identifier> expected
    Public static void main(String[] args){
          ^
1 error
```
但是，檔名在Ｗindows會不區分大小寫（以下為mac輸出結果）
```java
class HelloTaiwan2{
  public static void main(String[] args){
    System.out.print("Hello, World! 安安台灣！");  
    System.out.print("Hello, World! 安安台灣！");  
  }
}

// javac HelloWorld.java(這串code我寫在HelloWorld檔案裡面)
// java Hellwtaiwan輸出
Error: Could not find or load main class Hellotaiwan2
Caused by: java.lang.NoClassDefFoundError: HelloTaiwan2 (wrong name: Hellotaiwan2)

```

### 3.其他列印方法
* System.out.println會換行
```java
class HelloTaiwan1{
  public static void main(String[] args){
    System.out.println("Hello, World! 安安台灣！");  
    System.out.println("Hello, World! 安安台灣！");  
  }
}

// javac HelloTaiwan1.java 輸出
Hello, World! 安安台灣！
Hello, World! 安安台灣！
```

* System.out.print不會換行
```java
class HelloTaiwan2{
    public static void main(String[] args){
      System.out.print("Hello, World! 安安台灣！");  
      System.out.print("Hello, World! 安安台灣！");  
  }
}

// javac HelloTaiwan2.java 
Hello, World! 安安台灣！Hello, World! 安安台灣！
```

### 4.一個java檔案可以有很多class，public的class名和檔名相同才能編譯。
```java
//檔名：HelloWorld

public class HelloWorld1{
    public static void main(String[] args){
      System.out.println("Hello, World!");  
    }
}

// javac HelloWorld.java輸出
HelloWorld.java:1: error: class HelloWorld1 is public, should be declared in a file named HelloWorld1.java
public class HelloWorld1{
       ^
1 error
```

### 5. public方法只能有一個
```java
public class HelloWorld{
    public static void main(String[] args){
      System.out.println("Hello, World!");  
    }
}

public class HelloTaiwan1{
  public static void main(String[] args){
    System.out.println("Hello, World! 安安台灣！");  
  }
}

// javac HelloWorld.java 輸出
HelloWorld.java:7: error: class HelloTaiwan1 is public, should be declared in a file named HelloTaiwan1.java
public class HelloTaiwan1{
       ^
1 error
```