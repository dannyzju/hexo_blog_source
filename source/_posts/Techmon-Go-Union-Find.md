---
title: 'Techmon Go 4: Union Find'
date: 2016-07-30 13:37:32
tags: Techmon Go, Union Find
---
## 1. Union Find Definition
In computer science, a disjoint-set data structure, also called a union–find data structure or merge–find set, is a data structure that keeps track of a set of elements partitioned into a number of disjoint (nonoverlapping) subsets. It supports two useful operations:

- Find: Determine which subset a particular element is in. Find typically returns an item from this set that serves as its "representative"; by comparing the result of two Find operations, one can determine whether two elements are in the same subset.
- Union: Join two subsets into a single subset.
![Union Find Abstractions](/content/images/2016/unionFindAbstractions.png)

![Union Find Representation](/content/images/2016/unionFindRepresentation.png)

## 2. Union Find Implementation
### 2. 1. Quick-find apporach
```java
public class QuickFindUF {
    private int[] id; // id[i] is component id for object i
    public QuickFindUF(int N) {
        id = new int[N];
        for (int i = 0; i < N; ++i) {
            id[i] = i;
        }
    }

    public boolean connected(int p, int q) {
        return id[p] == id[q];
    }

    public void union(int p, int q) {
        int pid = id[p];
        int qid = id[q];
        for (int i = 0; i < id.length; ++i) {
            if (id[i] == pid) id[i] = qid;
        }
    }
}
```
Time Complexity:
- Find: O(1)
- Unite: O(N)

`Quick-find algorithm is too slow, it may take ~MN steps to process M union commands on N objects.`

### 2.2. Quick-union approach
```java
public class QuickUnionUF {
    private int[] id; // id[i] is parent of i
    public QuickUnionUF(int N) {
        id = new int[N];
        for (int i = 0; i < N; ++i) {
            id[i] = 1;
        }
    }

    private int root(int i) {
        while (i != id[i]) {
            //id[i] = id[id[i]];
            i = id[i];
        }
        return i;
    }

    public boolean connected(int p, int q) {
        return root(p) == root(q);
    }

    public void union(int p, int q) {
        int i = root(p);
        int j = root(q);
        id[i] = j;
    }
}
```
Quick-find defect
- Union too expensive (N steps)
- Trees are flat, but too expensive to keep then flat

Quick-union defect
- Trees can get tall
- Find too expensive (could be N steps)
- Need to do find to do union

`Quick-union is also too slow`

### 2.3. Weighted quick-union with path compression

Improvement 1: Weighting
- Modify quick-union to avoid tall trees.
- Keep track of size of each component.
- Balance by linking small tree below larget one.

Analysis:
- Find: takes time proportional to depth of p and q.
- Union: takes constant time, given roots.
- Fact: depth is at most lg N. [needs proof, remember it here.]

Improvement 2: Path compression
- Just after computing the root of i, set the id of each examined node to root(i).

```java
public class UF {
    private int[] id;
    int size[];
    public UF(int N) {
        id = new int[N];
        for (int i = 0; i < N; ++i) {
            id[i] = 1;
        }
    }

    private int root(int i) {
        while (i != id[i]) {
            id[i] = id[id[i]];
            i = id[i];
        }
        return i; h
    }

    public boolean connected(int p, int q) {
        return root(p) == root(q);
    }

    public void union(int p, int q) {
        int i = root(p);
        int j = root(q);
        if (size[i] < size[j]) {
            id[i] = j;
            size[j] += size[i];
        } else {
            id[j] = i;
            size[i] += size[j];
        }
        id[i] = j;
    }
}
```

## 3. Union Find Problems
### 3.1. Number of Islands
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

***Example 1:***
```
11110
11010
11000
00000
```
Answer: 1

***Example 2:***
```
11000
11000
00100
00011
```
Answer: 3

