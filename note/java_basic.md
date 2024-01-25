# java相关内容笔记
### 基本数据类型 vs 包装类
1. 对比
    | 基本数据类型 | 包装类    |
    | ------------ | --------- |
    | int          | Integer   |
    | long         | Long      |
    | char         | Character |
    | float        | FLoat     |
    | double       | Double    |
    | boolean      | Boolean   |

2. 装箱和拆箱
   + 基本数据类型转换为包装类的过程称为装箱
   + 包装类变为基本数据类型的过程称为拆箱  
    举例：int和Integer的装箱和拆箱
        ```
        int m = 500;
        Integer obj = new Integer(m);  // 手动装箱
        int n = obj.intValue();  // 手动拆箱
        ```
3. 常用的类型转换  
    + String转int：
        ```
        int x = Integer.parseInt(str1); 
        ```  
    + int转String：
        ```
        String str1 = Integer.toString(x);
        ```  
    + String转Integer:
        ```
        Integer x = Integer.valueOf(str1);
        ```  
    + Integer转String：
        ```
        String str1=Integer.toString(x);
        ```  
        或：
        ```
        String str1=x.toString();
        ```
### 列表
1. 数组和java.util.List的区别  
    数组与c++数组性质基本一致，变量指向数组头部的内存地址，固定长度，需要时需要动态创建：
      + 初始化
        ```
        int[] list1=new int[5];
        int[] list2={1,2,3,4,5};
        int[] list3=new int[]{1,2,3,4,5};
        ```
      + 访问与修改
        ```
        list[1]=3;
        ```  
      + 长度
        ```
        int length=list1.length;
        ```  
    List是一个interface，他有很多方法接口：  
      + 初始化
        ```
        List<Integer> list1=new ArrayList<>(); 
        List<Integer> list2=new LinkedList<>(); //List内部只能是包装类不能是基本数据类型
        ```
        注意：不能用List去初始化List
      + 访问与修改
        ```
        Integer x= list1.get(index);
        list1.set(index,x);
        ```
      + 长度
      + ```
        int length=list1.size();  
        ```   
    相互转化：  
      + List转数组：
        ```
        Integer[] nums=list.toArray(list1)  //list1:List<Integer>
        ```
      + 数组转list：
        ```
        List<Integer> list1=Arrays.asList(nums) //nums:Integer[]
        ```
2. List和ArrayList，LinkedList的关系
   List是列表的接口interface，而ArrayList和LinkedList是其实现类，他们继承自List，因此在创建时大部分情况会使用：        
    ```
    List<Integer> list1=new ArrayList<>(); 
    List<Integer> list2=new LinkedList<>();
    ```
    来创建List，即创建一个实现类来赋值给List，一定要注意不能：
    ```
    List<Integer> list3=new List();
    ```
    当使用
    ```
    List<Integer> list1=new ArrayList<>();
    List<Integer> list2=new LinkedList<>();
    ```  
    就会将一个刚创建的ArrayList赋值给List，而此时list1，list2只能使用List类的所有接口  
    而若使用
    ```
    ArrayList<Integer> list1=new ArrayList<>();
    LinkedList<Integer> list2=new LinkedList<>();
    ```  
    则可以list1可以使用ArrayList实现类自己的方法，list2可以使用LinkedList实现类的方法，例如list2.removeLast(),list2.removeFirst()
3. java.util.Arrays类
    该类有很多静态方法用于操作数组：
    + List<Integer> list1=Arrays.asList(nums) //nums:Integer[]
      注意:
      asList不能应用于基本数据类型，例如int[]
      list1无法进行修改操作，例如add，remove，若要使用以下方式需要：
      List<Integer> list1=new ArrayList(Arrays.asList(nums))
    + Arrays.fill(list1,3)
      该方法将list1所有元素都设为3  
      Arrays.fill(list1,from,to,3)
      该方法将list1从from到to-1的所有元素都设为3
    + Arrays.sort(list1)
      该方法将list1升序排列
### 字符串
1. String和char
   string用双引号"",char用单引号
   相互转化：
   ```
   char[] c=str.toCharArray();  //String 转 char[]
   String str=new String(c)   //char[] 转 String
2. String常用方法
   ```
   char charAt(int index)
   boolean contains(CharSequence s)
   int indexOf(String str)
   String substring(int beginIndex, int endIndex)
   String.valueOf()
   String.format("x=%d",10)
   ```
3. StringBuffer
   ```
   StringBuffer sb=new StringBuffer();
   sb.append("a").append("b");
   String str=sb.toString();
   ```
### 队列
1. Queue <- interface 单向队列
   method: offer/add, poll/remove(出队),element/peek(队头)
2. Deque <- interface 双向队列，继承自Queue
   method: offerFirst/addFirst,offerLast/addLast,pollFirst/removefist,pollLast/removeLast,peekFirst,peekLast
   同时他有栈的接口（继承方式见图），即有：
   push,pop,peek
   ![queue](../image/java_basic_queue.png)
3. ArrayDeque 实现类，可以实现Queue和Deque，即也可以构建Deque的栈
### LinkedList
1. 存储结构：双向链表
2. 可实现:List，Deque(Stack)，Queue的接口


