## 泛型

### Why Use Generics
提高代码复用率
```jAVA
public class IntegerPrinter{
    Integer content;
    InterPrinter(Integer content){
        this.content = content;
    }

    public void print(){
        System.ou.println(content)
    }
}

public class StringPrinter{
    String content;
    InterPrinter(String content){
        this.content = content;
    }

    public void print(){
        System.ou.println(content)
    }
}
```

### Generic CLasses
```JAVA
public class Printer<T,K>{
    T content1;
    K content2
    InterPrinter(T content1,K content2){
        this.content1 = content1;
        this.content2 = content2;
    }

    public void print(){
        System.ou.println(content1+content2)
    }
}
```
Use(T必须为包装类,为占位符)
```JAVA
Printer<T,K> printer = new Printer<>(123,"Test");
printer.print();
}
```

### Bounded generics:extends
`public class Test<T extends Vehicle>{}`

class&interface
`public class Test<T extends Vehicle & Thing>`

### Type-safe
泛型的工作方式实在编译阶段进行类型检查而不是运行时

### Generic Methods
```JAVA
private static <T,K> void pritn(T content1, K content2){
    System.out.println(content)
}
```
<T>表明是一个泛型

### Wildcard:?
`private static void print(List<?> conten){}`

- upper bounded wildcoard: `List<? extends Person>`
- lower bounded wildcoard: `List<? super Student>`

### Word
Generics
Wildcard
{} Curly Braces
<> Angle Brackets
? Question Mark