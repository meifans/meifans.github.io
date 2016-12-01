## 代码随笔
### interface
+ 接口中字段前 public static final ，反编译后消失。默认为psf的。

### final
+ final修饰方法入参，反编译后final消失，只存在于编译阶段。
> 《深入jvm》提到入参class结构中没有代表final的指令。
