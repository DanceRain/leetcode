# 移掉K位数字

给定一个以字符串表示的非负整数 num，移除这个数中的 k 位数字，使得剩下的数字最小。

注意:

num 的长度小于 10002 且 ≥ k。
num 不会包含任何前导零。
示例 1 :

```
输入: num = "1432219", k = 3
输出: "1219"
解释: 移除掉三个数字 4, 3, 和 2 形成一个新的最小的数字 1219。
```


示例 2 :

```
输入: num = "10200", k = 1
输出: "200"
解释: 移掉首位的 1 剩下的数字为 200. 注意输出不能有任何前导零。
```



### solution one

这道题目是贪心算法的应用。由于数字的大小是由**靠左边的数**决定的，因此尽可能将k位最大的数去掉。**存储结果放在栈中，从左到右遍历字符串，每次都比较栈顶和当前数的大小，若当前数小于栈顶则将其替换为栈顶，若不小于则作为后一位。

然后就是一些特殊情况，但不论怎样，需要保证k最后为0。

```c++
string removeKdigits(string num, int k) {
	stack<char> stk;
	for (auto& digit : num)
	{
		//为了使数尽可能地小，尽可能地删掉靠左边最大的k个数
		while(!stk.empty() && digit < stk.top() && k)
		{
			stk.pop();
			--k;
		}
		stk.push(digit);
	}
    
	//避免一个数或者连续相等的数出现
	while (k--)
	{
		stk.pop();
	}
    
    //还原数的正确顺序
	stack<char> tmpStk;
	while (!stk.empty())
	{
		tmpStk.push(stk.top());
		stk.pop();
	}
    
	bool judge = true;
	string newNum = "";
	while (!tmpStk.empty())
	{
		if (!(tmpStk.top() == '0' && judge == true))
		{
			judge = false;
			newNum += tmpStk.top();
		}
		tmpStk.pop();
	}
    
	return newNum == "" ? "0" : newNum;
}
```



