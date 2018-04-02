## 类和对象
### 定义方法
1.类的定义  
  修饰符 class 类名  
  {     构造器/  
        成员变量/  
        方法/}  
（1）修饰符可以是public,final,abstrcat或完全省略修饰符  
（2）static修饰的成员不能访问没有staic修饰的成员  
即静态变量不能直接访问非静态变量；  
2.成员变量的定义  
修饰符 类型 成员变量名=默认值  
（1）修饰符可以省略，也可以是Public，protected，private,static,final.其中public,protected,private三个最多只能出现一个，可以与static,final组合起来修饰；  
3.方法的而定义  
修饰符 方法返回值类型 方法名（形参列表）  
{   可执行语句}  
（1）修饰符可以省略，也可以是public,protected,private,static,final,abstract,其中,public,protected,private最多只能出现其中一个。final absract最多只能出现一个,它们可以和static组合起来修饰
4.构造器的定义  
修饰符 构造器名（形参列表）  
{   可执行语句}  
（1）修饰符可以生了，也可以是public,protected,private其中之一  
（2）构造器的名字必须与类名相同  
（3）形参列表和定义方法的形参列表的格式完全相同  
### static——特殊关键字    
1.static修饰的成员表明它属于类本身而不属于该类的单个实例。也就是说static修饰的成员不能访问非static修饰的成员  
2.而static修饰的成员可以通过类和实例来调用；  
  没有使用static的成员则只可通过实例调用。  
3.既然静态成员不能直接访问非静态成员，那么如果一定需要访问时，则只能重新创建一个对象。

        public class NonStaic
        {public void info()
        {   System.out.pintfln("鸡蛋")；}
        public static boid main(String[]arg)
        {   info();}
        }
        //因为main方法是静态方法，而info是非静态方法，因此编译错误
        //修正方法，创建一个对象作为调用者调用info方法
       //修改为 new NonStatic().info();
### 函数的传值  
函数的值传递在JAVA中和C语言存在差别  
按C语言的编程思维，例如将两个数对调  

        public calss transfer
        {   public static void swap(int a,int b)
                {int t=a;
                     a=b;
                     b=t;}
            public static void main(String[]arg)
            {   int a=6;
                int b=9;
                swap(a,b);}}
        /*在C语言中，这个程序输入的结果是a为9b为6；但在JAVA中，他的结果和原值不变；造成这样的结果是因为在JAVA中的存储方式不同；*/
在JAVA中，值传递指的是你将实际参数值的副本传入方法内，而本身的参数值不受影响。在JAVA中，main函数的参数存储在一个栈区，而swap的参数存储在另一个栈区，所以当我们将main函数的参数传给swap函数时，实际上只是给swap的形参进行赋值，最终结果并不影响main函数的栈存储区。  
  
解决这个问题，我们可以利用引用类型参数；  
当我们在main函数中定义了a,b变量后，我们可以定义一个dw变量作为引用指向她们。相当于c语言中的指针，只记住了他的地址。这样，当我们向swap传递参数的时候实际上传递的是两个a,b的地址，使得swap操作的是main函数上所指的值，最后使得函数得到正确结果

       public class transfer {
	    static int a;
	    static int b;
	    public static void swap(transfer dw)
	    {	int t=dw.a;
			dw.a=dw.b;
			dw.b=t;
	    }
	    public static void main(String[]arg)
	    {	transfer dw=new transfer();
		dw.a=6;
	    dw.b=9;
		swap(dw);
		System.out.println(+dw.a);
		System.out.println(+dw.b);
	    }
        }

### 形参个数的可变方法  
在定义方法时，在最后一个形参的类型后增加三点...则表明该形参可以接受多个参数值，而这多个参数值时以最后一个形参类型的数组传入。  
因此传递参数时，可以传入多个参数，也可以传入一个相同类型的数组  
例如

        public class Varargs
        {   public static void test(int a,String...book)
            {   //这里的book被当成数组处理
                for(String x:book)
                    {System.out.println(x);}
                Sysyem.out.println(a)}
            public static void main(String[]arg)
            {   test(5,"疯狂讲义"，“讲义”)；}
输出结果为：  
疯狂讲义  
讲义  
5
### 成员变量和局部变量的区别和联系  
成员变量指的是在类里定义的变量，这种变量还分为类变量和实例变量，类变量的作用域与这个类的生存周期一致，而实例变量则从该类的实例被创建直到系统销毁该实例为止。  
##### 访问/修改变量  
程序访问变量的语句  
实例.实例变量  
实例.类变量  
类.类变量  
  
  注意到在实例的访问中我们同样可以访问和修改类变量，需要注意的是，这种修改与类.类变量修改的结果是一样的，修改之后当实例销毁时，类变量的值将不会改变。  
  例如  
    
      class Person
        {	//定义一个实例变量
	        public int a=1;
	        //定义一个类变量
	        public static int b=2;
            }
            public class Persontest {
		    public static void main(String[] arg)
				{	System.out.println("Person的b类变量为："+Person.b);
				 	//创建person对象
				    Person p=new Person();
				    //通过Person对象引用的p访问 Person的变量
				    System.out.println("Person的a的实例变量为："+p.a);
				    System.out.println("Person的b的类变量为："+p.b);
				    //对a,b进行赋值
				    p.a=3;
				    p.b=4;
				    //再次通过引用对象访问Person的变量
				    System.out.println("person的a的实例变量为："+p.a);
				    System.out.println("PERSON的b的实例变量为："+p.b);
				    //前面通过p修改了类的b的变量值
				    System.out.println("Person的b的类变量为："+Person.b);
				    //再创建一个变量
				    Person p1=new Person();
				    //输出a,b的值
				    System.out.println("Person的b的类变量为："+p1.b);
			  	    System.out.println("Person的a的实例变量为："+p1.a);
				}
    }
      
输出结果为：  
person的a的实例变量为：3  
PERSON的b的实例变量为：4  
Person的b的类变量为：4  
Person的b的类变量为：4  
Person的a的实例变量为：1  
#### 局部变量  
1.局部变量分为形参//方法局部变量//代码块局部变量  
与成员变量不同的是，局部变量出形参外，都必须显示初始化，否则将不可以访问他们  
2.在java中，允许同一个方法不同的代码块内同名，同时也允许局部变量和成员变量同名/  
若局部变量和成员变量同名，在方法中局部变量将覆盖成员变量，若想避开这种情况则需要使用关键字this  

       public class variable {
		    String name="李刚";
		    static double price=78.0;
		    //程序的入口
		    public static void main(String[]arg)
		    {	//方法里的局部变量将覆盖成员变量
			    int price=58;
			    //直接访问price变量将输出58而不是78.0；
			    System.out.println(price);
			    //要输出78.0则要用类名限定
			    System.out.println(variable.price);
			    //运行info方法
			    new variable().info();
		    }
		    public void info()
		    {	//在方法里设置局部变量,他将覆盖成员变量
			String name="孙尚香";
			//直接访问price将输出孙尚香
			System.out.println(name);
			//要输出李刚的话，需要用this 限定变量
			System.out.println(this.name);
			
    		}
    		
运行结果：  
58  
78.0  
孙尚香  
李刚  
