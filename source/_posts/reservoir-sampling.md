---
title: 'Data Structure & Algorithms Notes: Reservoir Sampling'
date: 2016-10-09 00:34:55
tags:
- Data Structure & Algorithms
- Reservoir Sampling
---

在一个给定长度的数组中随机等概率抽取一个数据很容易，但如果面对的是长度未知的海量数据流呢？蓄水池采样(Reservoir Sampling)算法就是来解决这个问题的, 它在分析一些大数据集的时候非常有用。

## 1. 算法描述
1. 先选取数据流中的前k个元素，保存在集合A中；
2. 从第j（k + 1 <= j <= n）个元素开始，每次先以概率p = k/j选择是否让第j个元素留下。若j被选中，则从A中随机选择一个元素并用该元素j替换它；否则直接淘汰该元素；
3. 重复步骤2直到结束，最后集合A中剩下的就是保证随机抽取的k个元素。

## 2. 算法证明
算法的证明可以参照: [蓄水池抽样算法证明](http://sobuhu.com/algorithm/2012/11/01/reservoir.html)

## 3. LeetCode例题
### 3.1. Linked List Random Node 

Given a singly linked list, return a random node's value from the linked list. Each node must have the same probability of being chosen.

**Follow up:**
What if the linked list is extremely large and its length is unknown to you? Could you solve this efficiently without using extra space?

**Example:**
```
// Init a singly linked list [1,2,3].
ListNode head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
Solution solution = new Solution(head);

// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
solution.getRandom();
```
利用蓄水池采样原理，无需事先计算list长度即可求解，具体代码如下:
```java
public class Solution {
    Random r;
    ListNode head;

    public Solution(ListNode head) {
        this.r = new Random();
        this.head = head;
    }

    public int getRandom() {
        int count = 1;
        ListNode nodeVal = head;
        ListNode curr = head;
        while (curr != null) {
            if (r.nextInt(count++) == 0) {
                nodeVal = curr;
            }
            curr = curr.next;
        }
        return nodeVal.val;
    }
}
```


### 3.2. Random Pick Index
Given an array of integers with possible duplicates, randomly output the index of a given target number. You can assume that the given target number must exist in the array.

**Note:**
The array size can be very large. Solution that uses too much extra space will not pass the judge.

**Example:**
```
int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
solution.pick(3);

// pick(1) should return 0. Since in the array only nums[0] is equal to 1.
solution.pick(1);
```
若采用常规算法，我们需要用HashMap把对应的数值及所处的位置一一关联，这样则违背了题目的空间限制。使用蓄水池采样则避免了这个问题。具体代码如下：
```java
public class Solution {
    int[] nums;

    public Solution(int[] nums) {
        this.nums = nums;
    }

    public int pick(int target) {
        int index = -1;
        int count = 1;
        Random random = new Random();
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == target) {
                if (random.nextInt(count++) == 0) {
                    index = i;
                }
            }
        }
        return index;
    }
}
```