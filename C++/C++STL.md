# priority_queue 优先队列
- priority_queue<Type,Container,Functional>
    - Type:数数类型
    - Container：容器类型 必须是用数组实现的容器 vector deque等
    - Functional：比较方式 仿函数实现自定义比较方式
## 升序队列
`priority_queue <int,vector<int>,greater<int> > q;`

## 降序队列
`priority_queue <int,vector<int>,less<int> >q;`

>greater和less是std实现的两个仿函数（就是使一个类的使用看上去像一个函数。其实现就是类中实现一个operator()，这个类就有了类似函数的行为，就是一个仿函数类了）

## 自定义数据结构
`priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> busy;`

```c++
//方法1可以重载运算符
struct tmp1 //运算符重载<
{
    int x;
    tmp1(int a) {x = a;}
    bool operator<(const tmp1& a) const
    {
        return x < a.x; //大顶堆
    }
};
//方法2重写仿函数
    struct tmp2 
    {
        bool operator() (tmp1 a, tmp1 b) 
        {
            return a.x < b.x; //大顶堆
        }
    };
```

# Deque  双端队列
- 头文件：#include<deque>
- deque 是 double-ended queue 的缩写，又称双端队列容器。
- 和 vector 相比，额外增加了实现在容器头部添加和删除元素的成员函数(所耗费时间为O(1))，同时删除了 capacity()、reserve() 和 data() 成员函数。
```c++
deque<int> a;
a.push_front(1);
a.push_back(2);
a.pop_front();
a.pop_back();
```