**Solution 1: Depth First Search**
This problem can be solved with both depth-frist search and breath-first search, the following code is an example of depth-first search.
```java
public class Solution {
    public int numIslands(char[][] grid) {
        int sum = 0;
        if (grid == null) {
            return 0;
        }
        int height = grid.length;
        if (height == 0) {
            return 0;
        }
        int len = grid[0].length;

        if (len == 0) {
            return 0;
        }

        for (int i = 0; i < height; i++) {
            for (int j = 0; j < len; j++) {
                if (grid[i][j] == '1') {
                    sum++;
                    helper(grid, i, j, height, len);
                }

            }
        }
        return sum;
    }

    private void helper(char[][] grid, int i, int j, int height, int len) {
        grid[i][j] = 'x';
        if (i - 1 >= 0 && grid[i - 1][j] == '1') {
            helper(grid, i - 1, j, height, len);
        }

        if (i + 1 < height && grid[i + 1][j] == '1') {
            helper(grid, i + 1, j, height, len);
        }

        if (j - 1 >= 0 && grid[i][j - 1] == '1') {
            helper(grid, i, j - 1, height, len);
        }

        if (j + 1 < len && grid[i][j + 1] == '1') {
            helper(grid, i, j + 1, height, len);
        }
    }
}
```

**Solution 2: Union Find**

```java
public class Solution {
    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        int m = grid.length, n = grid[0].length;
        UF uf = new UF(m, n, grid);
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '0') continue;
                int p = i * n + j;
                int q;
                // check up
                if (i > 0 && grid[i - 1][j] == '1') {
                    q = p - n;
                    uf.union(p, q);
                }
                // check down
                if (i < m - 1 && grid[i + 1][j] == '1') {
                    q = p + n;
                    uf.union(p, q);
                }
                // check left
                if (j > 0 && grid[i][j - 1] == '1') {
                    q = p - 1;
                    uf.union(p, q);
                }
                // check right
                if (j < n - 1 && grid[i][j + 1] == '1') {
                    q = p + 1;
                    uf.union(p, q);
                }
            }
        }
        return uf.count;
    }

    class UF {
        int[] id;
        int[] sz;
        int count = 0;
        public UF(int m, int n, char[][] grid) {
            for (int i = 0; i < m; i++) {
                for (int j = 0; j < n; j++) {
                    // When creating the UF object, count the number of '1's.
                    if (grid[i][j] == '1') count++;
                }
            }
            id = new int[m * n];
            sz = new int[m * n];
            for (int i = 0; i < m * n; i++) {
                id[i] = i;
                sz[i] = 1;
            }
        }

        public int root(int k) {
            while (id[k] != k) {
                id[k] = id[id[k]];
                k = id[k];
            }
            return k;
        }
        public boolean connected(int p, int q) {
            return root(p) == root(q);
        }
        public void union(int p, int q) {
            int x = root(p);
            int y = root(q);
            if (x == y) return;
            if (sz[x] < sz[y]) {
                id[x] = y;
                sz[y] += sz[x];
            } else {
                id[y] = x;
                sz[x] += sz[y];
            }
            // Whenever do a union, reduce count by 1.
            count--;
        }
    }
}
```




### 3.2. Number of Islands II 
A 2d grid map of m rows and n columns is initially filled with water. We may perform an addLand operation which turns the water at position (row, col) into a land. Given a list of positions to operate, count the number of islands after each addLand operation. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

***Example:***
Given m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]].
Initially, the 2d grid grid is filled with water. (Assume 0 represents water and 1 represents land).
```
0 0 0
0 0 0
0 0 0
```
Operation #1: addLand(0, 0) turns the water at grid[0][0] into a land.
```
1 0 0
0 0 0   Number of islands = 1
0 0 0
```
Operation #2: addLand(0, 1) turns the water at grid[0][1] into a land.
```
1 1 0
0 0 0   Number of islands = 1
0 0 0
```
Operation #3: addLand(1, 2) turns the water at grid[1][2] into a land.
```
1 1 0
0 0 1   Number of islands = 2
0 0 0
```
Operation #4: addLand(2, 1) turns the water at grid[2][1] into a land.
```
1 1 0
0 0 1   Number of islands = 3
0 1 0
```
We return the result as an array: [1, 1, 2, 3]

**Challenge**
Can you do it in time complexity O(k log mn), where k is the length of the positions?


