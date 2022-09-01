为什么官方的代码这么难理解？

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int>(n,1));
        for(int i = 1;i < m;i++)
        {
            for(int j = 1;j < n;j++)
            {
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
                
        }
        
        return dp[m-1][n-1];
    }
};
```

内存优化后：

```cs
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> pre(n,1),cur(n,1);
        for(int i = 1;i < m;i++)
        {
            for(int j = 1;j < n;j++)
            {
                cur[j] = pre[j] + cur[j - 1];
            }
            swap(pre,cur);
        }
        return pre[n-1];
    }
};
```

再进一步优化：

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> dp(n,1);
        for(int i = 1;i < m;i++)
        {
            for(int j = 1;j < n;j++)
            {
                dp[j] += dp[j-1];
            }
        }
        return dp[n-1];
    }
};
```

#### [62. 不同路径](https://leetcode.cn/problems/unique-paths/)

