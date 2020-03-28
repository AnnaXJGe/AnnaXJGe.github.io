
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

另一种

```
public static int aladdin(int [] magic, int [] dis){
        int totalMagic = 0;
        int totalUsed = 0;
        int magicElixir = 0;
        int minStart = 0;
        for(int i = 0; i<magic.length;i++){
            totalMagic += magic;
            totalUsed += dis;
            magicElixir += magic - dis;
            if(magicElixir<0) {
                minStart = i+1;
                magicElixir = 0;
            }            
        }
        return (totalMagic < totalUsed) ? -1 : minStart;
    }
    
```
 
 
## Seperating Students

多少次相邻swap，能把打乱的[1,0,1,1,0,0,0,1]，变成[0,0,0,0,1,1,1,1]；一定只能相邻的交换！！

不对的解法
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
自己尝试
可以用两个pointer记录，第一个记录遇0的位置，第二个从第一个pointer之后开始loop, 遇到1，计算index差，然后pointer++。把list reverse一下再走一遍，取两次值小的。index为i + 1时，重新计算累计和也需要O(n)完成一个cycle，再次来到i + 1时停止

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

        for ( int i = 0; i < arr.length - 1; i++) {
		int m = i, j = 0;
		while (arr[m] = front) m++;
		if (arr[m] = end) {
			int j = m+1;
			}
		while (arr[j] = end) j++;
		if (arr[j] = 0) {
			count += j - i;
			temp = arr[i];
			arr[i] = arr[j];
			arr[j] = temp;
			}
		}
        System.out.println(Arrays.toString(arr));
        return count;
	}

```



## Who’s the closest

给一个string有重复char，比方说“babab”。给你任意char的idx， 找离这个char距离最近的相同char的idx，如果有一样距离的返回小的。前面例子如果给2，返回0
 

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
This is a sliding window problem

```
 public static int minRoofLength(int[] arr, int k){
    Arrays.sort(arr);
    int start = 0;
    int minRoofLength = Integer.MAX_VALUE;
    for(int end=0;end<arr.length;end++){
      if(end < k-1) continue;
      int currentRoofLength = arr[end]-arr[start++]+1;
      minRoofLength = Math.min(minRoofLength, currentRoofLength);
    }
    return minRoofLength;
  }
```

## Shifting Strings

这个主要是看下规律，会发现针对rightShifts移动字符的时候，其实就是针对
leftShifts移动s.length() - rightShifts个字符。
给一个string 和 int leftShifts, int rightShifts. 输出shift 后的strings. 如果s = abcd, leftShift1 =
bcda, 然后在rightShift2 = dabc.

```
import java.util.*; 
import java.io.*; 
  
class GFG  
{ 
          
    // function that rotates s towards left by d  
    static String leftrotate(String str, int d) 
    { 
            String ans = str.substring(d) + str.substring(0, d); 
            return ans; 
    } 
  
    // function that rotates s towards right by d  
    static String rightrotate(String str, int d) 
    { 
            return leftrotate(str, str.length() - d); 
    } 
  
    // Driver code 
    public static void main(String args[]) 
    { 
            String str1 = "GeeksforGeeks";  
            System.out.println(leftrotate(str1, 2)); 
  
            String str2 = "GeeksforGeeks";  
            System.out.println(rightrotate(str2, 2));  
    } 
} 
  
