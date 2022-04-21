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