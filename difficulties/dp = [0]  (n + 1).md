## `dp = [0] * (n + 1)`

在Python中，`dp = [0] * (n + 1)` 这行代码的作用是创建一个长度为 `n + 1` 的列表，列表中的每个元素都初始化为0。这个列表用于存储动态规划问题的子问题解，称为DP数组（Dynamic Programming array）。

这里的 `n` 是问题的规模，例如在斐波那契数列问题中，`n` 表示我们想要计算的斐波那契数列的第n项。`n + 1` 是因为我们需要包括从0到n的所有子问题解，共有 `n + 1` 个子问题。

例如，如果我们想要计算斐波那契数列的第5项，那么 `n = 5`，我们需要创建一个长度为 `n + 1 = 6` 的列表，用于存储斐波那契数列的前6项（从第0项到第5项）。

创建这个列表后，我们可以使用动态规划的方法，根据状态转移方程和边界条件，计算并填充列表中的每个元素。在斐波那契数列问题中，状态转移方程为 `dp[i] = dp[i - 1] + dp[i - 2]`，边界条件为 `dp[0] = 0` 和 `dp[1] = 1`。通过迭代计算，我们可以得到斐波那契数列的第n项。