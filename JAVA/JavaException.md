## IO Stream
NotSerializableException:没有做序列化

implemnts Serializable 

FileNotFoundException

ConnectException:Connection refused:connect
- 服务器端得优先启动
## IO优化2

```JAVA
if(choice == 2){
    //Input Information

    //Creating a book object
    Book book = new Book(Bno,bName,bAuthor,)

    //Creating list to store data
    Arraylist bookInformation = new Arraylist();
    bookInformation.add(book);

    //Writing list into disk
    File file = new File("location");
    //Stream and Write 
}
```

上述代码会导致文件被覆盖写入，而是追加写入为什么呢？

## 程序、进程、线程
进程是操作系统进行**资源分配**的基本单位

线程是操作系统**调度执行**的基本单位

### 创建线程
1. **继承Thread类**
2. Runnable接口
3. Callable接口

## 网络编程
设备之间进行数据的传输，发送/接受数据。

### IP地址
用来标志网络中的一个通信实体的地址。通信实体可以是计算机，路由器等

### 端口号
计算机上多台应用程序，使用端口号来区分这些应用程序

### 网络通信协议
TCP/IP协议，工程师大部分接触应用层（传输层：UDP/TCP）

## XML的引入
Extensiable Markup Language 纯文本

被设计用来结构化、存储以及传输信息
### XMl解析
hasNext()判断是否有下一个元素
获取元素，同时指针下移

## 注解


## Maven
### 资源坐标
GroupID : company
Artifactid :jar package name
Version

## Mybatis
### 持久层框架
### ORM（Object/Relation/Mapping）