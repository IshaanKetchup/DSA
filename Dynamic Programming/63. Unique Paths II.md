## 63. Unique Paths II
```cpp
class Solution {
public:
    int helper(int i, int j, int m, int n, vector<vector<int>>& grid, vector<vector<int>>& dp){
        if(i >= m || j >= n || grid[i][j] == 1) return 0;
        if(i == m - 1 && j == n - 1) return 1;
        if(dp[i][j] != -1) return dp[i][j];
        return dp[i][j] = helper(i, j + 1, m, n, grid, dp) + helper(i + 1, j, m, n, grid, dp);
    }

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int rows = obstacleGrid.size();
        int cols = obstacleGrid[0].size();
        if(obstacleGrid[0][0] == 1 || obstacleGrid[rows - 1][cols - 1] == 1) return 0;
        vector<vector<int>> dp(rows, vector<int>(cols, -1));
        return helper(0, 0, rows, cols, obstacleGrid, dp);
    }
};
```
