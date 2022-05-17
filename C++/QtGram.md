# 类型转换
1. **int转QString**
    - 用Qstring::number(long,base=10);
2. **QString转int**
    - QString.toInt();
3. **带中文的char[]转QString**
   - QString::fromLocal8Bit 
4. **QString到char***
   -str.toLocal8Bit().data()

# 重绘函数
## update()和repaint()区别    
- update()会自动优化，比如在连续update时，只会在最后一次调用paintEvent()
- repaint()会立即调用重绘函数，（做出动画连续效果）

# 循环中更新GUI
```c++
QCoreApplication::processEvents(QEventLoop::AllEvents, 100);
/*
解决程序假死，避免长时间不响应
*/
```

# QDateStream
```c++
//文本的串行化，很好用
QFile file("USER");
    file.open(QIODevice::WriteOnly);
    QDataStream out(&file);
    out << users;
    out << filedetails;
//对于结构体 需要重载运算符！！！
inline QDataStream& operator>>(QDataStream& out, diskdate& i) {
    out >> i.block;
    out >> i.date;
    out >> i.next;
    return out;
};
```