## Lambda表达式

### Lambda Introduction
### interface
接口用来定义一个协议或约定，只声明方法但不提供方法的具体实现
`public interface Vehicle {void start(); //Abstract Metho}`

实现类
```JAVA
public class Car implements Vehicle{
    public void start(){System.out.println("Starting car engine")}
}
``` 
业务中只需要关心方法而不要关心具体的实现类，从而实现代码的解耦和模块化

**Message.java:** 
```JAVA
public interface Message{
    void send();
}
```

**Email.java:** 
```JAVA
public class Email implements Message {
    String emali;
    public Email(String emali) {
        this.email=email;
    }
    public void send() {
        System.out.println("This is Email.");
    }
}
```
**Sms.java:** 
```JAVA
public class Sms implements Message {
    String phoneNumber;
    public Sms() {

    }
    public void send() {
        System.out.println("This is sms.");
    }
}
```
**Main.java:**
```JAVA
public static void main(String[] args){
    Message email = new Emial("test@email")
    sendMessage(email);
}

static void sendMessage(Message message){
    message.send();
}
```
参数类型为Message接口，实现类已经send方法，所以sendMessage内部只用执行message.send(),而不需要关心执行的到底是哪个对象的send方法，免去了复杂的判断和切换。（接口编程）
### Lambda表达式引入
实现接口：太过复杂，创建类，实现方法，实例化对象，调用方法
Lambda：快速简洁实现接口，直接在Lambda表达式定义即可
### Grammar
**Message.java:** 
```JAVA
public interface Message{
    void send();
}
```
**Main.java:**
```JAVA
public static void main(String[] args){
    sendMessage(() -> {
        System.out.println("This is Email.");
    })
}
static void sendMessage(Message message){
    message.send();
}
```

Lambda可以赋值给变量,十分简洁方便
**Message.java**
```JAVA
public inter Message{
    String send(String name,String title);
}
```
**Main.java:**
```JAVA
public static void main(String[] args){
    Message lambda = (name,title) -> {
        System.out.println("This is Email to" + title + " " + name );
        retur "success!"
    }
    sendMeaasge(lambda);
}
static void sendMessage(Message message){
    String status = message.send("Ye"."Mr");
}
```
### 函数式接口与Lambda表达式

**使用场景：**`有且只有一个抽象方法的接口上`，这样接口为函数式接口（Functional Interface）
存在多个抽象方法无法判断哪一个是需要实现的，上述的send满足条件

使用注解的方式 **@FunctionalInterface**表示这是一个函数式接口（建议标注，编译报错便于Debug，更好理解设计意图）

Lambda是语法糖用于简化函数式接口的实现，Java内置库中包含多种函数式接口比如:Predicate,Function...

### Word
Lambda Expressions
Functional Interface
Abstract Method
()Parentheses
\- Hyphen