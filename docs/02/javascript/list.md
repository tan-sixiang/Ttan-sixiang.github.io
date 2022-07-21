## 一. Calendar和Date的使用

````java
public static Date incrementDate(Date date,int month) {
Calendar now = Calendar.getInstance();
//获取到当前时间now.setTime(date);
//用带有意义的单词将这个变量语义话
   now.add(calendar. MONTH,month);
   return now.getTime();
}

public static void main(String[] args) {
Date date = incrementDate(new Date(,month: 2);
SimpleDateFormat sdf = new SimpleDateFormat( pattern: "yyyy-MM-dd HH:mm:ss");
//sdf.parse()	String转Date
//Date类型转String类型 format()
String format = sdf.format(date);       system.out.println(format);
}

````

## 二. Collection

![集合结构](E:\博客\Ttan-sixiang.github.io\docs\02\javascript\image\01.png)

```java
// 创建一个空的集合列表
Collection<Object> c1 = new HashSet<>();
```



### 1. 集合，数组，字符串之间的转换

````java
//toArray 将集合变成数组 
 Object[] arr = coll.toArray(); //coll一个集合

//Arrays.toString 将数组变成字符串形式 
System.out.println(Arrays.toString(arr)); 

//将数组转成集合 
int[] nums = {1,2,3,4}; 
List asList = Arrays.asList(nums); 
System.out.println(asList); 
````

### 2.List的遍历方式

````java
// List集合遍历的三种⽅式：
// 1、迭代器 
// 2、for循环 
// 3、foreach循环(增强for循环) 可以遍历数组和集合 
// 语法：
//	for(元素的类型 变量 : 数组|集合){ 变量就表⽰遍历出来的元素 
//	} 

// 迭代器遍历
Iterator<String> it = list.iterator();
while(it.hasNext()) { 
    System.out.println(it.next()); 
} 			     
// for循环遍历
for (int i = 0; i < list.size() ; i++) {
    System.out.println(list.get(i));
}  
// foreach循环遍历
for(String s : list) { 
    System.out.println(s);
}
````



### 3. 迭代器

#### 3.1迭代器原理

​	迭代是重复反馈过程的活动,其⽬的通常是为了逼近所需⽬标或结果。每⼀次对过程的重复称为⼀次“迭代”, 而每⼀次迭代得到的结果会作为下⼀次迭代的初始值。

![迭代器](E:\博客\Ttan-sixiang.github.io\docs\02\javascript\image\02.png)

#### 3.2迭代器作用(Iterator)

```java
// 获取到能访问这个容器中的元素的一个指针，它默认是指向这个容器中第一个元素的上方
Iterator<Object> it = c1.iterator();

// 它会往下移动一格，然后查看这个时候，指针指向的位置是否有数据
while(it.hasNext()){
    System.out.println(it.next()); // 读取此时指针指向的元素
}

//迭代器的作⽤：获取集合中的所有的元素 
 Collection coll = new ArrayList(); 
 coll.add("jack"); 
 coll.add("rose"); 
 coll.add(10); 
 coll.add(20.2); 
 //1、获取迭代器对象 
 Iterator it = coll.iterator(); 
 while(it.hasNext()) { 
	System.out.println(it.next()); 
 } 
 System.out.println(coll);
```

#### 3.3迭代器使用常见问题

1、迭代器迭代完成之后，迭代器的位置在最后⼀位。 所以迭代器只能迭代⼀次 

2、迭代器在迭代的时候，不要调⽤多次next⽅法，可能会出错 NoSuchElementException 

3、在迭代器迭代的时候，不能向集合中添加或者删除元素 ConcurrentModificationException



## 三. Array

### 1. ArrayList的特点

```java
// List特点
// 1、有序的（插入有序性）
// 2、可以放置重复元素

// ArrayList
// 1、基于数组实现的，具备了数组所有的优点
// 2、动态扩容
// 3、随机查找速度非常快（基于下标访问的），随机插入非常慢，如果插入的index非常靠前，那么后面的每一个元素都要为前一个元素腾出位置来
```

创建方式:

```java
// 所有的集合在使用泛型的时候，只能使用封装类型，不能使用基本类型
//基本类型要用它的包装类
List<Integer> list = new ArrayList<>();
```

```java
list.add("d"); //按顺序添加
list.add(1,"x"); // inert：在index的前面插入自己
list.set(0,"aa");//为指定位置设置值(替换)
list.get(0);//根据索引来获取特定的元素
System.out.println(list.contains("x"));//包含查找(true,false)

```

2.底层实现原理

````java
ArrayList底层实现原理: ArrayList底层使用数组实现.
add方法:
1、如果是第一次添加，那么将数组的长度扩容到10
2、如果是不是第一次添加，那么如果当有效个数size+1大于数组的长度那么就需要进行扩容
3、每次扩容会扩容数组的一半(1.5倍)
add(index,Element):
1、先判断下标是否在范围之内2、先判断是否需要扩容
3、将原数组的元素从index开始向后一个位置进行拷贝4、将要添加的元素添加到index位置上
get方法:
1、先判断下标是否在范围之内
2、直接返回数组中下标位置对应的元素
````


### 3. ArrayCopy截取,subList截取

截取元素

```java
int[] arr1 = {1, 2, 3, 4, 5, 6};
int[] arr2 = {10, 11, 12};
//截取数组元素
int[] arr3 = Arrays.copyOf(arr1, 4);//[1,2,3,4]
int[] arr4 = Arrays.copyOfRange(arr1, 2, 5);//[3,4,5]

//截取集合中指定下标开始到结束位置上的元素
List<String> list = list.subList(2, 5);
```

### 4. System.arraycopy拷贝

````java
// 参数1：从哪个数组拷贝出来
// 参数2：从原先这个数组的第几个位置开始拷贝
// 参数3：拷贝到哪里去
// 参数4：拷贝的元素放到目标数组里面，是从第几个位置开始放置
// 参数5：一共需要拷贝多少元素
System.arraycopy(data, index + 1, data, index, (size - index - 1));
````

## 四. LinkedList

### 1. LinkedList的特点

```java
// LinkedList 是一个基于Node（节点）来实现的虚拟容器（没有具体的边界），每一个节点都会从"前"和"后"两个方向记住临近节点的信息
// 双向链表
// 链表由两个部分组成:数据域,指针域
// 优点：
// 1、随机访问的速度比较慢，但是随机插入、删除的速度快
```

### 2. LinkedList与ArrayList查询速度比较

```java
static int count = 100_000;
static void testArrayList() {
    List<Integer> list = new ArrayList<>();
    long t1 = System.currentTimeMillis();
    for (int i = 0; i < count; i++) {
        list.add(0, i);
    }
    long t2 = System.currentTimeMillis();
    System.out.println("ArrayList :" + (t2 - t1));
}

static void testLinkedList() {
    LinkedList<Integer> list = new LinkedList<>();
    long t1 = System.currentTimeMillis();
    for (int i = 0; i < count; i++) {
        list.add(0, i);
    }
    long t2 = System.currentTimeMillis();
    System.out.println("LinkedList：" + (t2 - t1));
}
```

## 五.HashMap

### 1. HashMap的特点

```java
// Map
// 1、基于键值对(key-value)的数据结构
// 2、它的key是不能重复的，value是可以重复的
// 3、元素的排列顺序是无法得到保障的
//HashMap
// 1、设置初始容量为 16
// 2、根据键的 HashCode 值存储数据，具有很快的访问速度
// 3、HashMap 继承于AbstractMap
```

### 2. 创建方式,插入数据的小特点

```java
Map<String, Student> map = new HashMap<>();
//插入数据
map.put("a2", new Student("Jack", 20));
map.put("3_", new Student("Cool", 40));
//在原来键位置插入则会覆盖原来的数据
//但是可以返回原来的数据
old = map.put("3_", new Student("Tom", 6));
```

### 3. 获取所有的key和value

```java
Set<String> keys = map.keySet();
for (String key: keys) {
    Student value = map.get(key);
    System.out.println(key + "-" + value);
}
```

## 六.HashSet

### 1. 基本使用

常⽤⽅法与Collection接⼝中定义的⽅法⼀致 

特点:

⽆序 （插⼊顺序） 

⽆下标 

**不可重复**

### 2. HashSet去重原理

````java
HashSet底层去重： 

⾸先会⽐较两个对象的hashCode的值，如果hashCode值不⼀样，则直接认为两个对象是不同的对象，如果 HashCode值⼀样，那么就会⽐较两个⽅法的equals⽅法， 如果equals⽅法返回false，则表⽰两个对象是不同的对象，如果equals⽅法返回true，则表⽰两个对象是相同的对象，则不会向HashSet中添加 

总之：HashSet确定对象是否重复，是先判断hashcode再判断equals，两者都相等则认为是相同对象

````




