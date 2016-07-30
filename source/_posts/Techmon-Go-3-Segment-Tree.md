---
title: 'Data Structure & Algorithms Notes: Segment Tree'
date: 2016-07-17 23:21:47
tags: 
- Data Structure & Algorithms
- Segment Tree
---

## 1. Segment Tree Definition
In computer science, a segment tree is a tree data structure for storing intervals, or segments. It allows querying which of the stored segments contain a given point.

![Illustration of Segment tree](/content/images/2016/illustrationOfSegmentTree.png)

Segment tree could be implemented using either an array or a tree. For an array implementation, if the element at index i is not a leaf, its left and right child are stored at index 2i and 2i+1 respectively. 


## 2. Segment Tree Problems
### 2.1. Range Sum Query  - Mutable
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.

**Example:**
```
Given nums = [1, 3, 5]
sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```

This is a classic segment tree problem, and we can break it down to the three following steps:
1. Build the segment tree;
2. Update the segment tree when an element is modified;
3. Calculate the range sum query using the segment tree.

#### 2.1.1. Build segment tree
Here, we use array implementation as example:
```java
int[] tree;
int n;
public NumArray(int[] nums) {
    if (nums.length > 0) {
        n = nums.length;
        tree = new int[n * 2];
        buildTree(nums);
    }
}
private void buildTree(int[] nums) {
    for (int i = n, j = 0;  i < 2 * n; i++,  j++)
        tree[i] = nums[j]; //Give values for the leaf nodes.
    for (int i = n - 1; i > 0; --i)
        tree[i] = tree[i * 2] + tree[i * 2 + 1]; //Update the parents' value with a bottom-up approach.
}

```
**Complexity Analysis:**
The total amount of nodes is:
n + n/2 + n/4 + n/8 + ... + 1 ~= 2n
- Time complexity: O(n)
- Space complexity: O(n)

#### 2.1.2. Update segment tree
When updating the array at i, we need to rebuild the segment tree as well. Here, we use a bottom-up approach. 
```java
void update(int pos, int val) {
    pos += n;
    tree[pos] = val;
    while (pos > 0) {
        int left = pos;
        int right = pos;
        if (pos % 2 == 0) { // pos tands for left node.
            right = pos + 1; 
        } else { // pos stands for right node.
            left = pos - 1;
        }
        // parent is updated after child is updated
        tree[pos / 2] = tree[left] + tree[right];
        pos /= 2;
    }
}
```

**Complexity Analysis**
- Time Complexity: O(log n);
- Space complexity: O(1);

#### 2.1.3. Range Sum Query
- Loop till l <= r
    + Check if l is right child of its parent P
        * l is right child of P. Then P contains sum of range of l and another child which is outside the range and we dont't need parent P sum. Add l to sum without its parent and set l to the next node on the same level.
        * l is not right child of P. Then parent P contains sum of range which lies in [l, r]. Add P to sum and set l to point to the parent of P
    + Check if r is left child of its parent P
        * r is left child of P: Then P contains sum of range of r and another child which is out side the range and we don't need parent P sum. Add r to sum without its parent and set r to the previous node on the same level
        * r is not left child of P. Then parent P contains sum of range which lies in [l, r]. Add P to sum and set r to point to the parent of P.

**Drawing a graph by yourself will help a lot!**

Here's the code.
```java
public int sumRange(int l, int r) {
    // get leaf with value 'l'
    l += n;
    // get leaf with value 'r'
    r += n;
    int sum = 0;
    while (l <= r) {
        if ((l % 2) == 1) {
           sum += tree[l];
           l++;
        }
        if ((r % 2) == 0) {
           sum += tree[r];
           r--;
        }
        l /= 2;
        r /= 2;
    }
    return sum;
}
```

**Complexity Analysis**
- Time complexity: O(log n)
- Space complexity: O(1)

### 2.2. Range Sum Query 2D
`TODO`

### 2.3. The Skyline Problem
Suppose you are given the locations and height of all the buildings as shown on a cityscape photo (Figure A), write a program to output the skyline formed by these buildings collectively (Figure B).
![Illustration of the Skyline Problem ](/content/images/2016/skylineProblem.png)

For instance, the dimensions of all buildings in Figure A are recorded as:
 `[[2 9 10], [3 7 15], [5 12 12], [15 20 10], [19 24 8]]`

The skyline in Figure B should be represented as:
`[[2 10], [3 15], [7 12], [12 0], [15 10], [20 8], [24, 0]]`.

#### 2.3.1. Solution without segment tree
The idea is very straightforward and can be divided into the following 4 steps:
1. Create a list of all the nodes that sorted by the position in x axis;
2. Create a height array with the size of all nodes, and map the position in x axis to the array index;
3. Iterate all the buildings and update the height values in array.
4. Iterate the array and generate the final result.

Here's the complet code.

