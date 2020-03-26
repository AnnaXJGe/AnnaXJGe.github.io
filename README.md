
leetcode用java

不要完全按tag！头一次刷，先把这五个tag做了：array，string，tree，linkedlist，math，其它的千万别按tag刷。

按顺序前150道

按分类   图、树、堆、栈、链表、哈希表、记忆搜索、动态规划、指针法、并查集等



计算机基础

简单题#easy 汇总
leetcode.com/problemset/all/?difficulty=Easy

## 001 Two Sum

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] == target - nums[i]) {
                    result = new int[] {i,j};
                    
                }
            }
        }
        return result;
    }
}
```



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


## 24. Swap Nodes in Pairs

链表结构
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


递推
```
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
递归

```
class Solution {
    public ListNode swapPairs(ListNode head) {
      if (head == null || head.head == nell) return head;
      ListNode newone = head.next;
      head.next = swapPairs(head.next.next);
      newone.next = head;
      return newone;
    }
 }
 ```



### Two Strings (HackerRank)


```
static String twoStrings(String s1, String s2) {
        HashSet<Character> string1_chars = new HashSet();
        HashSet<Character> string2_chars = new HashSet();

        for (int i = 0; i < s1.length(); i++) {
            string1_chars.add(s1.charAt(i));
        }

        for (int j = 0; j < s2.length(); j++) {
            string2_chars.add(s2.charAt(j));
        }

        string1_chars.retainAll(string2_chars);

        if (string1_chars.isEmpty()) return "NO";
        else return "YES";

    }
```
含输入

```
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.regex.*;

public class Solution {

    // Complete the twoStrings function below.
    static String twoStrings(String s1, String s2) {
        HashSet<Character> string1_chars = new HashSet();
        HashSet<Character> string2_chars = new HashSet();

        for (int i = 0; i < s1.length(); i++) {
            string1_chars.add(s1.charAt(i));
        }

        for (int j = 0; j < s2.length(); j++) {
            string2_chars.add(s2.charAt(j));
        }

        string1_chars.retainAll(string2_chars);

        if (string1_chars.isEmpty()) return "NO";
        else return "YES";

    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int q = scanner.nextInt();
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int qItr = 0; qItr < q; qItr++) {
            String s1 = scanner.nextLine();

            String s2 = scanner.nextLine();

            String result = twoStrings(s1, s2);

            bufferedWriter.write(result);
            bufferedWriter.newLine();
        }

        bufferedWriter.close();

        scanner.close();
    }
}
```


面经里
```
public static void main(String[] args) {
	String[] a = {"ab", "cd", "ef"};
	String[] b = {"af", "ee", "ef"};
	String[] res = twoStrings(a, b);
	for(String r : res) {
		System.out.println(r);
	}
}

private static String[] twoStrings(String[] a, String[] b) {
	String[] res = new String[a.length];
	for(int i=0;i<a.length;i++) {
		int bitMaskA = 0;
		int bitMaskB = 0;
		for(int j =0;j<a[i].length();j++) {
			char ac = a[i].charAt(j);
			char bc = b[i].charAt(j);
			bitMaskA |= 1 << (ac - 'a');
			bitMaskB |= 1 << (bc - 'a');
		}
		res[i] = (bitMaskA & bitMaskB) > 0 ? "YES" : "NO"; 
	}
	return res;
}
```

另一种
```
public static void commonSubstring(List < String > a, List < String > b) {
      // Write your code here
      boolean[] ch = new boolean[26];
      int flag = 0;
      for (int i = 0; i < a.size(); i++) {
          flag = 0;
          ch = new boolean[26];
          for (int j = 0; j < a.get(i).length(); j++) {
              ch[a.get(i).charAt(j) - 'a'] = true;
          }

          for (int j = 0; j < b.get(i).length(); j++) {
              if (ch[b.get(i).charAt(j) - 'a']) {
                  flag = 1;
                  break;
              }
          }

          if (flag == 1)
              System.out.println("YES");
          else
              System.out.println("NO");
      }
  }
  ```
  
  


## Partitioning Array(HR)

```public static void main(String[] args) {
        System.out.println(partitionArrayUnique(new int[]{1,2,3,4}, 2)); // true
        System.out.println(partitionArrayUnique(new int[]{1,2,3,3}, 2)); // true
        System.out.println(partitionArrayUnique(new int[]{1,2,3,4}, 3)); // false
        System.out.println(partitionArrayUnique(new int[]{3,3,3,6,6,6,9,9,9}, 3)); // true
        System.out.println(partitionArrayUnique(new int[]{1,2,3,1,2,3,1,2,2}, 3)); // false
        System.out.println(partitionArrayUnique(new int[]{}, 1)); // true
        System.out.println(partitionArrayUnique(new int[]{1}, 1)); // true
        System.out.println(partitionArrayUnique(new int[]{1,2}, 2)); // true
    }

    public static boolean partitionArrayUnique(int[] nums, int k){
        if(nums.length % k != 0){
            return false;
        }

        HashMap<Integer, Integer> map = new HashMap<>();
        int max = 0;
        for(int num: nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
            if(map.get(num) > max){
                max = map.get(num);
            }
        }

        return max <= (nums.length / k);
    }
```


## 134. Gas Station



