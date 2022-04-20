# 类型转换
1. int转string：
	- c++11标准增加了全局函数std::to_string:
    ```c++
    String to_string(int temp);
    int c=110;
    string d=to_string(c);
    ```
2. string转int：
	- 使用std::stoi
    ```c++
    Stoi(字符串，起始位置，进制);
    //这个起始根本没用，详情见下面的解释 shit
	string a="110";
	int b=stoi(a,0,10);
	int stoi (const string& str, size_t* idx = 0, int base = 10);
    ```
>	Parses str interpreting its content as an integral number of the specified base, which is returned as an int value.
>	If idx is not a null pointer, the function also sets the value of idx to the position of the first character in str after the number.
3. Char[]转int：
	- 使用 std::atoi
	```c++
    char * d="110";
	b1=atoi(d);
    ```
4. int转char（不能转负数!）:
	```C++
    int b=3;
	char c='0'+b;
    ```
5. char转int：
    ```c++
	char c='2';
	int b=c-'0';
    ```
# String
1. 截取字符串 
    ```c++
    substr(int start,int length)  
    ```  
# 易错
1. 运算符优先级
    - & 逻辑与，^ 逻辑异或，| 逻辑或 的优先级低于==  
	在括号判断时，一定要加括号
    ```c++
	 if((n&1)==aim)
    ```

