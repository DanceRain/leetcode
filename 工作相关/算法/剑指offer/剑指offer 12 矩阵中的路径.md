## 矩阵中的路径

> 示例 1：
>
> 输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
> 输出：true
> 示例 2：
>
> 输入：board = [["a","b"],["c","d"]], word = "abcd"
> 输出：false

```c++
class Solution {
public:
    bool dfs(const vector<vector<char>>& board, vector<vector<bool>>& IsVisitedMatrix, const string& word, int pos, int boardX, int boardY)
    {
        if(boardX < 0 || boardX >= board[0].size() || boardY < 0 || boardY >= board.size())
        {
            return false;
        }
        if(IsVisitedMatrix[boardY][boardX])
        {
            return false;
        }
        if(board[boardY][boardX] != word[pos])
        {
            return false;
        }
        if(pos == word.size() - 1)
        {
            return true;
        }
        IsVisitedMatrix[boardY][boardX] = true;
        bool ret = dfs(board, IsVisitedMatrix, word, pos + 1, boardX + 1, boardY) ||
                dfs(board, IsVisitedMatrix, word, pos + 1, boardX, boardY + 1) ||
                dfs(board, IsVisitedMatrix, word, pos + 1, boardX - 1, boardY) ||
                dfs(board, IsVisitedMatrix, word, pos + 1, boardX, boardY - 1);
        IsVisitedMatrix[boardY][boardX] = false;
        return ret;
    }
```

DFS遍历，使用 IsVisitedMatrix 矩阵记录矩阵状态，使用if完成剪枝。