```
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        
        int start = 0, lack = 0, curr = 0;
        for(int i = 0; i < gas.length; i++)
        {
            curr += gas[i] - cost[i];
            if(curr < 0)
            {
                start = i+1;
                lack += curr;
                curr = 0;
            }
        }
        return curr + lack>=0?start:-1;

    }
}
```
有类似的题 阿拉丁神灯
```
public static int optimalPoint(List<Integer> magic, List<Integer> dist) {
        // Write your code here
        int pos = -1, curr = 0, total = 0; 
        for (int i = 0; i < magic.size(); i++) {
            int diff = magic.get(i) - dist.get(i);
            curr += diff; 
            total += diff;
            if (curr < 0) {
                curr = 0;
                pos = i;
            }
        }
        if (total >= 0) 
            return pos + 1; 
        return -1;
    }
 ```
 
 另一种面经
 ```
 public static int optimalPoint(List<Integer> magic, List<Integer> dist) {
        int sumofmagic = 0;
        int sumofdist = 0;
        int start = 0;
        int tank = 0;
        for(int i = 0; i < magic.size(); i++){
            sumofmagic += magic.get(i);
            sumofdist += dist.get(i);
            tank += magic.get(i) - dist.get(i);
            if(tank < 0){
                start = i + 1;
                tank = 0;
            }
        }
        if(sumofmagic < sumofdist){
            return -1;
        }
        else{
            return start;
        }
```
 
## Seperation Students

多少次相邻swap，能把打乱的[1,0,1,1,0,0,0,1]，变成[0,0,0,0,1,1,1,1]；一定只能相邻的交换！！


```
public static List<Integer> closest(String s, List<Integer> queries) {
        List<Integer> results = new ArrayList<>();
        char[] array = s.toCharArray();
        Map<Character, List<Integer>> map = new HashMap<>();
        for(int i = 0; i < array.length; i++){
            map.putIfAbsent(array[i], new ArrayList<Integer>());
            map.get(array[i]).add(i);
        }
        for(int query: queries){
            char c = array[query];
            List<Integer> index = map.get(c);
            if(index.size() == 1){
                results.add(-1);
            }
            else{
                int i = findclose(index, query);
                results.add(index.get(i));
            }
        }
        return results;

    }
    public static int findclose(List<Integer> indexs, int index){
        int start = 0;
        int end = indexs.size() - 1;
        int i = 0;
        while(start + 1 < end){
            int mid = start + (end - start) / 2;
            if(indexs.get(mid) == index){
                i = mid;
                break;
            }
            else if (indexs.get(mid) < index){
                start = mid;
            }
            else{
                end = mid;
            }
        }
        if(indexs.get(start) == index){
            i = start;
        }
        if(indexs.get(end) == index){
            i = end;
        }
        if(i == 0){
            return i + 1;
        }
        if(i == indexs.size() - 1){
            return i - 1;
        }
        if(Math.abs(indexs.get(i-1) - index) <= Math.abs(indexs.get(i+1) - index)){
            return i - 1;
        }
        return i+1;
    }


```

## Who’s the closest

给一个string有重复char，比方说“babab”。给你任意char的idx， 找离这个char距离最近的相同char的idx，如果有一样距离的返回小的。前面例子如果给2，返回0
 

```
public static int minMoves (int[] arr) {
        int ans = 0;
        ans = Math.min(helper(arr, true), helper(arr, false));
        return ans;
    }

    public static int helper (int[] arr, boolean flag) {
        int front = 0, end = 1;
        int count = 0;

        if (flag) {
            front = 1;
            end = 0;
        }

        int lo = 0, hi = arr.length - 1;
        while (lo < hi) {
            while (lo < hi && arr[lo] == front) {
                lo++;
            }
            while (hi > lo && arr[hi] == end) {
                hi--;
            }
            // forget to hi--, lo++.
            int tmp = arr[hi];
            arr[hi] = arr[lo];
            arr[lo] = tmp;
            hi--;
            lo++;
            count++;
        }
        System.out.println(Arrays.toString(arr));
        return count;
    }
```

下一个有时间上过不了的例子

```

public static List<Integer> closest(String s, List<Integer> queries) {
    // Write your code here
        List<Integer> result = new ArrayList<Integer>();
        if (queries.size() == 0) {
            return result;
        }

        char[] strToChar = s.toCharArray();

        for(int i = 0; i < queries.size(); i++) {
            int currIndx = queries.get(i); // target character index
            if (currIndx < 0 || currIndx >= strToChar.length) { // invalid index from query
                result.add(-1);
                continue;
            }

            char c = strToChar[queries.get(i)];

            int checkAway = 1;

            boolean found = false;
            
            // check left and right from current index and find closest index of same character
            while(currIndx - checkAway >= 0 || currIndx + checkAway < strToChar.length) {
                int moveLeft = currIndx - checkAway;
                int moveRight = currIndx + checkAway;
                
                if(moveLeft >=0 && c == strToChar[moveLeft]){
                    result.add(moveLeft);
                    found = true;

                    break;
                } else if(moveRight < strToChar.length && strToChar[moveRight] == c){
                    result.add(moveRight);
                    found = true;

                    break;
                }
                
                checkAway++;
            }

            if(!found){
                result.add(-1);
            }
        }

        return result;
    }
    
```


## Parking Dilemma

```
public static long carParkingRoof(List<Long> cars, int k) {
    // Write your code here
        if (cars.size() == 0 || k < 0) {
            return 0;
        }

        Collections.sort(cars);
        long minDist = Long.MAX_VALUE;

        for (int i = 0; i <= cars.size() - k; i++) {
            minDist = Math.min(minDist, cars.get(i + k - 1) - cars.get(i));
        }

        return minDist + 1;
    }
```




## Large Response

https://1o24bbs.com/t/topic/15217/8