```



## Purchasing Supplies

大致意思是 你有一个budget n, cost c, 还有一个m. 如果 n =
4, c = 1, m = 2的话， 你可以先买4个集装箱，然后着4个集装箱退给他，还给你4/m = 2个， 退回
来的2个再还给他，在给你2/m = 1个。最后你会有 4 + 2 + 1 = 7个。
买containers，给最开始的budget，每个container的cost，和多少个container可以exchange一个
新的。求总共能有多少个container。E.g., 6块budget，cost = 2，exchange = 2，总共能有5个箱
子（最开始能买仨，用这三个里面的两个再换一个，用刚刚三个里省下的和这个新换的再换一个
，总共5个）



这个就是啤酒空瓶换酒的模型，
输入是 《初始资金，啤酒单价，几个瓶子能换一瓶酒》的string， 输出是直接打印，不需要return （这个比较鬼畜）





## Census.csv

给定一个数据集（附件census.csv），这个数据集总共30162行。
每一行表示一名用户，每一个逗号分隔表示该用户的特征。总共拥有12个特征：
["age","sex","education","native-country","race","marital-status","workclass","occupation","hours-per-week","income","capital-gain","capital-loss"]
举个例子，某一行的数据可能长这个样子：
age=Middle-aged,sex=Male,education=Bachelors,native-country=United-States,race=White,marital-status=Never-married,workclass=State-gov,occupation=Adm-clerical,hours-per-week=Full-time,income=Small,capital-gain=Low,capital-loss=None

现在输入两个值 n, p，
要求输出拥有n个特征的，在原始数据中出现概率大于p的组合。

样例输入1
3
0.7

样例输出1
native-country=United-States,race=White,capital-gain=None
native-country=United-States,race=White,capital-loss=None
native-country=United-States,capital-gain=None,capital-loss=None
race=White,capital-gain=None,capital-loss=None

解释:
以第一行输出为例：
native-country=United-States，
race=White，
capital-gain=None
这3条的组合在数据集中出现的占比要高于0.7

样例输入2
4
0.6

样例输出2
native-country=United-States,race=White,capital-gain=None,capital-loss=None
native-country=United-States,income=Small,capital-gain=None,capital-loss=None

解释
同理，4个特征同时出现，概率大于 0.6 的情况
总共只有以上2种情况。


```
import csv
col_name = ["age","sex","education","native-country","race","marital-status",
            "workclass","occupation","hours-per-week","income","capital-gain","capital-loss"]

def iterator(wait_choose, file, count, total, start, target):
    flag = 0
    res_set = []
    res_ind = []
    if count == total:
        #print(count)
        return [],1,[-1]
    for index in range(start,len(wait_choose) - (total - count) +1):
        if len(wait_choose[index]) == 0:
            #print("jump",count,index)
            continue
        
        #print("try", count,index)
        for word in wait_choose[index]:
            fileChosen, counts = chooseFrom(file, index, word)
            if (counts + 0.0)/30162 < target:
                continue
            else:
                #print(counts/30162)
                strs, flag, s_index = iterator(wait_choose,fileChosen,count+1,total,index+1,target)
                #print(strs,flag,s_index)
            if flag == 1:
                if len(strs) == 0:
                    res_set.append(word)
                    res_ind.append(str(index))
                else:
                    for string in strs:
                        line = word
                        line = line + ","+ string
                        res_set.append(line)
                        
                    ind = "" + str(index)
                    for intd in s_index:
                        ind = "" + str(index)
                        ind = ind +","+ str(intd)
                        res_ind.append(ind)
                    
    if len(res_set) == 0:
        return [], 0,[-1]
    else:
        return res_set,1 ,res_ind
                    

def chooseFrom(files,attr_index,attr):
    number = 0
    file_chosen = []
    for file in files:
        if file[attr_index] == attr:
            number = number + 1
            file_chosen.append(file)
    return file_chosen, number

def attributesSet(numberOfAttributes, supportThreshold):
    dicts = []
    files = []
    for i in range(len(col_name)):
        diction = {}
        dicts.append(diction)
    with open("census.csv","r") as csv_file:
        all_lines = csv.reader(csv_file)
        for one_line in all_lines:
            a_line = []
            for index in range(len(one_line)):
                attr = one_line[index].split("=")
                if attr[1] in dicts[index].keys():
                    dicts[index][attr[1]] = dicts[index][attr[1]] + 1
                else:
                    dicts[index][attr[1]] = 0
                a_line.append(attr[1])
            files.append(a_line)
                    
    wait_choose = []
    for dic in dicts:
        wait_line = []
        for(k,v) in dic.items():
            dic[k] = (v + 0.0)/30162
            if dic[k] < supportThreshold:
                continue
            else:
                wait_line.append(k)
        wait_choose.append(wait_line)
    
    true_tabel = []
    ct = 0
    
    for wt in wait_choose:
        if len(wt) == 0:
            true_tabel.append(0)
        else:
            true_tabel.append(1)
            ct = ct + 1
    
    if ct < numberOfAttributes:
        return ""
    
    #print(wait_choose)
    #print(true_tabel)
    
    res_set, flag, res_ind = iterator(wait_choose,files,0,numberOfAttributes,0, supportThreshold)
    #print(res_set,res_ind)
    
    res_set_2 = []
    for index in range(len(res_set)):
        tag = res_set[index].split(",")
        #print(tag)
        ind = res_ind[index].split(",")
        #print(ind)
        lines = ""
        for j in range(len(tag)):
            line = ""
            if j == 0:
                line = col_name[int(ind[j])] +"="+ tag[j]
            else:
                line = lines+ ","+ col_name[int(ind[j])] +"="+ tag[j]
            lines = line
            #print(lines)
        res_set_2.append(lines)
    print(res_set_2)
    
    return 0

