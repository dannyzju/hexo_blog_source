---
title: 'Techmon Go 2: Topological Sort'
date: 2016-07-16 20:39:07
tags: TechmonGo TopologicalSort
---
### I. Topological Sort Definition
First of all, what is topological Sort? Here is the definition from WikiPedia
>In the field of computer science, **a topological sort** or **topological** ordering of a directed graph is a linear ordering of its vertices such that for every directed edge uv from vertex u to vertex v, u comes before v in the ordering.

Originally, say we have a graph like this.
![Original Graph](/content/images/2016/graph.png)

After the topological sort, we will get a list like this:
![Sorted Graph](/content/images/2016/sortedGraph.png)


### II. Topological Sort Algorithm
![Topological Sort Algorithm](/content/images/2016/topologicalSort1.png)
![Topological Sort Algorithm Explanation](/content/images/2016/topologicalSort2.png)

### III. Topological Sort Problems
#### 1. Alien Dictionary
There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

For example,
Given the following words in dictionary,
`["wrt", "wrf", "er", "ett", "rftt"]`

The correct order is: `"wertf"`.

思路：可以通过一定的转换，把这个问题转化为Topological Sort的问题。此外，在基本的拓扑排序算法之外，这里还需要考虑是否会有循环产生的情况，如果发生循环，则数据无效，返回空字符串。具体代码和注释如下。

```java
public class Solution {
    public int index;
    char[] results;
    Map<Character, Integer> visitedMap;
    public String alienOrder(String[] words) {
        Map<Character, GraphNode> map = new HashMap<Character, GraphNode>();
        int nodeCount = 0;
        //Step1: Create all graph nodes;
        for (int i = 0; i < words.length; i++) {
            String word = words[i];
            for (int j = 0; j < word.length(); j++) {
                char c = word.charAt(j);
                if (!map.containsKey(c)) {
                    map.put(c, new GraphNode(c));
                    nodeCount++;
                }
            }
        }

        //Step2: Create the connections between different nodes.
        for (int i = 0; i < words.length - 1; i++) {
            String word1 = words[i];
            String word2 = words[i + 1];
            int j = 0;
            while (j < word1.length() && j < word2.length()) {
                char c1 = word1.charAt(j);
                char c2 = word2.charAt(j);
                if (c1 != c2) {
                    map.get(c1).neighbors.add(map.get(c2));
                    break;
                }
                j++;
            }
        }

        //Step3: Topological Sorting.
        visitedMap = new HashMap<Character, Integer>();
        results = new char[nodeCount];
        index = nodeCount;
        for (GraphNode node : map.values()) {
            if (visitedMap.containsKey(node.c)) {
                continue;
            }
            if (!sortHelper (node)) {
                return "";
            }
        }
        return String.valueOf(results);
    }

    private boolean sortHelper(GraphNode node) {
        visitedMap.put(node.c, -1); //-1 代表该点正在被访问，用于避免循环的情况出现.
        Iterator it = node.neighbors.iterator();
        while (it.hasNext()) {
            GraphNode neighbor = (GraphNode)it.next();
            if (visitedMap.containsKey(neighbor.c)) {

                if (visitedMap.get(neighbor.c) == -1) { //如果循环发生，则返回false
                    return false;
                }

                if (visitedMap.get(neighbor.c) == 1) {  //如果已经被访问过，则跳过
                    continue;
                }
            } chua

            if (!sortHelper(neighbor)) {
                return false;
            }
        }

        visitedMap.put(node.c, 1); //完成该节点访问，状态变1
        results[--index] = node.c;
        return true;
    }

    public class GraphNode {
        char c;
        Set<GraphNode> neighbors;
        public GraphNode (char c) {
            this.c = c;
            this.neighbors = new HashSet<GraphNode>();
        }
    }
}
```

此外，可以用Topological Sort解决的问题还有：
- [LeetCode 210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)
- [LeetCode 329. Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)