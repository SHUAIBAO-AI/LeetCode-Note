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
### 笔记
什么是哈希表？
散列表（Hash table，也叫哈希表），是根据关键码值(Key value)而直接进行访问的数据结构。也就是说，它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度。这个映射函数叫做散列函数，存放记录的数组叫做散列表。
给定表M，存在函数f(key)，对任意给定的关键字值key，代入函数后若能得到包含该关键字的记录在表中的地址，则称表M为哈希(Hash）表，函数f(key)为哈希(Hash) 函数。
以上正式的解释摘自百度百科哈希表页面。
从这段解释中，我们理应知道的：
• 哈希表是一种数据结构
• 哈希表表示了关键码值和记录的映射关系
• 哈希表可以加快查找速度
• 任意哈希表，都满足有哈希函数f(key)，代入任意key值都可以获取包含该key值的记录在表中的地址

来自 <https://zhuanlan.zhihu.com/p/84327339> 
官方解释听过了，那么如何用大白话来解释呢？
简单的来说，哈希表是一种表结构，我们可以直接根据给定的key值计算出目标位置。在工程中这一表结构实现通常采用数组。
与普通的列表不同的地方在于，普通列表仅能通过下标来获取目标位置的值，而哈希表可以根据给定的key计算得到目标位置的值。
在列表查找中，使用最广泛的二分查找算法，复杂度为O(log2n)，但其始终只能用于有序列表。普通无序列表只能采用遍历查找，复杂度为O(n)。
而拥有较为理想的哈希函数实现的哈希表，对其任意元素的查找速度始终为常数级，即O(1)。

来自 <https://zhuanlan.zhihu.com/p/84327339> 


问题
Hash映射函数主要为取余函数
取余函数会导致可能有不同的数被映射到相同的位置上，比如523和23取余，都会映射到23这个位置上
解决方案：线性探测，拉链法

让我们回忆一下数据结构课程上的内容，当数据量比较大而且内存无法装下的时候，我们可以采用外排序的方法来进行排序，这里我们可以采用归并排序，因为归并排序有一个比较好的时间复杂度O(NlgN)。


外排序（External sorting）是指能够处理极大量数据的排序算法。通常来说，外排序处理的数据不能一次装入内存，只能放在读写较慢的外存储器（通常是硬盘）上。外排序通常采用的是一种“排序-归并”的策略。在排序阶段，先读入能放在内存中的数据量，将其排序输出到一个临时文件，依此进行，将待排序数据组织为多个有序的临时文件。而后在归并阶段将这些临时文件组合为一个大的有序文件，也即排序结果。


## 题目2
两数相加

给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例 1：

输入：l1 = [2,4,3], l2 = [5,6,4]

输出：[7,0,8]

解释：342 + 465 = 807.

提示：

每个链表中的节点数在范围 [1, 100] 内

0 <= Node.val <= 9

题目数据保证列表表示的数字不含前导零

### 思路：
方法：

由于输入的两个链表都是逆序存储数字的位数的，因此两个链表中同一位置的数字可以直接相加。

我们同时遍历两个链表，逐位计算它们的和，并与当前位置的进位值相加。具体而言，如果当前两个链表处相应位置的数字为 n1,n2n1,n2，进位值为carry，则它们的和为 n1+n2+carry；其中，答案链表处相应位置的数字为 (n1+n2+carry)mod10，而新的进位值为(n1+n2+carry)/10。

如果两个链表的长度不同，则可以认为长度短的链表的后面有若干个0。

此外，如果链表遍历结束后，有carry>0，还需要在答案链表的后面附加一个节点，节点的值为carry。

复杂度分析

时间复杂度：O(max(m,n))，其中 m 和 n 分别为两个链表的长度。我们要遍历两个链表的全部位置，而处理每个位置只需要 O(1) 的时间。

空间复杂度：O(1)。注意返回值不计入空间复杂度。

方法代码如下：
```Python
class Solution:
    def addTwoNumbers(self, l1, l2):
        head = curr = ListNode()
        carry = val = 0

        while carry or l1 or l2:
            val = carry

            if l1: l1, val = l1.next, l1.val + val
            if l2: l2, val = l2.next, l2.val + val

            carry, val = divmod(val, 10)
            curr.next = curr = ListNode(val)
        
        return head.next
```
### 笔记
链表是一种物理存储单元上非连续、非顺序的存储结构，数据元素的逻辑顺序是通过链表中的指针链接次序实现的。 链表由一系列结点（链表中每一个元素称为结点）组成，结点可以在运行时动态生成。 每个结点包括两个部分：一个是存储数据元素的数据域，另一个是存储下一个结点地址的指针域。 相比于线性表顺序结构，操作复杂。

比如，我们在数据集里面的一个表格，在展示上是连续的，有顺序的，但是在硬盘上是不连续的，没有顺序的
链表最显著的特征是：分散
链表中每个数据在储存中，都会有一个指针指向它的直接后继元素，也就是说，物理上的每个数据单元，都会在结尾有指针指向逻辑上的下一个元素
这样，这些由指针相连的数据直接就有了线性的关联

链表中数据的构成与概念

链表的数据有两部分：数据+指针
这个结构称为结点

n个结点通过指针相连
整个链表第一个结点称为首元结点
首元结点之前会有一个空结点，一般没数据，但是有时候也会有链表长度信息，这个空结点可有可无
链表也有增删查改的功能
删除B结点，假设数据为ABCD：此时我们要将A结点的指针直接指向C，尔后再释放掉B结点（一定要释放），然后就删掉了B结点
如果不释放B结点的数据，会造成内存泄漏
添加B结点，假设数据为ACD：此时我们要将A结点的指针指向B结点，B结点新增指针指向C结点

数组与链表的区别与优劣：
数组：
必须首先指定元素个数（定义长度），分配固定大小的空间，不能根据情况动态调整
数组从栈中分配空间，关于内存的申请与释放，都由系统完成，比较方便，但是自由度小
数组的插入与删除，都需要移动其后所有的元素，数组的效率低于链表
访问上，数组的内存是连续的，直接用下标访问数组元素，效率高于链表

链表：
不必指定元素个数，可以动态根据内存分配，很方便进行增减
链表从堆中分配空间，用多少就开多少内存，内存申请管理麻烦，但是自由度大
链表插入与删除，只需要修改指针，不需要移动节点，链表的效率高于数组
访问上，链表的内存是离散的，访问链表结点时，要从头结点开始查找，效率低于数组


结论是：
快速访加上少删插时，用数组
正常访问加多删插时，用链表
![image](https://user-images.githubusercontent.com/12431790/161229497-b5cc160a-cf5d-4ea4-9971-1970bc5bda15.png)



## 题目3
无重复字符的最长子串

给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:

输入: s = "abcabcbb"

输出: 3 

解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

示例 2:

输入: s = "bbbbb"

输出: 1

解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

示例 3:

输入: s = "pwwkew"

输出: 3

解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
 

提示：
0 <= s.length <= 5 * 104

s 由英文字母、数字、符号和空格组成

### 思路：
滑动窗口

思路和算法

我们先用一个例子考虑如何在较优的时间复杂度内通过本题。

我们不妨以示例一中的字符串abcabcbb 为例，找出从每一个字符开始的，不包含重复字符的最长子串，那么其中最长的那个字符串即为答案。对于示例一中的字符串，我们列举出这些结果，其中括号中表示选中的字符以及最长的字符串：

以 \texttt{(a)bcabcbb}(a)bcabcbb 开始的最长字符串为 \texttt{(abc)abcbb}(abc)abcbb；

以 \texttt{a(b)cabcbb}a(b)cabcbb 开始的最长字符串为 \texttt{a(bca)bcbb}a(bca)bcbb；

以 \texttt{ab(c)abcbb}ab(c)abcbb 开始的最长字符串为 \texttt{ab(cab)cbb}ab(cab)cbb；

以 \texttt{abc(a)bcbb}abc(a)bcbb 开始的最长字符串为 \texttt{abc(abc)bb}abc(abc)bb；

以 \texttt{abca(b)cbb}abca(b)cbb 开始的最长字符串为 \texttt{abca(bc)bb}abca(bc)bb；

以 \texttt{abcab(c)bb}abcab(c)bb 开始的最长字符串为 \texttt{abcab(cb)b}abcab(cb)b；

以 \texttt{abcabc(b)b}abcabc(b)b 开始的最长字符串为 \texttt{abcabc(b)b}abcabc(b)b；

以 \texttt{abcabcb(b)}abcabcb(b) 开始的最长字符串为 \texttt{abcabcb(b)}abcabcb(b)。

发现了什么？如果我们依次递增地枚举子串的起始位置，那么子串的结束位置也是递增的！这里的原因在于，假设我们选择字符串中的第k个字符作为起始位置，并且得到了不包含重复字符的最长子串的结束位置为 r_k。那么当我们选择第 k+1 个字符作为起始位置时，首先从 k+1 到 r_k 的字符显然是不重复的，并且由于少了原本的第 k 个字符，我们可以尝试继续增大 r_k ，直到右侧出现了重复字符为止。

这样一来，我们就可以使用「滑动窗口」来解决这个问题了：

我们使用两个指针表示字符串中的某个子串（或窗口）的左右边界，其中左指针代表着上文中「枚举子串的起始位置」，而右指针即为上文中的 r_k；

在每一步的操作中，我们会将左指针向右移动一格，表示 我们开始枚举下一个字符作为起始位置，然后我们可以不断地向右移动右指针，但需要保证这两个指针对应的子串中没有重复的字符。在移动结束后，这个子串就对应着 以左指针开始的，不包含重复字符的最长子串。我们记录下这个子串的长度；

在枚举结束后，我们找到的最长的子串的长度即为答案。

判断重复字符

在上面的流程中，我们还需要使用一种数据结构来判断 是否有重复的字符，常用的数据结构为哈希集合（即 C++ 中的 std::unordered_set，Java 中的 HashSet，Python 中的 set, JavaScript 中的 Set）。在左指针向右移动的时候，我们从哈希集合中移除一个字符，在右指针向右移动的时候，我们往哈希集合中添加一个字符。

至此，我们就完美解决了本题。

方法：
方法代码如下：
```Python
class Solution:
    def lengthOfLongestSubstring(self, s):
        # 哈希集合，记录每个字符是否出现过
        occ = set()
        n = len(s)
        # 右指针，初始值为 -1，相当于我们在字符串的左边界的左侧，还没有开始移动
        rk, ans = -1, 0
        for i in range(n):
            if i != 0:
                # 左指针向右移动一格，移除一个字符
                occ.remove(s[i - 1])
            while rk + 1 < n and s[rk + 1] not in occ:
                # 不断地移动右指针
                occ.add(s[rk + 1])
                rk += 1
            # 第 i 到 rk 个字符是一个极长的无重复字符子串
            ans = max(ans, rk - i + 1)
        return ans
```
### 笔记

子序列是什么？
一个字符串的 子序列 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。 例如， "ace" 是 "abcde" 的子序列，但 "aec" 不是 "abcde" 的子序列。


## 题目4
寻找两个正序数组的中位数

给定两个大小分别为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的 中位数 。

算法的时间复杂度应该为 O(log (m+n)) 。


示例 1：

输入：nums1 = [1,3], nums2 = [2]

输出：2.00000

解释：合并数组 = [1,2,3] ，中位数 2

示例 2：

输入：nums1 = [1,2], nums2 = [3,4]

输出：2.50000

解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
 
提示：

nums1.length == m

nums2.length == n

0 <= m <= 1000

0 <= n <= 1000

1 <= m + n <= 2000

-10^6 <= nums1[i], nums2[i] <= 10^6

### 思路：
这道题让我们求两个有序数组的中位数，而且限制了时间复杂度为O(log (m+n))，看到这个时间复杂度，自然而然的想到了应该使用二分查找法来求解。那么回顾一下中位数的定义，如果某个有序数组长度是奇数，那么其中位数就是最中间那个，如果是偶数，那么就是最中间两个数字的平均值。这里对于两个有序数组也是一样的，假设两个有序数组的长度分别为m和n，由于两个数组长度之和 m+n 的奇偶不确定，因此需要分情况来讨论，对于奇数的情况，直接找到最中间的数即可，偶数的话需要求最中间两个数的平均值。为了简化代码，不分情况讨论，我们使用一个小trick，我们分别找第 (m+n+1) / 2 个，和 (m+n+2) / 2 个，然后求其平均值即可，这对奇偶数均适用。加入 m+n 为奇数的话，那么其实 (m+n+1) / 2 和 (m+n+2) / 2 的值相等，相当于两个相同的数字相加再除以2，还是其本身。

这个题目可以归结到寻找第k小(大)元素问题，思路可以总结如下：取两个数组中的第k/2个元素进行比较，如果数组1的元素小于数组2的元素，则说明数组1中的前k/2个元素不可能成为第k个元素的候选，所以将数组1中的前k/2个元素去掉，组成新数组和数组2求第k-k/2小的元素，因为我们把前k/2个元素去掉了，所以相应的k值也应该减小。另外就是注意处理一些边界条件问题，比如某一个数组可能为空或者k为1的情况。

方法：
方法代码如下：
```Python
    def findMedianSortedArrays(self, nums1, nums2):
        def findKthElement(arr1,arr2,k):
            len1,len2 = len(arr1),len(arr2)
            if len1 > len2:
                return findKthElement(arr2,arr1,k)
            if not arr1:
                return arr2[k-1]
            if k == 1:
                return min(arr1[0],arr2[0])
            i,j = min(k//2,len1)-1,min(k//2,len2)-1
            if arr1[i] > arr2[j]:
                return findKthElement(arr1,arr2[j+1:],k-j-1)
            else:
                return findKthElement(arr1[i+1:],arr2,k-i-1)
        l1,l2 = len(nums1),len(nums2)
        left,right = (l1+l2+1)//2,(l1+l2+2)//2
        return (findKthElement(nums1,nums2,left)+findKthElement(nums1,nums2,right))/2
```
### 笔记
主要思路是二分法搜索


## 题目1
### 思路：
方法：
方法代码如下：
```Python
```
### 笔记
