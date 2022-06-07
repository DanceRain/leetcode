# 题目

> 字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。
>
>  
>
> 示例 1：
>
> 输入: s = "abcdefg", k = 2
> 输出: "cdefgab"
> 示例 2：
>
> 输入: s = "lrloseumgh", k = 6
> 输出: "umghlrlose"



# 实现一

使用C++ string中的方法即可完成操作，不过执行时间较高。

```c++
string reverseLeftWords(string s, int n)
{
    for(int i = 0; i < n; ++i)
    {
        s.push_back(*s.begin());
        s.erase(s.begin());
    }
    return s;
}
```



# 实现二

据说是某年408的真题解答，真实给爷整笑了，这种解答是怎么想出来的😀。

1. swap 0 到 n - 1 的字符
2. swap n 到 length - 1 的字符
3. swap 0 到 length - 1 的字符

```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        int length = s.size();
        swap_helper(s, 0, n - 1);
        swap_helper(s, n, length - 1);
        swap_helper(s, 0, length - 1);
        return s;
    }

    void swap_helper(string& s, int left, int right) {
        char tmp;
        while(left < right) {
            tmp = s[left];
            s[left] = s[right];
            s[right] = tmp;
            left++;
            right--;
        }
    }
};
```