**Solution**
The most straightforward solution is to put all positions into the map, and use the same approach as the **3.1. Number of Islands**. However, since it requires solving the problem in O(k logmn) time complexity, the union find approach becomes the only option.

```java
public class Solution {
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        List<Integer> res = new ArrayList<Integer>();
        if (m <= 0 || n <= 0 || positions == null || positions.length == 0) {
            return res;
        }
        int[][] grid = new int[m][n];
        UF uf = new UF(m, n);
        for (int i = 0; i < positions.length; i++) {
            int[] position = positions[i];
            int x = position[0];
            int y = position[1];
            if (grid[x][y] == 1) {
                continue;
            }
            grid[x][y] = 1;
            uf.count++;
            if (x > 0 && grid[x - 1][y] == 1) {
                uf.union((x - 1) * n + y, x * n + y);
            }

            if (x < m - 1 && grid[x + 1][y] == 1) {
                uf.union((x + 1) * n + y, x * n + y);
            }

            if (y > 0 && grid[x][y - 1] == 1) {
                uf.union(x * n + y - 1, x * n + y);
            }

            if (y < n - 1 && grid[x][y + 1] == 1) {
                uf.union(x * n + y + 1, x * n + y);
            }
            res.add(uf.count);
        }
        return res;
    }

    public class UF {
        int[] ids;
        int count;

        public UF (int m, int n) {
            ids = new int[m * n];
            for (int i = 0; i < m * n; i++) {
                ids[i] = i;
            }
            count = 0;
        }

        public int root (int p) {
            while (p != ids[p]) {
                ids[p] = ids[ids[p]];
                p = ids[p];
            }
            return p;
        }

        public void union(int p, int q) {
            int pParent = root(p);
            int qParent = root(q);
            if (pParent == qParent) {
                return;
            }
            ids[qParent] = pParent;
            count--;
        }
    }
}
```
### 3.3. Surrounded Regions
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.
A region is captured by flipping all 'O's into 'X's in that surrounded region.
For example,
```
X X X X
X O O X
X X O X
X O X X
```
After running your function, the board should be:
```
X X X X
X X X X
X X X X
X O X X
```

**Solution1: Breath First Search**
Use BFS to find all 'O' positions that are not surrounded by 'X', and change them to '.' from 'O', then replace all remaing 'O' to 'X', and '.' to 'O'
```java
public class Solution {
    public void solve(char[][] board) {
        if (board == null || board.length <= 2 || board[0].length <= 2) {
            return;
        }
        //Step1: change all invalid 'O's to '.';
        int rows = board.length;
        int cols = board[0].length;
        Queue<Integer> queue = new LinkedList<Integer>();
        for (int i = 0; i < rows; i++) {
            if (board[i][0] == 'O') {
                board[i][0] = '.';
                queue.offer(i * cols);
            }

            if (board[i][cols - 1] == 'O') {
                board[i][cols - 1] = '.';
                queue.offer(i * cols + cols - 1);
            }
        }

        for (int j = 1; j < cols - 1; j++) {
            if (board[0][j] == 'O') {
                board[0][j] = '.';
                queue.offer(j);
            }

            if (board[rows - 1][j] == 'O') {
                board[rows - 1][j] = '.';
                queue.offer((rows - 1) * cols + j);
            }
        }

        while (!queue.isEmpty()) {
            int num = queue.poll();
            int row = num / cols;
            int col = num % cols;
            if (row < rows - 1 && board[row + 1][col] == 'O') {
                board[row + 1][col] = '.';
                queue.offer((row + 1) * cols + col);
            }

            if (row > 0 && board[row - 1][col] == 'O') {
                board[row - 1][col] = '.';
                queue.offer((row - 1) * cols + col);
            }

            if (col < cols - 1 && board[row][col + 1] == 'O') {
                board[row][col + 1] = '.';
                queue.offer(row * cols + col + 1);
            }

            if (col > 0 && board[row][col - 1] == 'O') {
                board[row][col - 1] = '.';
                queue.offer(row * cols + col - 1);
            }
        }

        //Step2: Change all 'O' to 'X', and '.' to 'O';
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (board[i][j] == '.') {
                    board[i][j] = 'O';
                } else if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                }
            }
        }
    }
}
```

