## 题目

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

> *示例1*
>
> 输入：s = "We are happy."
> 输出："We%20are%20happy."



### 实现一

我直接使用 stl 中的内容进行，大概思路就是利用 <algorithm> 库中的 **find** 查找 ' '直到其返回结果为end，然后在循环体中使用replace + str.find完成替换。

```c++
string replaceSpace(string s) {
    while(s.find(' ') != std::string::npos)
    {
        s = s.replace(s.find(' '), 1, "%20");
    }
    return s;
}
```



### 实现二

首先计算出 space 的数量，然后对string进行扩容，再使用双指针从后往前遍历，如果左指针碰见 space 则使用右指针替换置换为 %20。

```c++
string replaceSpace(string s) {
    int spaceCount = 0;
    for(auto ch : s)
    {
        if(ch == ' ')
        {
            ++spaceCount;
        }
    }
    s.resize(s.size() + spaceCount * 2);
    /* 利用双指针，从后到前进行替换和移动，碰见空格就进行替换 */

    int i = s.size() - 1;
    int j = s.size() - spaceCount * 2 -1;

    while(j >= 0)
    {
        if(s[j] == ' ')
        {
            s[i--] = '0';
            s[i--] = '2';
            s[i] = '%';
        }
        else
        {
            s[i] = s[j];
        }
        --i;
        --j;
    }
    return s;
}
```

