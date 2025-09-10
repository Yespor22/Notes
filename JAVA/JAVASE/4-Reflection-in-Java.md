## Reflection
### 反射Reflction的介绍
反射机制使得程序能够在运行时反观和修改内部结构，反射允许程序在**运行时动态地操作类和对象。**
包括创建对象、访问字段和调用方法等等，但对于构建灵活的运用和复杂的框架非常重要

### 为什么要引入反射
```JAVA
public class Main {
    public static void main(String[] args) throws ClassNotFoundException {
        int field = User.publicStaticField;
        System.out.println(STR."field = \{field}");
        User.myPublicStaticMethod();
        User ye = new User("Ye", 22);
        System.out.println(ye.name);
        ye.myPublicMethod();
    }
}
```
这种访问清晰直观，但在有些场景中需要在运行时动态的操作成员，例如根据数据库中提供的类名或方法名或者基于字符串变量来动态实例化对象或调用方法时。 这种方式就不在试用了
反射机制提供了解决这类需求的能力，关键在于一个特殊的对象类对象————类对象(class对象)
### 什么是CLass对象
CLass对象是由JAVA虚拟机JVM在加载类时自动创建的，用于存储类的信息，通过Class对象就能访问类的结构以及对类本身和他的实例进行操作
JVM创建CLass对象的过程编写一个类并完成编译之后，编译器将其转换为字节码，存储在.class文件中，在类的加载过程中虚拟机利用Class Loader读取.class文件，将其中字节码加载到内存中。并基于这些信息创建对应的CLass对象，由于每个类在JVM只加载一次，所以每个类都对应着一个唯一的Class对象
获取Class对象
类字面常量<类名.class>
```JAVA
public class ClassTest {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException {
        //编译时就确定了具体的类，属于静态引用,存放User类的元数据，不会立即触发类的初始化；访问静态成员或创建实例才会触发
        Class<User> userClass = User.class;

        //运行时从User实例获取，具体类型在运行时创建和确认，在编译阶段无法判断class对象的确切类型
        User user = new User("Ye",22);
        Class<?> clazz = user.getClass(); //调用getclass方法类获取Class对象

        //forName静态方法，在运行时加载指定的类，并返回该类的Class对象实例，通常用于类名在编译时不可知的场景；立即触发类的初始化
        Class<?> clazz1 = Class.forName("com.ye.reflection.ClassTest");//字符串参数，表示代加载类的完全限定名Fully qualified name
    }
}
```


### 如何操作类？
```JAVA
public class ClassTest {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException { 
        //当前字段
        Field[] fields = clazz.getDeclaredFields();//获取当前类的所有字段，无视访问权限
        for (Field field : fields) {
            System.out.println(field.getName()); //返回字段名称
        }

        //父类及当前公共字段
        Field[] publicFields = clazz.getFields();//获取Public字段
        for (Field field : publicFields) {
            System.out.println(field.getName());
        }
        
        //获取单个字段
        Field name = clazz.getDeclaredField("name");
        System.out.println(name.getType());//字段类型
        System.out.println(name.getDeclaredAnnotation(MyAnnotation.class));//字段类型,（没有注解的字段null）
        Field comment = clazz.getDeclaredField("comments"); //comments是一个泛型 
        System.out.println(comment.getGenericType());//获取完整信息

        //通过反射获取字段的过程实在运行时动态执行的，所以无法在编译阶段进行错误检测和捕获，错误只在程序执行时被发现和处理
        Field comment1 = clazz.getDeclaredField("comment22s");//字段不存在，编译不报错，而是NoSuchFieldException
    }
}
类层面的操作
```JAVA
File publicField = clazz.getDeclaredField("publicStaticField")
System.out.println(publicField.get(null));//类的字段，不需要类的实例
//私有字段
File privatefield = clazz.getDeclaredField("privateStaticField")
private.setAccessible(true);//设置访问权限
System.out.println(privatefield.get(null));//类的字段，不需要类的实例
//修改字段
field.set(null,20)

//方法
Method[] methods = clazz.getDeclaredMethods();
for(Method method : methods){
    System.out.println(method.getName());
}

Method method = clazz.getDeclaredMethod("myPublicStaticMethod");
method.invoke(null);//调用方法

Method method = clazz.getDeclaredMethod(
    "myPublicStaticMethod",
    String.class
);
method.invoke(null,"Hi There");//调用方法
```
### 如何操作对象？
使用反射来创建类的实例，并对实例的字段值和方法进行访问和操作。在反射中，通过类的构造器来创建实例，简单来说先从目标类的Class对象中选择一个合适的构造器，然后通过调用他的newInstance方法来创建对象。
newIstance创建的对象是在运行时动态生成的，无法在编译阶段确切知道创建对象的类型，使用Object类型来接收


反射直接调用和操作对象的方法和字段
原因：在编写阶段明确转换类型，直接显示地调用更合适，而不必依赖于反射
反射真正的价值在于**处理编译时未知的类型，从而编写更具有通用性的代码**

### 反射的最佳实践（模拟框架）
创建Order实例并自动将Custormer和Address服务注入到Order实力当中

动态场景时存在限制，一旦代码完成，无法动态创建对象或调用方法

反射实现动态:"效仿常用框架的处理方式"



### 例子

Mybatis非常智能，配置映射关系，查询结果转换为实体类，属性会自动按照字段名称一一对应，免去了JDBC的繁琐操作。

- 底层通过反射赋值


mapUnderscoreToCameCase A_COLUMN -> aColumn

实际上Mybatis一开始会通过我们实体类默认的无参构造得到一个最初的对象，然后通过反射进行赋值，

Mybatis调用无参构造对象，属性则是通过反射进行赋值

但是注意，Mybatis仅仅是使用这种方式进行对象的构建，而字段的赋值无论是什么构造方法，都会使用反射进行一次赋值：

**接口注解**