**Solution2: Union Find**

```java
public class Solution {
    int[] id;
    boolean[] hasEdge;

    public void solve(char[][] board) {
        if (board == null || board.length <= 2 || board[0].length <= 2) {
            return;
        }
        int m = board.length, n = board[0].length;
        id = new int[m * n];
        hasEdge = new boolean[m * n];
        for (int i = 0; i < m * n; i++) {
            id[i] = i;
        }
        // check the O in boundary
        for (int i = 0; i < m * n; i++) {
            int x = i / n, y = i % n;
            hasEdge[i] = (board[x][y] == 'O' && (x == 0 || x == m - 1 || y == 0 || y == n - 1));
        }
        //union all the Os
        for (int i = 0; i < m * n; i++) {
            int x = i / n, y = i % n, up = x - 1, left = y - 1;
            // union itself with up if possible
            if (up >= 0 && board[x][y] == 'O' && board[up][y] == 'O') union( i - n, i);
            // union itself with left if possible
            if (left >= 0 && board[x][y] == 'O' && board[x][left] == 'O') union(i - 1, i);
        }
        for (int i = 0; i < id.length; i++) {
            int x = i / n, y = i % n;
            int root_i = root(i);
            if (!hasEdge[root_i] && board[x][y] == 'O') {
                board[x][y] = 'X';
            }
        }
    }
    public void union(int i, int j) {
        int x = root(i);
        int y = root(j);
        id[y] = x;
        hasEdge[x] = hasEdge[x] || hasEdge[y];
    }
    public int root(int i) {
        while (id[i] != i) {
            id[i] = id[id[i]];
            i = id[i];
        }
        return i;
    }
}
```

### 3.4. Graph Valid Tree 
Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.
For example:

Given n = 5 and edges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.
Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.

**Solution: Union Find**
Union the two nodes if they are connected by edge,  the tree is invalid if a new edge comes to connect two nodes that are already connected.
```java
public class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (n <= 1) {
            return n == 1;
        }
        
        int[] roots = new int[n];
        for (int i = 1; i < roots.length; i++) {
            roots[i] = i;
        }
        
        for (int[] edge : edges) {
            int root0 = findRoot(edge[0], roots);
            int root1 = findRoot(edge[1], roots);
            if (root0 != root1) {
                roots[root0] = roots[root1];
            } else {
                return false;
            }
        }
        return edges.length == n-1;
    }
    
    
    private int findRoot(int index, int[] roots) {
        while (roots[index] != index) {
            roots[index] = roots[roots[index]];
            index = roots[index];
        }
        return index;
    }
}
```
**Question:** can union find be applied to solving graph issue? Like finding circle in graph.
### 3.5. Number of Connected Components in an Undirected Graph
Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.
**Example 1:**
```
     0          3
     |          |
     1 --- 2    4
```
Given n = 5 and edges = [[0, 1], [1, 2], [3, 4]], return 2.

**Example 2:**
```
     0           4
     |           |
     1 --- 2 --- 3
```
Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]], return 1.

**Solution:**
```java
public class Solution {
    public int countComponents(int n, int[][] edges) {
        if (n <= 1) {
            return n;
        }

        int[] roots = new int[n];
        for (int i = 0; i < roots.length; i++) {
            roots[i] = i;
        }

        for (int[] edge : edges) {
            int x = findRoot(edge[0], roots);
            int y = findRoot(edge[1], roots);
            if (x != y) {
                roots[x] = y;
                n--;
            }
        }
        return n;
    }

    private int findRoot(int i, int[] roots) {
        while (i != roots[i]) {
            roots[i] = roots[roots[i]];
            i = roots[i];
        }
        return i;
    }
}
```

## 4. References
- [Princeton Algorithms: Union Find](https://www.cs.princeton.edu/~rs/AlgsDS07/01UnionFind.pdf)
- [Tushar Roy's Video: Disjoint Sets using union by rank and path compression Graph Algorithm](https://www.youtube.com/watch?v=ID00PMy0-vE)

