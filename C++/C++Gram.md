# 类型转换
1.  **int转string**
	- c++11标准增加了全局函数std::to_string:
    ```c++
    String to_string(int temp);
    int c=110;
    string d=to_string(c);
    ```
2. **string转int**
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
3. **Char[]转int**
	- 使用 std::atoi
	```c++
    char * d="110";
	b1=atoi(d);
    ```
4. **int转char（不能转负数!）**
	```C++
    int b=3;
	char c='0'+b;
    ```
5. **char转int**
    ```c++
	char c='2';
	int b=c-'0';
    ```
6. **char*和char[]之间拷贝**
    ```C++
    char* strcpy(char* strDestination, const char* strSource);  
    //后复制到前
    ```
# String
1. 截取字符串 
    ```c++
    substr(int start,int length);
    //缺省长度的情况下是将到结束的全部复制过来  
    ```  
2. 删除一个字符
    ```c++
    erase (iterator p);//参数时迭代器
    ```
3. 找第一个某字符出现的位置
    ```c++
    int i=a.find_first_of(' ');
    ```
4. 判断一个字符是不是数字
    ```c++
    bool c=isdigit(log2[pos]);
    ```
# 易错
1. 运算符优先级
    - & 逻辑与，^ 逻辑异或，| 逻辑或 的优先级低于==  
	在括号判断时，一定要加括号
    ```c++
	 if((n&1)==aim)
    ```
    
# C++文件流
```c++
#include<fstream>
//读文件
ifstream infile;
infile.open(StrFile, ios::in | ios::binary);//读文件，以二进制形式
if (infile.is_open())//判断是否打开成功
    infile.read((char*)&strHead, sizeof(tagBITMAPFILEHEADER));
infile.seekg(strHead.bfOffBits, ios::beg);//读文件指针跳跃
//写文件
ofstream outfile;
outfile.open(ComFile, ios::out | ios::binary);
if (outfile.is_open())
    outfile.write((char*)&strHead, sizeof(tagBITMAPFILEHEADER));
outfile.seekp(strHead.bfOffBits, ios::beg);//写文件指针跳跃

```