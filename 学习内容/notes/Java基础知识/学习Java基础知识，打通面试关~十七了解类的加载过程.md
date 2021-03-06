我们在学习Java的时候总是会学习到很多基础知识，但是不怎么深入到类加载到虚拟机中的过程。今天我们就来了解下整个流程是怎么样的。明白我们所写的类文件是怎么运行在虚拟机中。
## 类的加载
   在我们Java程序中我们所写的Calss文件最终都会加载到内存当中，再次过程中会进行数据校验，转换解析和初始化的操作。完成后就可以形成我们虚拟机所需要的Java类型，这就是我们所说的虚拟机的类加载机制。
### 类加载的过程
   我们在类文件加载到虚拟机中会分为
   1. 加载 ： 
        - 我们在加载的过程中，虚拟机并没有定义什么时候必须开始加载。由程序运行成功中进行自行把握，简单的来说有很强的自我性。
        - 加载阶段实际上是将Java将字节码数据从不同的数据源中加载到JVM中，并加载成虚拟机可以识别的数据结构。 
   2. 链接：
       - 包含了三部分的操作，验证，准备操作，解析。数据验证与准备操作是按照顺讯开始进行，但是解析就不是这么做的，是因为我们在Java程序在执行的时候有部分程序是动态编译执行的。
       - 验证：保证虚拟机安全，检查字节信息是否符合虚拟机的规范。验证阶段主要完成四个阶段的检验动作，**文件格式验证，元数据验证，字节码验证，符号引用验证**
        a. 文件格式验证：验证是否字节流中的文件格式是否包含魔数0xCAFEBABE开头。当然还有很多其他的格式 验证，在此只是举例说明。
        b. 元数据验证： 数据符合Java语言的规范。
        c. 字节码验证：确保程序寓意是合法的，符合逻辑的。
        d. 符号引用验证：确保解析阶段是可以正常执行。
       - 准备：创建类或者是接口中的静态变量，初始化静态变量的初始值。这里是数据的初始化。
       - 解析：将常量池中的符号引用替换为直接引用。
   3. 初始化：
      在这部分初始化就行执行我们的代码逻辑操作，并且还有静态字段赋值操作。当然还有其他的，我们在简单如下操作一般都是进行初始化。
      > - 遇到 new、getstatic、putstatic或invokestatic这4条字节码指令时,类没有进行初始化需要进行初始化操作，还有调用类的静态方法的时候，也是同样的操作。
      > - 使用反射包的方法进行反射调用的时候，进行类的初始化。
      > - 初始化一个类时，存在父类的情况，会先进行父类的初始化。
      > - 虚拟机启动，执行主类，先初始化该类。
  
