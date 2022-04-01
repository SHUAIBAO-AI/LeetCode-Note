# LeetCode-Note
LeetCode刷题记录与笔记

全部语言都是Python，便于理解


## 题目1
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/two-sum

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。
你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
你可以按任意顺序返回答案。

示例 1：

输入：nums = [2,7,11,15], target = 9

输出：[0,1]

解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

### 思路：

方法一：
暴力破解
用两层循环进行解题，不过提交结果后提示 “超出时间限制”，这里就不做讲解。

方法二：
用 Python 中 list 的相关函数求解
解题关键主要是想找到 num2 = target - num1，是否也在 list 中，那么就需要运用以下两个方法：

num2 in nums，返回 True 说明有戏

nums.index(num2)，查找 num2 的索引

方法三：

解题思路是在方法二的基础上，优化解法。想着，num2 的查找并不需要每次从 nums 查找一遍，只需要从 num1 位置之前或之后查找即可。但为了方便 index 这里选择从 num1 位置之前查找：

方法四：

用字典模拟哈希求解
参考了大神们的解法，通过哈希来求解，这里通过字典来模拟哈希查询的过程。
个人理解这种办法相较于方法一其实就是字典记录了 num1 和 num2 的值和位置，而省了再查找 num2 索引的步骤。

通过字典的方法，查找效率快很多，执行速度大幅缩短，共 88ms。

方法四代码如下：
```Python
def twoSum(nums, target):
    hashmap={}
    for ind,num in enumerate(nums):
        hashmap[num] = ind
    for i,num in enumerate(nums):
        j = hashmap.get(target - num)
        if j is not None and i!=j:
            return [i,j]
```