if __name__ == "__main__":
    
    attributesSet(3,0.7)
```


## Meandering Array





sort array in meandering order








## Triple


有几个小于特定值的3Sum。
可以参考这个  Print triplets with sum less than or equal to k
https://www.geeksforgeeks.org/pr ... than-or-equal-to-k/

https://baihuqian.github.io/2018-07-28-3sum-smaller/

https://blog.csdn.net/qq508618087/article/details/50881359

里抠二吴久, 不一样的是他给的是个long，你输出也用long就行

https://leetcode.com/problems/valid-triangle-number/discuss/104200/



## merge 两个sorted list。







## Large Response

large response. 他会用Sacnner读一个文件名，然后你根据这个文件名按行读文件，读出其中的一个数字存下来再写出去的就行，做之前稍微看一下bufferReder和bufferWriter的用法就行。




文件I/O题 request record，给一个文件名，按行读取里面的记录，只要取最后的bytes数就行，大于5000就输出，txt文件里长得类似这样：
www.leetcode.com - - GET /leetcode.com/problems/all 200 300
www.google.com - - GET /google.com/search? 200 59349
www.baidu.com - - GET /baidu.com/news 200 300

我的代码：

```
ifstream ifile(filename);
ofstream ofile(ofilename);
string line;
int sum = 0, count=0;
while (getline(file, line)
{
int n = line.size()-1, t=1, tmp=0;
while (isdigit(line[n])){
tmp += (line[n] - '0')*t;
t *= 10;
n--;
}
if (tmp >= 5000) {
sum += tmp;
count++;
}
}
ofile<< count<<endl<<sum;
return ;
```


opsDev的oa，四道题，第一题很简单，第二题写regex也很简单，
后面两题竟然要本地ssh，

https://blog.csdn.net/qq_34581118/article/details/77132208?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

第三题写shell（算fib，不难）

https://blog.csdn.net/lizhidefengzi/article/details/76860425

第四题写一个叫puppet的东西（完全懵逼），挣扎着查了一下好像是运维用的东西

https://blog.51cto.com/blxueyuan/1924072


## Email Threads

一个把Email变成Thread的题目，给一连串的Email，有收件人，发件人，内容。内容里面如果包含之前的信息的话之前的信息会有“---”的标记，然后问题是你如何把Email变成thread，你懂的，就是Gmail里面那个把来信和发信都整一起的那玩意。刚上手第一想法：根据收件人和发件人进行分类，分类分完了直接每个分类里面的内容标记一下是当前这个thread的哪道邮件。结果被test case打脸，仔细想了想发现不对，谁规定了两个人只能有一个thread了？
没有给subject，需要根据sender和receiver来确定放哪个thread
------结果想出的方法是先找出开头的一封邮件，再在邮件堆里搜索有木有接下来的邮件，复杂度（O(n^2)), testcase全过

一个responsive的HTML Design, flexbox+mediaQuery轻松搞定。


https://1o24bbs.com/t/topic/15217/8


https://paper.dropbox.com/doc/IBM-OA-4WtsQ9aiolsi0HXm3mECx


https://www.1point3acres.com/bbs/collection/229895


https://1o24bbs.com/t/topic/15217/7



js的题
https://www.1point3acres.com/bbs/thread-584292-1-1.html


