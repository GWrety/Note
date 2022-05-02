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


