# 导读

# 1.accustoming yourself to C++
## 条款1 ：view C++ as a federation of languages(四个次语言)  
1. C语言是C++的基础
2. 面向对象  object-oriented c++
3. 泛型编程  template c++
4. 库    STL
## 条款2 ：prefer consts,enums and inlines to #define（宁可以编译器代替预处理器）
### #define不被视为语言的一部分，因此在编译和追踪问题时，会造成很大的困难，如果用常量，就更加稳定，更容易追踪错误。
```c++
	//大写名称通常用于宏
	#define A 1.63 -> const double a =1.63
```
1. 在取代常量时有两种情况值得特殊说明：      
	- 第一类是定义常量指针:
    ```C++
	const int*a ; //常用这种
	int const*c; //这两种一样，都是指针指向一个const int 类型的变量；
	int b;
	int* const d=&b;//这是const指针，指针的指向在必须初始化后就不可以改变
	//所以，在替换时一般用const指针指常量
	const char* const temp="衣衫胜雪徐凤年"; 
	//但实际上，用string比用char更合宜
    ```
	- 第二类是class专属常量：
	```C++
    //为了将常量的作用域限制于class内，必须让他成为一个member，而为了保证至多有一个实体要把他定义为static成员   
	class T{
	       static const int Num=30; //常量声明式
	            .......
	};
    ```
	然而上面的Num是声明式而非定义式，通常C++要求对所使用的人任何东西提供一个定义式，但在处理class专属常量是static也是int时，需要特殊处理：  
	1. 如果不取它的地址，你可以声明并使用它们而无需提供定义式。
	2. 但是如果你要取它的地址或是编译器并不认可这种行为，你需要在实现文件中添加如下代码：
    ```C++
	const int T::i;
	//如果你的编译器不支持以上语法，即不允许static成员在其声明式中获得初值，你可以将初值放在定义式内。
	class abc{
	    static const int i; //常量声明式
	    ......
	};
	const int abc::i = 10;//常量定义式，位于实现文件内
	//但是如果你的class在编译期间需要一个class常量值，例如编译器需要知道ui数组的大小。这时你可以使用enum来弥补。
	class abc{                  
	    enum{ i = 10};//the enum hack 补偿做法
	    int ui[i];
	};
    ```
    >理论基础;一个属于枚举类型的数值可全充ints使用。    

	1. 认识enum back的理由：  
	    1. 它更像define，所有编译器都不允许它被获得地址（而const差的编译器可以获得地址）
	    2. 它是模板元编程的基础技术  
    
2. 而对于宏定义的“函数” 使用inline解决:  
    >`#define Max_F（a，b） f((a)>(b)? (a):(b))`  
	1. 虽然define定义的类似函数可以避免调用函数带来的额外开销，但像下面这种宏会有很多问题
      
        1. 首先所有的实参都必须有小括号
        2. 但即使全加了小括号也有很多问题  
	2. 而inline函数可以获得宏的效率而更可靠：  
    ```C++
	template<typename T>
	inline void Max_F(constT& a, constT& b ){
	    f(a>b?a:b);
	}
    ```
**尽量给予预处理器更长更频繁的假期**  
1. 对于单纯常量，用cnosts对象或enums替换#define;
2. 对于形似函数的宏，用inline函数替换#define
## 条款3：use const whenever possible   
### const允许你告诉编译器某些东西不可以被改动，对于这些东西，你应该尽可能的限制为const，来获得编译器的帮助。
1. const和指针：
	- 当const在*号左边，代表所指物是常量。
	- 当const在*号右边，代表指针是常量。
	```C++
	const char*a ; 
	char const*c; 
	
	char b;
	char* const d=&b;
	
	const char* const temp="岁岁平安"; 
	```
2. const和STL迭代器：  
	STL迭代器是指针为根据塑模出来，迭代器的作用就像个T*指针。
	因此也有两种迭代器：
    ```C++
	vector<int> ve;
	
	const std::vector<int>::iterator iter =ve.begin();
	*iter=5;
	++iter;//错误，iter是const
	
	std::vector<int>::const_iterator cIter=ve.begin();
	*cIter=5;//错误，*cIter是const
	cIter++;
    ```
3. const最具威力的用法是面对函数声明时的应用。  
	**通过对返回对象和传入参数的const修饰可以避免很多意外的错误**    
**const成员函数**  
   1. 将const实施于成员函数的目的，是为了确定该成员可以作用于const对象身上。这类成员函数的作用有二：  

      	1. 使class的接口容易被理解，便于识别函数的用途
      	2. 使操作“const”对象成为可能
	>两个函数只有常量性不同，可以被重载。

  	1. 对于const成员函数的const属性也有两种理解：
		1. bitwise（physical） constness  
			成员函数只有在不改变对象的任何成员变量（static除外）时，才可以说是const
			但对于修改指针所指物的函数也可以被认定为const函数
		2. logical constness  
			一个const成员函数可以修改他所处理过的对象内的某些bits，但只有在客户端侦测不出来的情况下，才得以如此。  

		**为了放宽bitwise constness的界限，利用mutable释放掉non-static成员变量的bitwise constness约束**

     1. 在cosnt和non-const成员函数中避免重复:
		![20220422224823](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220422224823.png)
		由于两个函数及其相似，我们有必要实现一个函数使用两次。
		再考虑之后，发现用const函数调用non-const函数是安全的，只需要把返回值const属性移除。  
		![20220422224839](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220422224839.png)  

**尽量把不修改的东西声明为const，可以帮助编译器侦测出错误用法。编译器强制实施bitwise constness，但编写程序时一个使用概念上的常量性。当const和nonconst成员函数代码重复时，令non-const版本调用const版本可以改善。**
## 条款4：make sure that objects are initialized defore they're uesd
### 对于一般的对象而言，需要自己保证在使用之前将他初始化。
### 对于类而言，依赖于构造函数身上：
>不要混淆赋值和初始化。
1. 对于一个单一的类   
   	比较好的做法是用列表初始化（效率更高）    
	*需要注意的是:他们的初始化顺序严格按照声明的顺序来执行，与构造函数所写的顺序无关。*
2. 不同编译单元内定义之non-local static对象  
   	当实际两个以上源码文件时，每一个内至少包含一个non-local static对象，那么可能在某个编译单元内的某个non-local static对象的初始化和动作使用了另一个编译单元某个non-local static对象，而这个对象可能没有被初始化。    
	*为了解决这种问题，需要将每个non-local static 对象搬到自己的专属函数里（该对象在此函数里声明为static），返回这个对象的引用，换句话说，non-local static对象被local对象给替换掉了。*  

	>但这种函数内含static对象，使他们在多线程系统中带有不确定性，处理这个麻烦的一种做法是:在程序的单线程启动阶段手工调用所有的reference-returnning函数，。消除与初始化有关的“竞速形势”。  
**为内置类型手动初始化。使用成员初值列初始化类成员。用local static替换non-local static，来免除跨编译单元之初始化次序的问题**
