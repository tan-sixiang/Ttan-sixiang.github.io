## 1.抽象类(abstract):

```java
3.所谓的抽象类，就是我们不想具体化一个类型所封装出来的类型
// - 1、不能实例化的
// - 2、抽象类存在的意义，他就是用来被继承或扩展的
// - 3、抽象类中不一定有抽象方法，但是有抽象方法一定它就是抽象类
// - 4、抽象类中也可以有具体的方法
// - 5、抽象类的子类不一定非要实现父类型中的抽象方法，它可以继续声明自己也是抽象的

//  没有具体实现（方法体）的方法称之为抽象方法
```

![1](image\1.png)

## 2.静态类(static)

```
// 1、static修饰的变量，它不依赖类的实例而存在，一般直接通过类名进行调用，它是这个类的实例所有共有的（它只有一份）
// 2、static修饰方法
// 3、static方法只能引用静态变量和静态方法
// 4、static一般都"只执行一次"或者"只有一份"
```

```java
static void testName() {
    System.out.println(name);
    // System.out.println(msg);
    testXxx();
    // 调用该方法，是不需要任何实例，也就是说不需要"对象.testName()",一般都是"类名.testName()"
    // 如果能调用testYyy，那么它一定是有一个成员在执行这个方法，
    // 程序流执行到这里就会无法找到这个具体的成员是谁
     testYyy();	//error
}

static void testXxx() {
    System.out.println("Xxx");
}

void testYyy() {
    System.out.println("Yyy");
}
```

// TODO 面试题：父子类中各个资源的初始化顺序 - **静态优先，然后是父类型优先**
//
// 1、父亲的静态属性 (1)
// 2、子类的静态属性 (1)
// 3、初始化父亲中的属性
// 4、构造父亲实例
// 5、初始化子类中的属性
// 6、构造子类实例

![2](image\2.png)





## 3.final类:

```java
// final 最终的
// 1、被final修饰的变量，具有"不可改变"的特性
// 2、修饰基本类型：其值不可以再进行修改
// 3、修饰引用类型
    static void testReference() {
        final Student stu = new Student();
        // 可以改 - 地址没有变
        stu.setName("A");
        stu.setName("B");
        // new一定是在内存中创建了一个新对象，所以地址会改变
        // stu = new Student();
// 4、修饰类：这是这个类的最终版，不能被扩展和继承
// 5、修饰方法：这是这个方法的最终版，不能被重写
final class A {}
```



// 6、**final修饰的变量可以在构造器中进行第一次赋值初始化**

```java
class B {
    final String name;
}
public B() {
    name = "Default name"; // 只能第一次去赋值初始化
}
```
![3](image\3.png)