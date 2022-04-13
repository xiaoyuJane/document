

### java接口

- interface关键字修饰
- 可以包含变量和方法
  - 变量被隐式指定为`public static final`
  - 方法被隐式指定为`public abstract`

- 接口支持多继承，接口可以extends多个接口
- 一个类可以实现多个接口



jdk1.8中对接口增加了新特性

- 默认方法（default method）：JDK 1.8允许给接口添加非抽象的方法实现，但必须使用default关键字修饰

  - 定义了default的方法可以不被实现子类所实现，但只能被实现子类的对象调用
  - 如果子类实现了多个接口，并且这些接口包含一样的默认方法，则子类必须重写默认方法；

- 静态方法（static method）：JDK 1.8中允许使用static关键字修饰一个方法，并提供实现，称为接口静态方法

  - 接口静态方法只能通过接口调用（接口名.静态方法名）。

    

---



### java抽象类

- 被abstract修饰
- 抽象类不能被实例化只能被继承
  - 一个子类继承一个抽象类，则子类必须实现父类抽象方法，否则子类也必须定义为抽象类；
- 抽象类可以包含属性、方法、构造方法，但是构造方法不能用于实例化，主要用途是被子类调用。
- 抽象类不一定含有抽象方法，抽象类中的抽象方法的修饰符只能为public或者protected，默认为public；
- 

### java8

#### :: method references

There are four kinds of method references:

- Reference to a **static method** `ClassName::staticMethodName`
- Reference to an **instance method** of a particular object `Object::instanceMethodName`
- Reference to an instance method of an arbitrary object of a particular type `ContainingType::methodName`–
- Reference to a constructor `ClassName::new`



``` java
List<String> list = Arrays.asList("node", "java", "python", "ruby");
list.forEach(System.out::println);          // method references


List<String> list = Arrays.asList("node", "java", "python", "ruby");
list.forEach(str -> System.out.println(str)); // lambda
```



### java对象

#### object类的方法

* toString 。 该方法返回一个代表该对象的字符串。该方法的默认实现返回的字符串在绝大多数情况下是没有信息量的，因此通常都需要在子类中重写该方法。

* equals。该方法检验两个对象是否相等。该方法的默认实现使用 `==` 运算符检验两个对象是否相等，通常都需要在子类中重写该方法。

  *  `==` 运算符，比较的是值是否相等，如果是对象，则比较的是对象所指向的内存地址是否相等。

  * 重写该方法，可以根据对象的值来判定是否相等。

  * ``` java
    #Object中equals()的默认实现
    public boolean equals(Object obj) {
        return (this == obj);
    }
    ```

* hashCode 。该方法返回对象的散列码。

  * public native int hashCode() ， `native` 方法表示实现方法的编程语言不是 Java

  * 散列码是一个整数，用于在散列集合中存储并能快速查找对象。

  * 根据散列约定，如果两个对象相同，它们的散列码一定相同，因此如果在子类中重写了 equals 方法，必须在该子类中重写 hashCode 方法，以保证两个相等的对象对应的散列码是相同的。

  * 两个相等的对象一定具有相同的散列码，两个不同的对象也可能具有相同的散列码。实现 hashCode 方法时，应避免过多地出现两个不同的对象也可能具有相同的散列码的情况。

    

* finalize。该方法用于垃圾回收。如果一个对象不再能被访问，就变成了垃圾。`finalize` 方法会被该对象的垃圾回收程序调用。该方法的默认实现不做任何事，如果必要，子类应该重写该方法
* getClass。该方法返回对象的元对象。元对象是一个包含类信息的对象。包括类名、构造方法和方法等

* clone 。该方法用于复制一个对象，创建一个有单独内存空间的新对象

  * 不是所有的对象都可以复制，只有当一个类实现了 java.lang.Cloneable 接口时，这个类的对象才能被复制。

  * 该方法可能抛出 CloneNotSupportedException 异常。

  * new 对象和clone对象的区别。

    > - 程序执行到new操作符时， 首先去看new操作符后面的类型，因为知道了类型，才能知道要分配多大的内存空间。
    > - 分配完内存之后，再调用构造函数，填充对象的各个域，这一步叫做对象的初始化。
    > - 构造方法返回后，一个对象创建完毕，可以把他的引用（地址）发布到外部，在外部就可以使用这个引用操纵这个对象
    >
    > new操作符的本意是分配内存。调用clone方法时，分配的内存和源对象（即调用clone方法的对象）相同，然后再使用源对象中对应的各个域，填充新对象的域， 填充完成之后，clone方法返回，一个新的相同的对象被创建，同样可以把这个新对象的引用发布到外部。

    ``` java
    
    Person p = new Person(23, "zhang");  
    Person p1 = p;   #引用的复制，p和p1指向同一个内存地址
    
    Person p = new Person(23, "zhang");  
    Person p1 = (Person) p.clone();  #对象的复制，p和p1指向的内存地址也不同
    ```

