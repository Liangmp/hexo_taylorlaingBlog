---
title: Java获取项目当前路径
date: 2017-11-23 16:55:28
tags:
  - Java
categories:
  - 技术
---
当多人合作共同完成一个项目的时候，项目的存放路径在每一台设备上不可能都一致，因此需要获取项目当前路径，方便项目代码实现项目文件查找和生成。
代码实现：
```java
package javaDemo;

import java.nio.file.Path;
import java.nio.file.Paths;

public class test {

    public static String getRootDirectory(){
        Path workingDirectory = Paths.get("").toAbsolutePath();
        return workingDirectory.toString();
    }

    public static void main(String[] args) {
        System.out.println(">>> Project directory: " + getRootDirectory());
    }
}
```
<!--more-->

运行结果：
```
>>> Project directory: D:\TaylorLiang\jase\ideaProjects\MyTest

Process finished with exit code 0
```