```java
public class Solution {
    public List<int[]> getSkyline(int[][] buildings) {
        List<int[]> res = new ArrayList<int[]>();
        if (buildings == null || buildings.length == 0) {
            return res;
        }

        //Step1: create a list of all nodes;
        Set<Integer> nodesSet = new HashSet<Integer>();
        for (int[] building : buildings) {
            nodesSet.add(building[0]);
            nodesSet.add(building[1]);
        }
        List<Integer> nodes = new ArrayList<Integer>(nodesSet);
        Collections.sort(nodes);

        //Step2: put all nodes into an array, and build hashmap to map the x axis position to the index in array.
        int nodesLen = nodes.size();
        int[] nodesHeight = new int [nodesLen];
        Map<Integer, Integer> nodesMap = new HashMap<Integer, Integer>();
        for (int i = 0; i < nodesLen; i++) {
            nodesMap.put(nodes.get(i), i);
        }

        //Step3: update the array
        for (int[] building : buildings) {
            int startIndex = nodesMap.get(building[0]);
            int endIndex = nodesMap.get(building[1]);
            int height = building[2];
            for (int j = startIndex; j < endIndex; j++) {
                nodesHeight[j] = Math.max(nodesHeight[j], height);
            }
        }
        //Step4: generate the result.
        for (int i = 0; i < nodesLen ; i++) {
            if (i > 0 && nodesHeight[i] == nodesHeight[i - 1]) {
                continue;
            }
            int[] r = new int[2];
            r[0] = nodes.get(i);
            r[1] = nodesHeight[i];
            res.add(r);
        }
        return res;
    }
}
```



#### 2.3.2 Solution with segment tree

Do we have better solution? Yes! Now we are going to use the segment tree approach to solve it.

In this case, since more than one value needs to be saved for each node: height, start and end, so it's better to use the tree node implementation instead of the array implementation.

Comparing wiht the solution without segment tree, when we update the nodes' height values, if we reach a tree node with an equal or higher height values, we can just ignore this building and continue to the next one. This makes the solution more efficient.

```java
public class Solution {
    public class TreeNode {
        int start; //Inclusive
        int end; //Exclusive
        int height;
        TreeNode left;
        TreeNode right;
        public TreeNode (int start, int end) {
            this.start = start;
            this.end = end;
        }
    }

    public List<int[]> getSkyline(int[][] buildings) {
        List<int[]> res = new ArrayList<int[]>();
        if (buildings == null || buildings.length == 0) {
            return res;
        }

        //Step1: create a list of all nodes;
        Set<Integer> nodesSet = new HashSet<Integer>();
        for (int[] building : buildings) {
            nodesSet.add(building[0]);
            nodesSet.add(building[1]);
        }
        List<Integer> nodes = new ArrayList<Integer>(nodesSet);
        Collections.sort(nodes);

        //Step2: put all nodes into an array, and build hashmap to map the(x position, index in array
        int nodesLen = nodes.size();
        Map<Integer, Integer> nodesMap = new HashMap<Integer, Integer>();
        for (int i = 0; i < nodesLen; i++) {
            nodesMap.put(nodes.get(i), i);
        }

        //Step3: build the segment tree
        TreeNode root = buildTree(0, nodesLen - 1);

        //Step4: update the height value
        for (int[] building : buildings) {
            int startIndex = nodesMap.get(building[0]);
            int endIndex = nodesMap.get(building[1]);
            int height = building[2];
            updateHeight(startIndex, endIndex, height, root);
        }

        //Step5: generate the result.
        generateResult(res, root, nodes);
        if (nodes.size() > 0) {
            int[] last = new int[2];
            last[0] = nodes.get(nodes.size() - 1);
            last[1] = 0;
            res.add(last);
        }
        return res;
    }

    private TreeNode buildTree (int start, int end) {
        if (start >= end) {
            return null;
        }
        TreeNode node = new TreeNode (start, end);
        if (start + 1 < end) {
            int mid = start + (end - start) / 2;
            node.left = buildTree(start, mid);
            node.right = buildTree(mid, end);
        }
        return node;
    }

    private void updateHeight (int start, int end, int height, TreeNode node) {
        if (node == null || start >= node.end || end <= node.start || height <= node.height) {
            return;
        }
        if (node.left == null && node.right == null) {
            node.height = height;
        } else {
            //We don't need to change the start and end value, just the same.
            updateHeight (start, end, height, node.left);
            updateHeight (start, end, height, node.right);
            int leftHeight = (node.left == null) ? 0 : node.left.height;
            int rightHeight = (node.right == null) ? 0 : node.right.height;
            node.height = Math.min(leftHeight, rightHeight);
        }
    }

    private void generateResult (List<int[]> res, TreeNode root, List<Integer> nodes) {
        if (root == null) {
            return;
        }

        //We only need the value from the leaf nodes
        if (root.left == null && root.right == null && (res.size() == 0 || res.get(res.size() - 1)[1] !=  root.height)) {
            int[] r = new int[2];
            r[0] = nodes.get(root.start);
            r[1] = root.height;
            res.add(r);
        } else {
            generateResult(res, root.left, nodes);
            generateResult(res, root.right, nodes);
        }
    }
}
```

### 2.4. Count of Smaller Numbers After Self
`TODO`












