在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

>/*矩阵*/
>[
>  [1,   4,  7, 11, 15],
>  [2,   5,  8, 12, 19],
>  [3,   6,  9, 16, 22],
>  [10, 13, 14, 17, 24],
>  [18, 21, 23, 26, 30]
>]

在评论区看到一句话“站在右上角看，这个矩阵其实就像是一个Binary Search Tree。”于是就有了如下答案：

```c++
bool findNumberIn2DArray(vector<vector<int>>& matrix, int target)
{
    if(matrix.empty())
    {
        return false;
    }
    int i = 0;
    int j = matrix[0].size() - 1;
    unsigned numCol = matrix[0].size();
    unsigned numRow = matrix.size();
    while(i < numRow && j < numCol && i >= 0 && j >= 0)
    {
        if(matrix[i][j] > target)
        {
            --j;
        }
        else if(matrix[i][j] < target)
        {
            ++i;
        }
        else
        {
            return true;
        }
    }
    return false;
}
```

其算法复杂度为O(n + m)，如果使用暴力算法则事件复杂度为O(n * m)。