xxx
leetcode用java

不要完全按tag！头一次刷，先把这五个tag做了：array，string，tree，linkedlist，math，其它的千万别按tag刷。

按顺序前150道

按分类   图、树、堆、栈、链表、哈希表、记忆搜索、动态规划、指针法、并查集等



计算机基础

简单题#easy 汇总
leetcode.com/problemset/all/?difficulty=Easy




## 344. Reverse String

遍历循环 递推
```java
class Solution {
  public void reverseString(char[] s) {
    int length = s.length;
    for (int i = 0; i < length/2; i==) {
      char temp = s[length - i - 1];
      s[i] = s[length - i - 1];
      s[length - i - 1] = temp;
    }
  }
}
```

递归
```java
class Solution {
  public void reverseString(char[] s) {
    helper(0,s);
  )
  public static void helper(int index, char[] s) {
    if (s == null || index >= s.length/2) {
      return;
     }
    char temp = s[index];
    s[index] = s[s.length - index - 1];
    s[s.length - index - 1] = temp;
    helper(index + 1, s);
  }
}
```


### 24. Swap Nodes in Pairs