#### 浅复制和深复制

- 浅复制：被复制对象的所有变量都含有与原来的对象相同的值，而所有的对其他对象的引用仍然指向原来的对象。换言之，浅复制仅仅复制所考虑的对象，而不复制它所引用的对象。
- 深复制：被复制对象的所有变量都含有与原来的对象相同的值，除去那些引用其他对象的变量。那些引用其他对象的变量将**指向被复制过的新对象**，而不再是原有的那些被引用的对象。换言之，深复制把要复制的对象所引用的对象都复制了一遍。



#### 对象的比较

Java中提供了两种方式来使得对象可以比较大小，实现`Comparator`接口或者`Comparable`接口

- Comparator接口

  实现Comparator接口需要重写其中的compare()方法。

  ```java
  int compare(T o1,T o2)
  ```

  根据第一个参数小于、等于或大于第二个参数分别返回负整数、零或正整数，通常使用-1, 0, +1表示。

  ``` java
  public class Student {  
  	//省去Student类的定义过程..	
  	public static void main(String[] args) {
  	    Student stu1 = new Student("sakuraamy",20);
  		Student stu2 = new Student("sakurabob",21);
  		Student stu3 = new Student("sakura",19);
  
  		ArrayList<Student> stuList = new ArrayList<>();
  		stuList.add(stu1);
  		stuList.add(stu2);
  		stuList.add(stu3);
  
      //没有必要去创建一个比较器类 采用内部类的方式实现Comparator接口
  		Collections.sort(stuList, new Comparator<Student>() {
  			@Override
  			public int compare(Student o1, Student o2) {
  				return (o1.age<o2.age ? -1 : (o1.age == o2.age ? 0 : 1));
  				//return o1.name.compareTo(o2.name);
  			}
  		});
      //或者使用lambda表达式
      //Collections.sort(stuList, (o1,o2)->o1.age-o2.age);
  		System.out.println(stuList); 
          //输出 [name:sakura age:19, name:sakuraamy age:20, name:sakurabob age:21]
  	}
  }
  ```

- 以`able`结尾的接口都表示拥有某种能力。若是某个自定义类实现了comparable接口，则表示**该类的实例对象拥有可以比较的能力**

  实现comparable接口需要覆盖其中的compareTo()方法。

  ```Java
  int compareTo(T o)
      
  public class Student implements Comparable<Student>{
  	//省去Student的构造过程
  
    //重写comparaTo方法 以age作为标准比较大小
  	@Override
  	public int compareTo(Student o) {
  		return return (this.age<o.age ? -1 : (this.age == o.age ? 0 : 1));;//本类接收本类对象，对象可以直接访问属性(取消了封装的形式)
  	}
  
  	public static void main(String[] args) {
  		Student stu1 = new Student("sakura",20);
  		Student stu2 = new Student("sakura",21);
  		Student stu3 = new Student("sakura",19);
      //TreeSet会对插入的对象进行自动排序，所以要求知道对象之间的大小
  		TreeSet<Student> stuSet = new TreeSet<>();  
  		stuSet.add(stu1);
  		stuSet.add(stu2);
  		stuSet.add(stu3);
      //使用foreach(), lambda表达式输出stuSet中的值 forEach()方法从JDK1.8才开始有
  		stuSet.forEach(stu->System.out.println(stu));
  	}
  }
  /*
  output:
  name:sakura age:19
  name:sakura age:20
  name:sakura age:21
  */
  ```

### java异常

 Java 语言中所有错误或异常的超类（父类）为Throwable 

Throwable ，是对所有异常进行整合的一个普通类。它的作用就是能够**提取保存在堆栈中的错误信息**。

- 成员方法：
  - public String getMessage()：返回此 throwable 的详细消息字符串
  - public String toString()：获取异常类名和异常信息。
  - public void printStackTrace()：获取异常类名和异常信息，以及异常出现在程序中的位置。
  - public void printStackTrace(PrintStream s)：通常用该方法将异常内容保存在日志文件中，以便查阅。
- 异常的分类：
  - 异常(Exception)
  - 编译时异常: 凡是Exception或者是Exception的子类都成为编译时异常,这种是可以解决的,一般编译不通过
  - 运行时异常: 凡是RuntimeException或者是RuntimeException的子类都成为运行时异常,这种也是可以解决的,一般都是代码不够严谨或者逻辑错误
  - 错误 (Error)



 > 为什么将throwable设计为一个普通类？
  >
  > 1. 因为Throwable里面存储的是错误描述的对象体现，是字符串，只不过把这些字符串表示为一个对象
  > 2. 子类的解决异常处理方法里都是构造方法，一个是无参构造，另外一个就是带字符串参数（对象）的带参构造，既然有了构造方法，那就可以直接从父类中直接提取所需要的异常处理信息从而来构造一个方法，这样可以省略子类很多代码
  > 3. 普通类继承的话是直接继承，不能够改变，如果改变的话就会影响到父类，根据这个特点也可以很清楚的说明Throwable为什么是普通类，因为它压根就不需要子类重写方法，只需要提取信息便可。



