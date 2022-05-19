## 题目

> 地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？
>

```c++
class Solution {
public:
    int count = 0;
    int col = 0;
    int row = 0;
    int max = 0;

    int movingCount(int m, int n, int k)
    {
        vector<vector<bool>> IsVisited(m, vector<bool>(n, false));
        row = m;
        col = n;
        max = k;
        dfs(IsVisited, 0, 0);
        return count;
    }

    int digitSum(int num)
    {
        int sum = 0;
        do{
            sum += num % 10;
            num /= 10;
        }while(num != 0);
        return sum;
    }

    void dfs(vector<vector<bool>>& status, int x, int y)
    {
        if(x < 0 || y < 0 || x >= col || y >= row)
        {
            return;
        }
        if(digitSum(x) + digitSum(y) > max)
        {
            return;
        }
        if(status[y][x])
        {
            return;
        }
        status[y][x] = true;
        ++count;
        dfs(status, x + 1, y);
        dfs(status, x, y + 1);
        dfs(status, x - 1, y);
        dfs(status, x, y - 1);
    }
};
```

与12题思路相似。