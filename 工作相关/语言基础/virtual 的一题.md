![virtual](E:\工作相关\leetcode\img\virtual.jpg)

输出为：

> ~classB
>
> ~classA
>
> ~classB
>
> ~classA
>
> ~classA

只有在基类指针指向派生类而析构函数未进行virtual声明时才会产生静态绑定为定义的类类型，继而导致内存泄露。