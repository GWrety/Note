# 快速求解一个int的二进制有多少个1
```C++
    __builtin_popcount = int
    __builtin_popcountl = long int
    __builtin_popcountll = long long
    int wit=__builtin_popcount(x);
```
# 大小写  
1. 大写变小写、小写变大写 : 字符 ^= 32;
2. 大写变小写、小写变小写 : 字符 |= 32;
3. 小写变大写、大写变大写 : 字符 &= -33;


# lower_bound()函数
lower_bound() 函数用于在指定区域内查找不小于目标值的第一个元素。也就是说，使用该函数在指定范围内查找某个目标值时，最终查找到的不一定是和目标值相等的元素，还可能是比目标值大的元素。
```c++
//在 [first, last) 区域内查找不小于 val 的元素
ForwardIterator lower_bound (ForwardIterator first, ForwardIterator last,const T& val);
//在 [first, last) 区域内查找第一个不符合 comp 规则的元素
ForwardIterator lower_bound (ForwardIterator first, ForwardIterator last,const T& val, Compare comp);x`
```


# accumulate函数 
对数组进行求和求乘等操作
```c++
int main(int, char**) {
    vector<int> nums = { 6,3,2 };
    // 默认求和，输出为：0+6+3+2 = 11
    cout << accumulate(nums.begin(), nums.end(), 0) << endl;
    // 初始值为1求和，输出为：1+6+3+2 = 12
    cout << accumulate(nums.begin(), nums.end(), 1) << endl;
    // 求累减，输出为：0-6-3-2 = -11
    cout << accumulate(nums.begin(), nums.end(), 0, minus<int>()) << endl;
    // 求累乘，输出为：1*6*3*2 = 36
    cout << accumulate(nums.begin(), nums.end(), 1, multiplies<int>()) << endl;
    // 求累除，输出为：36/6/3/2 = 1
    cout << accumulate(nums.begin(), nums.end(), 36, divides<int>()) << endl;
    return 0;
}
```