> jvm处理异常的方式？
>
> 1. 打印错误信息 （异常的类名，异常的信息，异常的位置，错误的行号）
>
> 2. 将程序停止



> 我们处理异常的方式
>
> 1. 使用try catch来捕获异常并作处理，使得程序继续正常执行下去。如果未捕获到，还是会交给jvm的，所以建议把Exception作为catch的参数类型放在异常处理格式的最后
>
> 2. 在开发中,有的时候我们没有权限处理该异常,我们不知道该如何处理异常,或者不想处理异常,这种情况下我们可以将异常抛出,抛出给调用者处理
>
> 3. throw和throws的作用都是将异常抛出给调用者或者虚拟机来处理，但是两者有个根本区别就是throw的是**异常对象**，而throws的是**异常类**。throw在方法体内出现,throws在方法的声明上
>
> 4. 抛出异常的处理方法千万不能抛出给JVM处理[主方法]，调用者最好都处理，编译时异常必须出来，运行时异常建议处理。
>
>    



###  位数组

位数组的应用是用更少的内存构建hashmap进行判断某个数值是否存在在海量的数据中。

- 位数组的核心思想是用一个char来表示8个整数，char转换成2进制后，正好是8位长，每一位表示一个整数

  > 10011010，分别对应0,1,2,3,4,5,6,7，其中0存在，3存在，4存在，6存在，其他不存在。
  >
  > 一个char数组表示8*lenth个数字了，内存大大减少





### java 并发

#### 同步异步

同步和异步关注的是消息通信机制

- **同步是指:** 发送方发出数据后, 等待接收方发回响应后才发下一个数据包的通讯方式.

  > 就是在发出一个调用时, 在没有得到结果之前, 该调用就不返回, 但是一旦调用返回, 就得到返回值了. 
  >
  > 也就是由"调用者"主动等待这个"调用"的结果.

  1. 任务A和任务B之间有关联, 例如任务B中途要给任务A一个数字, 那么**任务A或许需要等待任务B生产这个数**, 任务A需要等待任务B的这个动作叫做同步.

  2. ```java
     //同步阻塞
     int i = System.in.read();
     //当命令终端没有输入时, 调用该方法的线程被阻塞 ,表现出和终端同步
     
     
     //同步非阻塞
     concurrentLinkedQueue.offer((T) t);
     //该过程一个元素需要入队列, 该并发队列为了让当前线程不阻塞而又能正确入队, 使用CAS算法实现的乐观锁循环尝试入队. 
     //offer()方法并没有阻塞当前线程, 而又希望同步, 于是通过循环来实现, 最终实现同步非阻塞.
     ```

  

- **异步是指:** 发送方发出数据后, 不等待接收方发回响应, 接着发送下个数据包的通讯方式. 

  > 当一个异步过程调用发出后, 调用者不会立刻得到结果. 而是在调用发出后, "被调用者"通过状态、通知来通知调用者, 或通过回调函数处理这个调用.

  异步: 事件A和事件B之间没有关联, 是相互独立的, 那么相互都不用管对方干了什么.

```java
//异步非阻塞

//callable内的任务结果没有马上需要的必要, 于是调用submit()方法马上返回一个实现Future的存根. callable任务对于当前线程是异步的, 不需要阻塞当前线程.
Future<T> future = threadPool.submit(Callable<T> callable);
// doSomething

//需要callable任务的结果时, 就需要同步了, get()方法通过阻塞来实现
future.get();

```

####  阻塞非阻塞

阻塞和非阻塞属于进程API执行动作的方式, 关注的是程序在等待调用结果时的状态.

- **阻塞是指:** 调用结果返回之前, **当前线程**会被挂起. 

  >  函数只有在得到结果之后才会返回, 线程需要等待结果.

  线程A需要等待线程B, 于是线程A在等待这个数的步骤上被挂起, 不能分到cpu, 不能执行, 这样被称为阻塞.

  

- **非阻塞是指:** 与阻塞的概念相对应, 指在不能立刻得到结果之前, 该函数不会阻塞**当前线程**, 而会立刻返回. 线程不需要等待结果.

  > 理解为不负责责任的，调用函数没有得到结果，函数立刻返回，当前线程不会被阻塞

  线程A同样需要线程B给一个数, 但是线程A仅仅告知线程B要给这个数, 并没有马上就要使用这个数, 此时线程A没有被挂起, 仍然能分到cpu, 仍然能执行, 这样被称为非阻塞.