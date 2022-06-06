# 题目

> 一个整型数组 nums 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。
>
>  
>
> 示例 1：
>
> 输入：nums = [4,1,4,6]
> 输出：[1,6] 或 [6,1]
> 示例 2：
>
> 输入：nums = [1,2,10,4,1,4,3,3]
> 输出：[2,10] 或 [10,2]



# 解答

思路：若有一个不重复的数，则直接使用一个数累计异或得出的结果就是这个不重复的数；若有两个不重复的数，则这两个数的二进制表示形式必有某一位是不同的（使用整体异或结果找出第一个为1那一位就是他们的一个不同位），因此使用该位作为区分即可将数分为各有一个不重复数的数组。

```c++
vector<int> singleNumbers(vector<int>& nums) {
    vector<int> vecRet;
    int xorResult = 0;
    for(auto num : nums)
    {
        xorResult ^= num;
    }
    int idx = 1;
    while(xorResult % 2 == 0)
    {
        xorResult = xorResult >> 1;
        idx = idx << 1;
    }
    int xorZero = 0;
    int xorOne = 0;
    for(auto num : nums)
    {
        if((num ^ idx) < num)
        {
            xorOne ^= num;
        }
        if((num ^ idx) > num)
        {
            xorZero ^= num;
        }
    }
    vecRet.push_back(xorOne);
    vecRet.push_back(xorZero);
    return vecRet;
}
```

