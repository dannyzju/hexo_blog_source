---
title: 'Techmon Go 1: Hash'
date: 2016-07-14 21:57:32
tags: TechmonGo Hash
---
### I. Hash Function
##### a. 31
In Java, the hash code for a String object is computed as

```
s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]
```

The value 31 was chosen because it is an odd prime. If it were even and the multiplication overflowed, information would be lost, as multiplication by 2 is equivalent to shifting. The advantage of using a prime is less clear, but it is traditional. A nice property of 31 is that the multiplication can be replaced by a shift and a subtraction for better performance: 31 * i == (i << 5) - i. Modern VMs do this sort of optimization automatically.

##### b. 31 mod n
Based on 31, mod the result with n, n stands for capacity.

##### c. rolling hash
This is used to find if str1 contains str2:

    index = 0123456789
    str1 = "fsaabcdefg"
    str2 = "abc"
    ...
    result1 = str1[3] * 31 ^ 0 + str1[4] * 31 ^ 1 + str1[5] * 31 ^ 2
    ...
    result2 = str2[0] * 31 ^ 0 + str2[1] * 31 ^ 1 + str2[2] * 31 ^ 2

### II. Hash Families
Hashtable: thread safe, but deprecated.
ConcurrentHashMap: an advanced version of Hashtable;
HashMap: not thread safe.
TreeMap: https://docs.oracle.com/javase/7/docs/api/java/util/TreeMap.html

### III. Implement hashCode and equals methods
```java
class Item {
    public String str;
    public Integer inter;
    public Object obj;
    public Integer inter1;

    @Override
    public int hashCode() {
        final int prime = 31;
        final int N = 345678;
        int result = 1;
        result = result * prime + str.hashCode();
        result = result * prime + inter;
        result = result * prime + obj.hashCode();
        return result;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }

        if (getClass() != obj.getClass()) {
            return false;
        }

        Item other = (Item) obj;

        if (str == null && other.str != null) {
            return false;
        } else if (!str.equals(other.str)) {
            return false;
        }
        return true;
    }
}
```

### IV. Probabilities
a. n elements, n cells, question: for any particular cell, the prob of
    the number of elements is equal to k.
    Ans: prob = C(n, k) * (1/n)^k * (1-1/n)^(n-k)

b. N people with everyone of different birthday
    Ans: p(n) = 365/365 * 364/365 * .. * (365-n)/365 < 50%

c. More probability questions
https://www.careercup.com/page?pid=probability-interview-questions

### V. Further Readings
a. Java Knowledge
    1. Annotation;


