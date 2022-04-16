# strcpy

要考虑两种情况，一种是内存重叠的情况，即改变 dest 也会改变未复制的 src，这也会导致'\0'的复制可能失败，进而出现复制错误。

## 代码

```c++
#include <cassert>
#include <cstdio>

//normal edition
char* w_strcpy(char* dest, const char* src)
{
    assert(nullptr != dest && nullptr != src);
    char* ret = dest;
    while(((*dest++) = (*src++)) != '\0');
    return ret;
}

//memroy coincidence edition
char* w_memcpy(char* dest, const char* src, int src_length)
{
    assert(nullptr != dest && nullptr != src);
    char* ret = dest;

    //if exist memory coincidence, use src_length, copying back to front.
    //if dest == src + src_length, dest's first address is src's memory address where storage '\0'.
    if( (dest > src) && (dest <= src + src_length))
    {
        int tmp_length = src_length;
        while(0 <= tmp_length)
        {
            *(dest + tmp_length) = *(src + tmp_length);
            --tmp_length;
        }
    }
    else
    {
        return w_strcpy(dest, src);
    }
    return ret;
}

int main()
{
    char ch_1[6];
    char ch_2[7] = "hello";
    printf("%s", w_memcpy(ch_2, ch_2, 5));
    printf("%s", ch_2);
    return 0;
}
```



## assert

 assert是**运行期断言**，它用来发现运行期间的错误，不能提前到编译期发现错误，也不具有强制性，也**谈不上改善编译信息的可读性，既然是运行期检查，对性能当然是有影响的**，所以经常在发行版本中，assert都会被关掉；

```c++
函数原型：
#include<assert.h>
void assert(int expression);
```

assert是运行期的判断，**并且会强制终止程序**，一般要求**只能用于debug版本中，是为了尽可能快的发现问题。assert是要从release版本中去掉**。所以一般开发会重新定义assert宏。



## static_asset

**语法：static_assert（常量表达式，要提示的字符串）；**
如果第一个参数常量表达式的值为false，会产生一条编译错误，错误位置就是该static_assert语句所在行，第二个参数就是错误提示字符串。然后通过调用 abort 来终止程序运行。*

**使用static_assert优点：**

1. 可以在编译期间发现更多的错误，用编译器来强制保证一些契约，并帮助我们改善编译信息的可读性，**尤其是用于模板的时候**。

2. static_assert可以用在全局作用域中，命名空间中，类作用域中，函数作用域中，几乎可以不受限制的使用。

3. 编译器在遇到一个static_assert语句时，通常立刻将其第一个参数作为常量表达式进行演算，但如果该常量表达式依赖于某些模板参数，则延迟到模板实例化时再进行演算，这就让检查模板参数成为了可能。

4. 性能方面，由于是static_assert编译期间断言，不生成目标代码，因此static_assert不会造成任何运行期性能损失。



