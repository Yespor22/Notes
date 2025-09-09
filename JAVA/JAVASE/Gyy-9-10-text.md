### Example
但是 Java 编译器在编译成 .class 文件时，默认不会保留这些参数名。

所以编译后的字节码里，参数只是占位符，JVM 只知道这是“第一个参数、第二个参数”，但名字变成了 arg0、arg1 或 MyBatis 里自动映射的 param1、param2。