
leetcode用java

不要完全按tag！头一次刷，先把这五个tag做了：array，string，tree，linkedlist，math，其它的千万别按tag刷。

按顺序前150道

按分类   图、树、堆、栈、链表、哈希表、记忆搜索、动态规划、指针法、并查集等



计算机基础

简单题#easy 汇总
leetcode.com/problemset/all/?difficulty=Easy




## 344. Reverse String

遍历 递推
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
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
```
```
递推 
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode dummy = new ListNode(0);//建虚拟头
        dummy.next = head;//虚拟头指向head
        ListNode l1 = dummy;
        ListNode l2 = head;
        while (l2 != null && l2.next != null) {
            ListNode newStart = l2.next.next;//建下一次转换的开始，不能用l2.next.next, 因为l2会变
            l1.next = l2.next;//l1指向l2的下一个
            l2.next.next = l2;//l2的下一个指向l2
            l2.next = newStart;//l2指向newstart
            l1 = l2;//指针后错一位
            l2 = l2.next;//指针后错一位
        }
        return dummy.next;//不能用l1，l2，那是指针
    }
}
```
