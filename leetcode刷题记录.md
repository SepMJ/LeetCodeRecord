# leetcode刷题记录

## day1：2025/1/5

### 数组-二分查找

1. 704 二分查找

2. 35 搜索插入位置

3. 34 在排序数组中查找元素的第一个和最后一个位置

## day2：2025/1/6

### 数组-二分查找-移除元素（快慢指针/双指针）

1. 69 X的平方根 -- 二分查找

2. 367.有效的完全平方数 -- 二分查找

3. **27 移除元素 -- 快慢指针**

4. 26 删除排序数组中的重复项 --快慢指针

5. 283 移动零 -- 快慢指针

## day3：2025/1/7

### 数组-双指针-滑动窗口

1. 844 比较含退格的字符串 --双指针

   `toString()` 是 Java 中 `Object` 类的一个方法，它的目的是返回对象的字符串表示形式，默认情况下，`Object` 类的 `toString()` 方法返回的是**对象的类名和该对象的哈希码**。

```java
MyClass obj = new MyClass();
System.out.println(obj.toString());  // 输出: MyClass@15db9742
```

​	  `new String(s)` 会创建一个新的 `String` 对象，该对象包含 `s` 字符数组中的所有字符内容。

2. 977 有序数组的平方 ---双指针，指针从两端开始，空间复杂度不再是O(n)

3. **209长度最小的子数组 --滑动窗口**

4. **94 水果成篮 -- 滑动窗口 -- 哈希表 --哈希表put，remove**

5. **76 覆盖最小字串 -- 滑动窗口 -- 哈希表** 

## day4：2025/1/8

### 数组-螺旋矩阵II-模拟矩阵--四个指针转圈 -- 区间和 -- 前缀和

1. **59螺旋矩阵II  ---每圈分为顶部、右列、底部、左列四个部分，每部分左闭右开，判断圈数，偏移量，也可以想象成四个指针转圈圈**

2. **54螺旋矩阵 -- ==四个指针转圈圈==**

   ![image-20250108151009722](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250108151009722.png)

3. **LCR 146. 螺旋遍历二维数组**

4. 区间和  - - - ==**前缀和 在涉及计算区间和的问题时非常有用**！==

   设置一个数组p[i]，先做累加，即 p[i] 表示 下标 0 到 i 的 vec[i] 累加 之和

![image-20250108154117333](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250108154117333.png)



```java
   import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        int[] vec = new int[n];
        int[] p = new int[n];

        int presum = 0;
        for (int i = 0; i < n; i++) {
            vec[i] = scanner.nextInt();
            presum += vec[i];
            p[i] = presum;
        }

        while (scanner.hasNextInt()) {
            int a = scanner.nextInt();
            int b = scanner.nextInt();

            int sum;
            if (a == 0) {
                sum = p[b];
            } else {
                sum = p[b] - p[a - 1];
            }
            System.out.println(sum);
        }

        scanner.close();
    }
}

```
5. 开发商购买土地   -- 也用到了前缀和

### 数组总结

二分法、双指针、滑动窗口、模拟行为、前缀和

## day5：2025/1/9

### 链表   -- 移除 -- 设计 --反转链表-- 两两交换元素

**链表节点定义：**

```java
public class ListNode {
    int val;
    ListNode next;

    ListNode() {
    }

    ListNode(int val) {
        this.val = val;
    }

    ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }

}

```

1. 203 移除链表元素  -- ==设置一个虚拟的头节点，统一操作== --注意循环条件 `cur.next!=null`

2. 707 设计链表  --虚拟头结点+单链表  --- 也可以使用双向链表，设计虚拟头结点，虚拟尾结点

   ```
   class MyLinkedList { //链表由多个链表结点构成
   
       class ListNode { //链表结点的定义
           int val;
           ListNode next;
   
           public ListNode(int val) {
               this.val = val;
           }
       }
   
       private int size;
       private ListNode virtualhead; //虚拟头结点
   
       public MyLinkedList() {
           //初始化size，初始化虚拟头结点
           this.size = 0;
           this.virtualhead = new ListNode(0);
   
       }
   }
   ```

3. 206 反转链表  -- 设置一个虚拟头结点，并且头插法，向头结点之前插入节点 -- 也可以使用双指针法

```
if (head == null) return head;
//虚拟头结点解决链表反转
ListNode virtualnode = new ListNode(0);
ListNode cur = head;
while (cur != null) {
    ListNode newNode = new ListNode(cur.val);
    newNode.next = virtualnode.next;
    virtualnode.next = newNode;
    cur = cur.next;
}
return virtualnode.next;
```

双指针法

```
//双指针方法解决链表反转
ListNode pre = null;
ListNode cur = head;
ListNode temp = null;//用来暂时保存节点
while (cur != null) {
    temp = cur.next;
    cur.next = pre;
    pre = cur;
    cur = temp;
}
return pre;
```

4. 两两交换链表中的结点   -- 

![image-20250109162041250](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250109162041250.png)

```
class Solution {
  public ListNode swapPairs(ListNode head) {
        ListNode dumyhead = new ListNode(-1); // 设置一个虚拟头结点
        dumyhead.next = head; // 将虚拟头结点指向head，这样方便后面做删除操作
        ListNode cur = dumyhead;
        ListNode temp; // 临时节点，保存两个节点后面的节点
        ListNode firstnode; // 临时节点，保存两个节点之中的第一个节点
        ListNode secondnode; // 临时节点，保存两个节点之中的第二个节点
        while (cur.next != null && cur.next.next != null) {
            temp = cur.next.next.next;
            firstnode = cur.next;
            secondnode = cur.next.next;
            cur.next = secondnode;       // 步骤一
            secondnode.next = firstnode; // 步骤二
            firstnode.next = temp;      // 步骤三
            cur = firstnode; // cur移动，准备下一轮交换
        }
        return dumyhead.next;  
    }
}
```

5. 删除链表倒数第N个结点（一趟扫描）--使用双指针，首先让两个指针相距n，设置一个虚拟头结点，到后一个指针指到最后一个的时候，那么删除的元素就是前面指针的下一个结点。

   ```
   class Solution {
       public ListNode removeNthFromEnd(ListNode head, int n) {
           //新建一个虚拟头节点指向head
           ListNode dummyNode = new ListNode(0);
           dummyNode.next = head;
           //快慢指针指向虚拟头节点
           ListNode fastIndex = dummyNode;
           ListNode slowIndex = dummyNode;
   
           // 只要快慢指针相差 n 个结点即可
           for (int i = 0; i <= n; i++) {
               fastIndex = fastIndex.next;
           }
           while (fastIndex != null) {
               fastIndex = fastIndex.next;
               slowIndex = slowIndex.next;
           }
   
           // 此时 slowIndex 的位置就是待删除元素的前一个位置。
           // 具体情况可自己画一个链表长度为 3 的图来模拟代码来理解
           // 检查 slowIndex.next 是否为 null，以避免空指针异常
           if (slowIndex.next != null) {
               slowIndex.next = slowIndex.next.next;
           }
           return dummyNode.next;
       }
   }
   ```

## day6：2025/1/10

### 链表相交 -- 环形链表

1. 160 链表相交 

   就是求两个链表交点节点的**指针**。 要注意，**==交点不是数值相等，而是指针相等==**，比较curA和curB是否相同，如果不相同，同时向后移动curA和curB，==如果遇到curA == curB，则找到交点，交点后面都一样。==否则循环退出返回空指针。

   ![image-20250110112235627](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250110112235627.png)

2. 142 环形链表II --考虑哈希Set集合，判断指针指向的结点是否存在，利用set集合不能有重复元素的特性。不用hashmap，是因为map基于key-value，如果有相同结点的值，那么可能会覆盖，或者让指针作为key。

   也可以用快慢指针，但是快慢指针非常不好理解，而且需要数学推导

   **有序和无序是指元素插入的顺序**

3. 234 回文链表   

   我的做法：反转链表，再判断链表上各个结点的值是否相等

   **还可以用栈（暂时还不熟练，后面可以再做一遍）**

### 链表总结

设置虚拟头结点。链表的基本操作（增删改查）、反转链表（双指针、虚拟头结点和头插法）、删除倒数第N个结点（双指针）、链表相交（指针，双指针）、环形链表（哈希表）

**指针相同，而不是数值相同，注意区别**



## day7：2025/1/12

### 哈希表

常见三种哈希结构：

- 数组
- set （集合）
- map(映射)

1. 242 有效的字母异位词

   **字母异位词定义**：字母异位词是两个包含相同字母但排列顺序不同的字符串。例如 `"abc"` 和 `"bca"` 就是异位词

## day8：2025/1/13

### **字母异位词  -- 涉及：数组，滑动窗口，哈希map**

1. 49 字母异位词分组  -- 哈希map，涉及到字符串的排序，可以将排序之后的字符串作为哈希表的键

2. 438 找到字符串中所有字母异位词-- 这道题的思路就不是哈希map，而是**==选择用数组+滑动窗口==**，与往常不同的是，滑动窗口的长度这次是已知的，**让==滑动窗口的长度与目标字符串长度一致==**，不断移动窗口，本质上，数组也是一种哈希表。

   如果使用哈希map的也可以，只是需要在判断的时候，判断key的value如果等于0的话，需要remove移除key，这一点不如数组操作起来比较方便。

   ```
   public List<Integer> findAnagrams(String s, String p) {
       int sLen = s.length(), pLen = p.length();
   
       // 如果 s 的长度小于 p 的长度，直接返回空列表，因为不可能有异位词
       if (sLen < pLen) {
           return new ArrayList<Integer>();
       }
   
       List<Integer> ans = new ArrayList<Integer>();
       int[] sCount = new int[26]; // 用于统计字符串 s 中每个字母的频次
       int[] pCount = new int[26]; // 用于统计字符串 p 中每个字母的频次
   
       // 初始化 pCount 和 sCount 数组，统计 p 和 s 中前 pLen 个字符的频次
       for (int i = 0; i < pLen; ++i) {
           ++sCount[s.charAt(i) - 'a']; // 更新 sCount
           ++pCount[p.charAt(i) - 'a']; // 更新 pCount
       }
   
       // 如果初始窗口的字符计数与 pCount 相同，则添加 0 到结果中（表示第一个窗口就是一个异位词）
       if (Arrays.equals(sCount, pCount)) {
           ans.add(0);
       }
   
       // 开始滑动窗口，i 为窗口的左端点
       for (int i = 0; i < sLen - pLen; ++i) {
           // 窗口左边的字符移除，右边的新字符加入
           --sCount[s.charAt(i) - 'a']; // 左边的字符不在窗口中，减少频次
           ++sCount[s.charAt(i + pLen) - 'a']; // 右边的字符进入窗口，增加频次
   
           // 如果当前窗口的字符计数与 pCount 相同，说明是一个异位词，加入结果
           if (Arrays.equals(sCount, pCount)) {
               ans.add(i + 1); // 注意此时 i + 1 是新的窗口的起始索引
           }
       }
   
       return ans;
   }
   
   ```

3. 383 赎金信  -- **哈希map，利用key-value，也可以使用数组，用一个长度为26的数组来记录magazine里字母出现的次数，然后再用ransomNote去验证这个数组是否包含了ransomNote所需要的所有字母**

4. 349 两个数组的交集  -- 可以使用hashSet，因为Set集合是不允许重复的

5. 350 两个数组的交集II  -- 学会使用count--，==让key-value的value--==，而不是每次都增加，==学会先考虑数组的长度大小==，不是随便拿一个数组上来就遍历。

   

## day9：2025/1/14

### set、map、数组

1. 202 快乐数 -- 哈希set，这道题目**使用哈希法，来判断这个sum是否重复出现**，如果重复了就是return false， 否则一直找到sum为1为止。
2. 1 两数之和 -- 这道题已经做过很多次，但是依旧没有做出最优解。最优的解法，**需要map存放遍历过的元素和它的下标**。map目的用来存放我们访问过的元素，因为遍历数组的时候，需要记录我们之前遍历过哪些元素和对应的下标，这样才能找到与当前元素相匹配的（也就是相加等于target）

****

 	**在遍历数组的时候，只需要向map去查询是否有和目前遍历元素匹配的数值，如果有，就找到的匹配对，如果没有，就把目前遍历的	元素放进map中，因为map存放的就是我们访问过的元素。**

![image-20250114114219213](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250114114219213.png)

​	

```
//使用哈希表
public int[] twoSum(int[] nums, int target) {
    int[] res = new int[2];
    if(nums == null || nums.length == 0){
        return res;
    }
    Map<Integer, Integer> map = new HashMap<>();
    for(int i = 0; i < nums.length; i++){
        int temp = target - nums[i];   // 遍历当前元素，并在map中寻找是否有匹配的key
        if(map.containsKey(temp)){
            res[1] = i;
            res[0] = map.get(temp);
            break;
        }
        map.put(nums[i], i);    // 如果没找到匹配对，就把访问过的元素和下标加入到map中
    }
    return res;
}
```

3.  454四数之和II ---有四个相同长度的数组---**本题是使用哈希法的经典题目**

   我的一开始做法是比较错误的，时间复杂度达到O(n*4)，我的想法是，两个数组两个数组操作，但是用两个新的数组来保存相加的值。新的数组的大小就是lenxlen，这样在最后遍历的时候会达到O(n*4)，严重超时。最好的解法是哈希表，同样也是两两数组操作

   ```
   class Solution {
       public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
           int res = 0;
           Map<Integer, Integer> map = new HashMap<Integer, Integer>();
           //统计两个数组中的元素之和，同时统计出现的次数，放入map
           for (int i : nums1) {
               for (int j : nums2) {
                   int sum = i + j;
                   map.put(sum, map.getOrDefault(sum, 0) + 1);
               }
           }
           //统计剩余的两个元素的和，在map中找是否存在相加为0的情况，同时记录次数
           for (int i : nums3) {
               for (int j : nums4) {
                   res += map.getOrDefault(0 - i - j, 0);
               }
           }
           return res;
       }
   }
   ```

   

4. **==18 四数之和，比较难 ，不会写-- 一个数组==**

   **使用双指针**，五数之和、六数之和都可以使用这种解法

   ```
   public class Solution {
       public List<List<Integer>> fourSum(int[] nums, int target) {
           Arrays.sort(nums);  // 排序数组
           List<List<Integer>> result = new ArrayList<>();  // 结果集
           for (int k = 0; k < nums.length; k++) {
               // 剪枝处理
               if (nums[k] > target && nums[k] >= 0) {
                   break;
               }
               // 对nums[k]去重
               if (k > 0 && nums[k] == nums[k - 1]) {
                   continue;
               }
               for (int i = k + 1; i < nums.length; i++) {
                   // 第二级剪枝
                   if (nums[k] + nums[i] > target && nums[k] + nums[i] >= 0) {
                       break;
                   }
                   // 对nums[i]去重
                   if (i > k + 1 && nums[i] == nums[i - 1]) {
                       continue;
                   }
                   int left = i + 1;
                   int right = nums.length - 1;
                   while (right > left) {
                       long sum = (long) nums[k] + nums[i] + nums[left] + nums[right];
                       if (sum > target) {
                           right--;
                       } else if (sum < target) {
                           left++;
                       } else {
                           result.add(Arrays.asList(nums[k], nums[i], nums[left], nums[right]));
                           // 对nums[left]和nums[right]去重
                           while (right > left && nums[right] == nums[right - 1]) right--;
                           while (right > left && nums[left] == nums[left + 1]) left++;
                           right--;
                           left++;
                       }
                   }
               }
           }
           return result;
       }
       }
   
   ```

   

## day10：2025/1/15

### 双指针 --哈希表-- 字符串

1. 15 三数之和  -----双指针 -- 和四数之和比较类似  ，将三重循环转化为两重循环

   一层for循环，然后left、right指针 。==**首先将数组排序**，然后有一层for循环，**i从下标0的地方开始，同时定一个下标left 定义在i+1的位置上，定义下标right 在数组结尾的位置上。**==如果nums[i] + nums[left] + nums[right] > 0 就说明 此时三数之和大了，因为数组是排序后了，所以right下标就应该向左移动，这样才能让三数之和小一些。如果 nums[i] + nums[left] + nums[right] < 0 说明 此时 三数之和小了，left 就向右移动，才能让三数之和大一些，直到left与right相遇为止。

   ![image-20250115113015236](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250115113015236.png)

   ==去重逻辑的思考：==本题是**不能有重复的三元组，但三元组内的元素是可以重复的**

   a的去重：需要判断与前一位是否相等

   bc的去重：去重逻辑应该放在找到一个三元组之后，对b 和 c去重。

   ```
   class Solution {
       public List<List<Integer>> threeSum(int[] nums) {
           List<List<Integer>> result = new ArrayList<>();
           Arrays.sort(nums);
   	// 找出a + b + c = 0
           // a = nums[i], b = nums[left], c = nums[right]
           for (int i = 0; i < nums.length; i++) {
   	    // 排序之后如果第一个元素已经大于零，那么无论如何组合都不可能凑成三元组，直接返回结果就可以了
               if (nums[i] > 0) { 
                   return result;
               }
   
               if (i > 0 && nums[i] == nums[i - 1]) {  // 去重a
                   continue;
               }
   
               int left = i + 1;
               int right = nums.length - 1;
               while (right > left) {
                   int sum = nums[i] + nums[left] + nums[right];
                   if (sum > 0) {
                       right--;
                   } else if (sum < 0) {
                       left++;
                   } else {
                       result.add(Arrays.asList(nums[i], nums[left], nums[right]));
   		    // 去重逻辑应该放在找到一个三元组之后，对b 和 c去重
                       while (right > left && nums[right] == nums[right - 1]) right--;
                       while (right > left && nums[left] == nums[left + 1]) left++;
                       
                       right--; 
                       left++;
                   }
               }
           }
           return result;
       }
   }
   ```

### 总结

一般来说哈希表都是用来快速判断一个元素是否出现集合里。

对于哈希表，要知道**哈希函数**和**哈希碰撞**在哈希表中的作用。

==哈希函数：==，把传入的key映射到哈希表的索引上，主要是用hashcode转化为数值。

==哈希碰撞：==处理有多个key映射到相同索引上时的情景，处理碰撞的普遍方式是**拉链法**和**线性探测法**。

![image-20250115115131087](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250115115131087.png)

**==数组作为哈希表：==**使用map的空间消耗要比数组大一些，因为map要维护红黑树或者符号表，而且还要做哈希函数的运算。所以数组更加简单直接有效！

缺点：

- 数组的大小是有限的，受到系统栈空间（不是数据结构的栈）的限制。
- 如果数组空间够大，但哈希值比较少、特别分散、跨度非常大，使用数组就造成空间的极大浪费。

**==set作为哈希表：==**判断一个数是否重复出现过，set中不允许重复。

**==map作为哈希表：==**map是一种`<key, value>`的结构，在两数之和当中要求返回下标，所以可以用key保存数值，用value在保存数值所在的下标。



2.  344反转字符串  -- 使用双指针原地反转数组即可

   那么反转字符串依然是使用双指针的方法，只不过对于字符串的反转，其实要比链表简单一些。

   因为字符串也是一种数组，所以元素在内存中是连续分布，这就决定了反转链表和反转字符串方式上还是有所差异的。

   swap有两种实现：

   一种就是常见的交换数值：

   ```
   int tmp = s[i];
   s[i] = s[j];
   s[j] = tmp;
   
   ```

   一种就是通过位运算：

   ```
   s[i] ^= s[j];
   s[j] ^= s[i];
   s[i] ^= s[j];
   ```

   

3.  541反转字符串II  --**反转每个下标从 2*k* 的倍数开始的，长度为 *k* 的子串。若该子串长度不足 *k*，则反转整个子串**。

4. 151 翻转字符串里的单词  -- 三个重要的函数，**trim()、split("\\s+")**、**replaceAll("\\s+"," ")**

   ==trim()：==忽略字符串前后多余的空格

   ==split("\\s+")：==处理连续多个空格

   ==replaceAll("\\s+"," ")：==将中间多余的空白字符替换为只有一个空格

   但是要求使用空间复杂度为O(1)，不使用辅助空间：

   - 解题思路：

   - 移除多余的空格

   - 将整个字符串反转

   - 再将每个单词反转过来

   ```
   //移除字符串前后多余空格，再移除中间的多余空白字符（包括空格、制表符），替代为只有一个空格
   str.trim().replaceAll("\\s+"," ");
   ```

   

## day11：2025/1/16

### 字符串匹配 -- KMP

1. 28 找出字符串中第一个匹配项的下标  ----substring()函数---indexof()函数---   **但这道题是 ==<u>经典的KMP题目</u>==**，[具体可以看代码随想录](https://programmercarl.com/0028.%E5%AE%9E%E7%8E%B0strStr.html#%E6%80%9D%E8%B7%AF)

   我的做法：使用subsutring()截取文本串，然后截取的文本串与模式串作比较，找到第一个匹配的下标

   **但是这道题的核心思想是字符串匹配吗，下面就学习KMP**，**====KMP主要用于字符串匹配，在一个串中查找是否出现过另一个串==**

   KMP：文本串、模式串、最长相同前后缀，next[]数组也可以称为前缀表（**用来回退的，它记录了模式串与主串(文本串)不匹配的时候，模式串应该从哪里开始重新匹配**）

   1. 文章中字符串的==**前缀是指不包含最后一个字符的所有以第一个字符开头的连续子串**。==

   2. ==**后缀是指不包含第一个字符的所有以最后一个字符结尾的连续子串**。==

   3. ![image-20250116120903728](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250116120903728.png)

   4. 构造next数组，就是计算模式串s，前缀表的过程。可以不用整体右移或者整体减1，主要有三步：

      - 初始化
      - 前后缀不相同
      - 前后缀相同

      时间复杂度: O(n + m)

      空间复杂度: O(m)

      **==具体代码：==**

      ```
      class Solution {
          //前缀表（不减一）Java实现
          public int strStr(String haystack, String needle) {
              if (needle.length() == 0) return 0;
              int[] next = new int[needle.length()];
              getNext(next, needle);
      
              int j = 0;
              for (int i = 0; i < haystack.length(); i++) {
                  while (j > 0 && needle.charAt(j) != haystack.charAt(i)) 
                      j = next[j - 1];
                  if (needle.charAt(j) == haystack.charAt(i)) 
                      j++;
                  if (j == needle.length()) 
                      return i - needle.length() + 1;
              }
              return -1;
      
          }
          
          private void getNext(int[] next, String s) {
              int j = 0;
              next[0] = 0;
              for (int i = 1; i < s.length(); i++) {
                  while (j > 0 && s.charAt(j) != s.charAt(i)) 
                      j = next[j - 1];
                  if (s.charAt(j) == s.charAt(i)) 
                      j++;
                  next[i] = j; 
              }
          }
      }
      ```

      

   2. 459 重复的字符串  -- **==KMP算法==**

      - 前缀是指**不包含最后一个字符**的所有以第一个字符开头的连续子串；
      - 后缀是指**不包含第一个字符**的所有以最后一个字符结尾的连续子串；
      - next数组里，统计了各个位置为终点字符串的最长相同前后缀的长度。

      在这道题目中，需要检查一个字符串是否可以通过由它的一个子串重复多次构成。KMP算法非常适用于字符串匹配的做法，这道题求解步骤：

      1. 获取字符串next数组

      2. 判断next[length-1]是否为0，如果为0，说明不存在最长前后缀，那么肯定也不是由某个字串重复构成

      3. 如果不为0，则获取next[length-1]的值，说明这就是最长相同前后缀的长度

      4. **==如果一个字符串是由子串重复构成，则去掉最长相同前后缀的剩余子串就是组成这个大字符串的最小子串==**

      5. ==判断剩余子串长度是否能被大字符串长度整除，如果可以，返回true；如果不能，返回false；==，这地方就不用重新遍历字符串用substring这种了，直接在长度上进行比较；

      6. 关于上述证明的部分可以参考代码随想录。

         ![image-20250116152923105](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250116152923105.png)

   

### 总结

#### **要不要使用库函数：**

如果题目关键的部分直接用库函数就可以解决，建议不要使用库函数。

如果库函数仅仅是 解题过程中的一小部分，并且你已经很清楚这个库函数的内部实现原理的话，可以考虑使用库函数。

#### 双指针法：

双指针法在数组，链表和字符串中很常用。

#### 反转系列：

当需要固定规律一段一段去处理字符串的时候，要想想在在for循环的表达式上做做文章。

反转字符串中，只要让 i += (2 * k)，i 每次移动 2 * k 就可以了，然后判断是否需要有反转的区间。

翻转字符串里的单词中，通过先整体反转，再局部反转，实现整个反转；

反转字符串还有个作用是实现左旋的效果，主要是通过先局部反转再整体反转。

#### **KMP:**

KMP的主要思想是**当出现字符串不匹配时，可以知道一部分之前已经匹配的文本内容，可以利用这些信息避免从头再去做匹配了。**

使用KMP可以解决两类经典问题：

1. 匹配

2. 重复子串

   

## day12：2025/1/17

### 栈和队列

栈是先进后出，队列是先进先出

![image-20250117111324813](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250117111324813.png)

栈提供push 和 pop 等等接口，所有元素必须符合先进后出规则，所以栈不提供走访功能，也不提供迭代器(iterator)。 不像是set 或者map 提供迭代器iterator来遍历所有元素。

**栈是以底层容器完成其所有的工作，对外提供统一的接口，底层容器是可插拔的（也就是说我们可以控制使用哪种容器来实现栈的功能）。**

C++栈往往不被归类为容器，而被归类为container adapter（容器适配器），从下图中可以看出，栈的内部结构，**栈的底层实现可以是vector，deque，list 都是可以的， 主要就是数组和链表的底层实现。**

**==在Java中，实现栈有两个方法：一个是Java本身的集合类型Stack类型。另一个是借用LinkedList链表来间接实现栈==**（其实链表或者数组都可以间接实现一个栈的功能，LinkedList就是链表），Stack集合类型继承于Vector，由于Vector是通过数组实现的，所以Stack集合类型也是通过数组来实现的。
 平时的Stack就是指Stack集合类型。而不是栈这种更广泛的概念。

LinkedList是双向链表，不仅仅能用来实现栈，还可以被用来实现队列queue或者双端队列。是一个比较“全能”的数据结构。因为LinkedList实现了List接口，所以可以进行队列的操作，还实现了Deque接口，所及还能当做双端队列使用。

![image-20250117111000600](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250117111000600.png)



队列中先进先出的数据结构，==同样不允许有遍历行为，不提供迭代器,== **SGI STL中队列一样是以deque为缺省情况下的底部结构。**

也可以指定list 为起底层实现。

1. **232用栈实现队列 -- 定义两个栈，输入栈和输出栈**

   ==**java中栈的基本操作：**==

   - ==pop()：==弹出栈顶元素。
   - ==peek()：==查看栈顶元素，但不移除。
   - ==`push(E item)`：==将元素压入栈
   - ==isEmpty()==：检查栈为空
   - ==`search(Object o)`：==查找某个元素的位置（相对栈顶）
   - ==size()：==返回栈中元素的数量

2. **225用队列实现栈 -- 题目中要求用两个队列，那么设置一个栈和一个辅助栈**

   **==队列的基本操作：==**

   初始化一个队列通常是通过使用 `Queue` 接口的实现类来完成的。常用的实现类包括 `LinkedList` 和 `PriorityQueue`

   使用 `LinkedList` 初始化队列  `Queue<Integer> queue = new LinkedList<>();`

   - ==add(E e)或者offer(E e)：==向队列末尾添加元素

   - ==poll()或者remove()：==移除队列首元素并且返回

   - ==peek()：==查看队列头部元素

   - ==`isEmpty()`：==检查队列是否为空

   - `size()`：获取队列中元素的个数

   - `clear()`：清空队列

     

3. **20 有效的括号  -- 经典的括号匹配使用栈的问题**

   设置一个栈，如果当前遍历到的字符是[、（、或者{，栈中就存储匹配的字符）] }，

   **有三种情况不会匹配**

   1. 字符串中左方向的括号多余，所以不匹配

      ![image-20250117161336740](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250117161336740.png)

      2. 没有多余，但是括号的类型不匹配

      3. 右方向的括号多余

         ![image-20250117161441746](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250117161441746.png)

         代码：

         ```
         class Solution {
             public boolean isValid(String s) {
                 //判断空的字符串也是有效的
                 int length = s.length();
                 if (length == 0) return true;
         
                 if (length % 2 != 0) return false;
                 //只需要一个栈
                 Stack<Character> stack=new Stack<>();
                 for (int i = 0; i < length; i++) {
                     if(s.charAt(i)=='('){
                         stack.push(')');
                     }else if(s.charAt(i)=='{'){
                         stack.push('}');
                     }else if(s.charAt(i)=='['){
                         stack.push(']');
                     }else if(!stack.isEmpty()&&s.charAt(i)!=stack.peek()){ //没有多余，但是括号类型不匹配
                         return false;
                     }else if(stack.isEmpty()){ //判断在遍历过程中栈空了，说明右方向括号多余了
                         return false;
                     }else
                     {
                         stack.pop();//如果是与右方向括号匹配，那么出栈
                     }
                 }
                 if(!stack.isEmpty()) return false; //如果栈不为空，说明左方向括号多余了
                 return true; //最终栈为空，则括号匹配
             }
         }
         ```

         

         

4. **1047 删除字符串中所有相邻重复项**

   定义一个栈，用来存储遍历过的元素，如果当前遍历的元素与栈顶元素相同，则执行pop出栈操作，如果不相同，入栈，最终栈里剩余的元素就是不重复的，但此时还要对栈中元素出栈之后做个逆序，则得到最终的字符串。



## day13：2025/1/18

### 栈  --  队列 --  堆（优先级队列）-- 比较器的原理，重写compare方法，升序，降序

1. **150 逆波兰表达式求值 --** 

   用栈操作，遇到数字压入栈，遇到运算符，则弹出栈顶两个元素进行运算，并将运算结果压入栈

2.  **347 前k个高频元素** -- **==堆的典型问题，这道题使用堆，使用最小堆来实现优先级队列，优先级队列内部元素是自动依照元素的权值排列==**

   Java中默认使用**最小堆**（Min-Heap）来实现元素的优先级排序，堆就是完全二叉树。

   **堆是一棵完全二叉树，树中每个结点的值都不小于（或不大于）其左右孩子的值。** 如果父亲结点是大于等于左右孩子就是大顶堆，小于等于左右孩子就是小顶堆。

   所以大家经常说的大顶堆（堆头是最大元素），小顶堆（堆头是最小元素），如果懒得自己实现的话，就直接用priority_queue（优先级队列）就可以了，底层实现都是一样的，**从小到大排就是小顶堆，从大到小排就是大顶堆**。

   这道题应该是用大顶堆还是小顶堆呢，都可以，小顶堆的话因为要求给出前k个高频的元素，那么每次新的数值与堆头进行比较，如果是大于堆头，我们就移除堆头，将新的元素添加进来，这样最后就可以通过移除推头也就是不断移除当前堆里面的最小元素的方式来得到前k个高频的元素。

   **==定义优先级队列的方式：==**

   ```
   //定义优先级队列，里面的元素类型是整型数组，(pair1, pair2) -> pair1[1] - pair2[1]用lamba表达式的方式，设置升序排序的规则；如果pair1[1] - pair2[1]>0则说明pair2[1]比较小，pair2[1]排在pair1[1]前面，反之pair1[1]在pair2[1]前面，优先排比较小的元素，将元素按照升序进行排序。
   
   PriorityQueue<int[]> pq = new PriorityQueue<>((pair1, pair2) -> pair1[1] - pair2[1]);
   //原理其实是重写了compare()方法
   
   public int compare(int[] m, int[] n) {
                   return m[1] - n[1];
               }
   
   ```

   **==比较器的原理：==**

   这里面重写了Comparator接口当中的compare()方法，让`Comparator` 的 `compare(m, n)` 方法返回一个整数，这个整数决定了两个元素在队列中的顺序：

   **负数**：表示 `m` 排在 `n` 前面；

   **正数**：表示 `n` 排在 `m` 前面；

   **零**：表示 `m` 和 `n` 等同，顺序不变。

   **“排在前面”**：意思是，在队列的顺序中，某个元素被认为是 **优先级更高的元素**，所以它**会比其他元素更早被访问或者出队。**

   升序排序是说较小的元素比较早出队或者被访问，所以他的优先级比较高，所以它应该排在前面

   降序排序是说较大的元素比较早出队或者被访问，所以它的优先级比较高，所以它应该排在前面

   所以最后**`m[1] - n[1]`** 是 **升序** 排序，而 **`n[1] - m[1]`** 是 **降序** 排序。

   

   **==遍历map集合的方式：==**

   学会使用==entrySet()==方法，返回的是map集合里面所有的键值对返回到一个set集合里面，通过==getKey()==和==getValue()==获取键值对中相应的key和value

   ```
   //map.entrySet() 返回一个包含 Map 中所有键值对的 Set<Map.Entry<K, V>> 集合。这个集合的每个元素是一个 Map.Entry 对象，它包含了 Map 中的一个键值对。
   
     for (Map.Entry<Integer, Integer> entry : map.entrySet()) { //小顶堆只需要维持k个元素有序
               if (pq.size() < k) { //小顶堆元素个数小于k个时直接加
                   pq.add(new int[]{entry.getKey(), entry.getValue()});
               } else {
                   if (entry.getValue() > pq.peek()[1]) { //当前元素出现次数大于小顶堆的根结点(这k个元素中出现次数最少的那个)
                       pq.poll(); //弹出队头(小顶堆的根结点),即把堆里出现次数最少的那个删除,留下的就是出现次数多的了
                       pq.add(new int[]{entry.getKey(), entry.getValue()});
                   }
               }
           }
           
      //小顶堆，按照小顶堆遍历的方式是从小到大，但我们返回的结果是从大到小，所以是要逆序遍历     
      int[] ans = new int[k];
           for (int i = k - 1; i >= 0; i--) { //依次弹出小顶堆,先弹出的是堆的根,出现次数少,后面弹出的出现次数多
               ans[i] = pq.poll()[0];
           }
           return ans;
       }
   ```



## day14：2025/1/20

### **队列的经典应用 -- 滑动窗口的最大值**

1.  **239 滑动窗口最大值**  ---一般的想法都会超时 --- **==使用双端队列deque实现单调队列==**

   ==双端队列deque==

   `Deque` 是一个接口，**可以使用 LinkedList双向链表 来实现**或者 ArrayDeque动态数组 来实现，

   比如整型双端队列：`Deque<Integer> deque = new LinkedList<>();`

   **==双端队列的基本操作：==**

   `addFirst()`或者：将元素添加到队列的头部。

   `addLast()`或者add()：将元素添加到队列的尾部。

   `removeFirst()`或者remove()：移除并返回队列头部的元素。

   `removeLast()`：移除并返回队列尾部的元素。

   `peekFirst()`或者peek()：查看队列头部的元素，但不移除它。

   `peekLast()`：查看队列尾部的元素，但不移除它。

   

   如何使用双端队列实现单调队列，本题是找到移动中的滑动窗口最大值，**队列没有必要维护窗口里的所有元素，只需要维护有可能成为窗口里最大值的元素就可以了，同时保证队列里的元素数值是由大到小的。**滑动窗口移动过程中，滑动窗口移除最前面的元素，滑动窗口添加最后面的元素。

   而且**不要以为实现的单调队列就是 对窗口里面的数进行排序，如果排序的话，那和优先级队列又有什么区别了呢。**

   ```
   class MyQueue {
       Deque<Integer> deque = new LinkedList<>();
       //弹出元素时，比较当前要弹出的数值是否等于队列出口的数值，如果相等则弹出
       //同时判断队列当前是否为空
       void poll(int val) {
           if (!deque.isEmpty() && val == deque.peek()) {
               deque.poll();
           }
       }
       //添加元素时，如果要添加的元素大于入口处的元素，就将入口元素弹出
       //保证队列元素单调递减
       //比如此时队列元素3,1，2将要入队，比1大，所以1弹出，此时队列：3,2
       void add(int val) {
           while (!deque.isEmpty() && val > deque.getLast()) {
               deque.removeLast();
           }
           deque.add(val);
       }
       //队列队顶元素始终为最大值
       int peek() {
           return deque.peek();
       }
   }
   ```

   

### 总结 -- 栈和队列

#### 栈在系统中应用：

1. ==进入目录==：`cd a/b/c/../../`

系统进入a目录，这就是栈的应用

2. ==递归==：**递归的实现是栈：每一次递归调用都会把函数的局部变量、参数值和返回地址等压入调用栈中**，然后递归返回的时候，从栈顶弹出上一次递归的各项参数，所以这就是递归为什么可以返回上一层位置的原因。

括号匹配、字符串去重、逆波兰表达式求值

#### 队列的应用：

1. 求前k个高频元素：使用堆（不想自己手写实现的话可以使用优先级队列）
2. 滑动窗口最大值  - -使用deque来实现单调队列  `Deque<Integer> deque=new LinkedList<>();  `





## day15：2025/2/8

### 二叉树 --深度优先搜索--二叉树的递归遍历

**二叉树节点的定义**

```
  public class TreeNode {
      int val;
      TreeNode left;
      TreeNode right;
      TreeNode() {}
      TreeNode(int val) { this.val = val; }
      TreeNode(int val, TreeNode left, TreeNode right) {
          this.val = val;
          this.left = left;
          this.right = right;
      }
  }
```

==**List和Set区别**：**List是有序的，set是无序的！！！**==

==**`List`** 是 **有序** 的，元素按照插入的顺序存储，并且可以包含重复元素。==

==**`Set`** 是 **无序** 的，元素的顺序不固定，并且不允许重复元素。`HashSet` 是典型的无序实现，而 `LinkedHashSet` 是有序的（按插入顺序）。==

1. **144二叉树的前序遍历**  -- 采用递归逻辑

   ==**递归三要素：**==

   1. **确定递归函数的参数和返回值**
   2. **确定终止条件**
   3. **确定单层递归的逻辑**

   ```
   class Solution {
       public List<Integer> preorderTraversal(TreeNode root) {
   
           //采用递归遍历 前序遍历
           //存储结果
           List<Integer> result = new ArrayList<>();
           Traversal(root, result);
           return result;
       }
   
       //确定参数和返回类型
       //确定终止条件
       //确定单个递归逻辑
       private void Traversal(TreeNode cur, List<Integer> result) {
           //确定终止条件
           if (cur == null) return;
           //前序遍历
           //确定单层递归逻辑
           result.add(cur.val);
           Traversal(cur.left, result);
           Traversal(cur.right, result);
       }
   }
   ```

   

2. **145二叉树的后序遍历**  -- 采用递归逻辑

   ```
   class Solution {
       public List<Integer> postorderTraversal(TreeNode root) {
   
           List<Integer> result=new ArrayList<>();
           Traversal(root,result);
           return result;
   
       }
       private void Traversal(TreeNode cur,List<Integer> result){
           if(cur==null) return;;
           Traversal(cur.left,result);
           Traversal(cur.right,result);
           result.add(cur.val);
       }
   }
   ```

3. **二叉树的中序遍历  -- 采用递归逻辑**

   ```
   class Solution {
       public List<Integer> inorderTraversal(TreeNode root) {
           List<Integer> result = new ArrayList<>();
           Traversal(root, result);
           return result;
       }
   
       private void Traversal(TreeNode cur, List<Integer> result) {
           //中序遍历
           if (cur == null) return;
   
           Traversal(cur.left, result);
           result.add(cur.val);
           Traversal(cur.right, result);
       }
   }
   ```



## day16：2025/2/9

### 深度优先搜索--二叉树的迭代遍历--用栈来实现递归  -- 用Collections.reverse()反转

1. **144二叉树的前序遍历 -- 采用迭代遍历**

前序遍历采用迭代遍历，中左右

但在代码中，必须要先是右节点入栈，然后是左节点入栈，这样出栈的时候才能是中左右

`if (node.right != null) stack.push(node.right);`

`if (node.left != null) stack.push(node.left);`

```
//先是右节点入栈，这样出栈才会是左右
if (node.right != null) stack.push(node.right);
if (node.left != null) stack.push(node.left);
```

```

//迭代遍历
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {

        //迭代遍历
        //前序遍历  中左右
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();

        if (root == null) return result;
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            //中 入栈
            result.add(node.val);
            //先是右节点入栈，这样出栈才会是左右
            if (node.right != null) stack.push(node.right);
            //再是左节点入栈
            if (node.left != null) stack.push(node.left);

        }
        return result;
    }
}

```



2.**94 二叉树的中序遍历 -- 采用迭代遍历**

中序遍历是左中右，先访问的是二叉树顶部的节点，然后一层一层向下访问，直到到达树左面的最底部，再开始处理节点（也就是在把节点的数值放进result数组中），这就造成了**处理顺序和访问顺序是不一致的。**

```

//迭代遍历
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();

        Stack<TreeNode> stack = new Stack<>();

        TreeNode cur = root; //借用指针的遍历来帮助访问节点

        if(root==null) return result;
        //中序遍历 左中右
        //迭代遍历
        while (cur != null || !stack.isEmpty()) {
            if (cur != null) {//沿着根部左节点访问
                stack.push(cur);//访问的节点入栈，空节点不入栈
                cur = cur.left;//沿着根部往左走,一直走到最下面
            } else {
                cur = stack.pop();//栈中顶部节点弹出栈，指针指向这
                result.add(cur.val);
                cur = cur.right;//访问当前节点的右子节点
            }

        }
        return result;
    }

}

```



3. **145 二叉树的后序遍历 -- 迭代遍历**

**==java中反转的方法：Collections.reverse();==**

后序遍历：左右中

可以通过调整前序遍历来实现后序遍历

中左右--》中右左--》左右中

```

//迭代遍历
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        //后序遍历  左右中
        List<Integer> result = new ArrayList<>();

        Stack<TreeNode> stack = new Stack<>();

        if (root == null) return result;
        stack.push(root);

        //先是中右左
        while (!stack.isEmpty()) {
            //入栈顺序
            TreeNode node = stack.pop();
            result.add(node.val);
            //入栈顺序 左右
            if (node.left != null) stack.push(node.left);
            if (node.right != null) stack.push(node.right);
        }
        //现在得到了中右左
        //下面进行反转 ---> 左右中
        Collections.reverse(result);
        return result;
    }
}

```



## day17：2025/2/10

### 广度优先搜索 --  二叉树的层序遍历

1. **102 二叉树的层序遍历 ** -- **==很重要，作为一个模板==**

   

   ```
   //二叉树的层序遍历
   class Solution {
   
       public List<List<Integer>> levelOrder(TreeNode root) {
           //存储结果
           List<List<Integer>> result=new ArrayList<>();
           if(root==null) return result;
           //定义队列
           Queue<TreeNode> queue=new LinkedList<>();
           //根部节点入队
           queue.offer(root);
           
           while(!queue.isEmpty()){
               List<Integer> itemResult=new ArrayList<>();
               int len = queue.size();
               while (len>0){
   
                   TreeNode node = queue.poll();
                   itemResult.add(node.val);
                   if(node.left!=null) queue.offer(node.left);
                   if(node.right!=null) queue.offer(node.right);
                   len--;
               }
               result.add(itemResult);
           }
           return result;     
       }
   }
   
   ```

2. **107 二叉树的层序遍历II -- 自底向上的层序遍历，根据上面的层序遍历完之后再反转集合即可。**

3. **199 二叉树的右视图  -- 所谓的右视图，就是指每个单层的最后一个元素，所以在层序遍历的时候判断是否遍历到单层的最后一个元素，如果是则加入到结果集合中。**

   ![image-20250210142449010](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250210142449010.png)

   ```
   
   class Solution {
       public List<Integer> rightSideView(TreeNode root) {
   
           List<Integer> result=new ArrayList<>();
           Queue<TreeNode> queue=new LinkedList<>();
           //LinkedList 在插入 null 元素时不会报错，而 ArrayDeque 则 不允许 向队列中插入 null 元素。
           if(root==null) return result;
           queue.offer(root);
           while(!queue.isEmpty()){
               int size = queue.size();
   
               //所谓的右视图其实就是单层的最后一个元素
               //层序遍历的时候判断是否遍历到单层的最后一个元素
               //如果是，那么加入result集合
               while (size>0){
                   TreeNode node = queue.poll();
                   if(node.left!=null) queue.offer(node.left);
                   if(node.right!=null) queue.offer(node.right);
                   size--;
                   if(size==0){
                       result.add(node.val);
                   }
               }
           }
           return result;
   
       }
   }
   ```

4. **637 二叉树的层平均值**

5. **429 N叉树的层序遍历**

   ```
   
   class Solution {
       public List<List<Integer>> levelOrder(Node root) {
   
           List<List<Integer>> result = new ArrayList<>();
           Queue<Node> queue = new LinkedList<>();
   
           if (root == null) return result;
   
           queue.offer(root);
   
           while (!queue.isEmpty()) {
               List<Integer> itemresult = new ArrayList<>();
               int size = queue.size();
   
               for (int i = 0; i < size; i++) {
   
                   Node node = queue.poll();
                   itemresult.add(node.val);
   
                   List<Node> children = node.children;
                   
                   if (children == null || children.size() == 0) continue;//注意这个地方，continue执行之后还是会执行for循环的i++，使用//while(size>0)那个逻辑这一块必须先写size--再写continue；
                   
                   for (Node child : children) {
                       if (child != null) queue.offer(child);
                   }
               }
               result.add(itemresult);
           }
           return result;
       }
   }
   ```

6. **515 在每个树行中找最大值  -- 就是求每一层的最大值**

7. **116 填充每个节点的下一个右侧节点指针**
8. **117 填充每个节点的下一个右侧节点指针II**   --- 和116解法代码一样

9. **104 二叉树的最大深度  -- ==采用层序遍历求解二叉树的最大深度即可==**

   **==也可以采用递归解法，使用的是递归后序遍历，后序遍历相当于沿着根节点找到最左节点，然后一点一点回溯往上==**

   也可以使用递归法求前序遍历

   ```
   class Solution {
       /**
        * 递归法  后序遍历
        */
       public int maxDepth(TreeNode root) {
           if (root == null) {
               return 0;
           }
           int leftDepth = maxDepth(root.left);
           int rightDepth = maxDepth(root.right);
           return Math.max(leftDepth, rightDepth) + 1;
       }
   }
   ```

   

   ```
   
   class Solution {
       public int maxDepth(TreeNode root) {
           //采用层序遍历
           Queue<TreeNode> queue = new ArrayDeque<>(); //这个地方应该想一想实现Queue接口，使用ArrayDeque和LinkedList到底有什么区别，//leetcode上一些队列的基本实现采用的是LinkedList
           //LinkedList 在插入 null 元素时不会报错，而 ArrayDeque 则 不允许 向队列中插入 null 元素。
           if (root == null) return 0;
           queue.offer(root);
           int sum=0;
           while (!queue.isEmpty()) {
               int size = queue.size();
               while (size > 0) {
                   TreeNode node = queue.poll();
                   if (node.left != null) queue.offer(node.left);
                   if (node.right != null) queue.offer(node.right);
                   size--;
               }
               sum++;
           }
           return sum;
       }
   }
   ```

   

10. **111 二叉树的最小深度 -- 需要注意的是，当左右孩子节点均为空的时候，说明遍历到最低节点了**

    **==也可以采用递归解法，使用的是递归后序遍历，后序遍历相当于沿着根节点找到最左节点，然后一点一点回溯往上==**

    但是与上述求解最大深度不同的是，对于最小深度的定义，如果左右孩子有一个为空时，那么最小深度并不是1，而是1+另一个子树的最小深度

    ```
    class Solution {
    	public int minDepth(TreeNode root){
    		int leftDepth=minDepth(root.left);
    		int rightDepth=minDepth(root.right);
    		
    		//如果左子树为空，右子树不为空
    		if(root.left==null&&root.right!=null){
    			return 1+rightDepth;
    		}
    		//如果右子树为空，左子树不为空
    		if(root.right==null&&root.left!=null){
    			return 1+leftDepth;
    		}
    		int result=1+Math.min(leftDepth,rightDepth);
    		return result;
    	}
    }
    
    ```

    

    ```
    
    class Solution {
        public int minDepth(TreeNode root) {
            //采用层序遍历
            Queue<TreeNode> queue = new ArrayDeque<>();//这个地方应该想一想实现Queue接口，使用ArrayDeque和LinkedList到底有什么区别
            //LinkedList 在插入 null 元素时不会报错，而 ArrayDeque 则 不允许 向队列中插入 null 元素。
            
            if (root == null) return 0;
            queue.offer(root);
            int sum = 0;
            List<Integer> result = new ArrayList<>();
            while (!queue.isEmpty()) {
            
                int size = queue.size();
                sum++;
                while (size > 0) {
                    TreeNode node = queue.poll();
                    if (node.left != null) queue.offer(node.left);
                    if (node.right != null) queue.offer(node.right);
                    if (node.left == null && node.right == null) {
    
                        result.add(sum);
                    }
                    size--;
                }
            }
            Integer min = Collections.min(result);
            return min;
        }
    }
    ```

    

## day18：2025/2/11

### **翻转二叉树！！**建议抓住本质 -- 对称二叉树

1. **==226 翻转二叉树 -- 把每个节点的左右孩子交换一下就可以 -- 这道题很重要！！！==**

   选择的方法：递归法前序遍历、递归法后序遍历、迭代法前序遍历、层序遍历；注意的是不能用中序遍历，因为中序遍历会将左右孩子节点翻转两次

   **递归法前序遍历**

   ```
   
   class Solution {
       public TreeNode invertTree(TreeNode root) {
           //使用递归的方法前序遍历
           if(root==null) return null;
           invertTreeRoot(root);
           return root;
       }
       private void invertTreeRoot(TreeNode node){
           if(node==null) return;
   
           //交换左右孩子节点
           TreeNode temp=node.left;
           node.left=node.right;
           node.right=temp;
           //翻转左子树
           invertTreeRoot(node.left);
           //翻转右子树
           invertTreeRoot(node.right);
       }
   }
   ```

   **迭代法前序遍历**

   ```
   public TreeNode invertTree(TreeNode root){
           if(root==null) return null;
           Stack<TreeNode> stack=new Stack<>();
   
           stack.push(root);
           while(!stack.isEmpty()){
               TreeNode node = stack.pop();
               //交换左右孩子节点
               TreeNode temp=node.left;
               node.left=node.right;
               node.right=temp;
               //翻转右子树
               if(node.right!=null) stack.push(node.right);
               //翻转左子树
               if(node.left!=null) stack.push(node.left);
   
           }
           return root;
   
       }
   ```

   **层序遍历**

   ```
   public TreeNode invertTree(TreeNode root){
           if(root==null) return null;
           Queue<TreeNode> queue=new ArrayDeque<>();//这个地方应该想一想实现Queue接口，使用ArrayDeque和LinkedList到底有什么区别
           //LinkedList 在插入 null 元素时不会报错，而 ArrayDeque 则 不允许 向队列中插入 null 元素。
           queue.offer(root);
           while(!queue.isEmpty()){
               int size = queue.size();
               while (size>0){
                   TreeNode node = queue.poll();
                   //交换左右孩子节点
                   TreeNode temp=node.left;
                   node.left=node.right;
                   node.right=temp;
                   //翻转左子树
                   if(node.left!=null) queue.offer(node.left);
                   //翻转右子树
                   if(node.right!=null) queue.offer(node.right);
                   size--;
               }
           }
           return root;
       }
   ```

   

2. **101 对称二叉树 --** 本质就是，两棵树，判断一棵树翻转过去是不是与另外一棵树完全相同

   **==关于采用LinkedList实现Queue接口和采用ArrayDeque实现Queue接口的区别：==**

   `LinkedList` 在插入 `null` 元素时不会报错，而 **`ArrayDeque`** 则 **不允许** 向队列中插入 `null` 元素。

   **使用栈也是一样的，就是把队列换成栈就行**

   ```
   
   class Solution {
       public boolean isSymmetric(TreeNode root) {       
           //镜像二叉树
           //在根节点的左右子树，比较左子树的左节点和右子树的右节点，比较左子树的右节点和右子树的左节点
           //使用队列,迭代法
           Queue<TreeNode> queue = new LinkedList<>();
           //LinkedList 在插入 null 元素时不会报错，而 ArrayDeque 则 不允许 向队列中插入 null 元素。
           
           if (root == null) return true;
           queue.offer(root.left);
           queue.offer(root.right);
   
           while (!queue.isEmpty()) {
               TreeNode pollleft = queue.poll();
               TreeNode pollright = queue.poll();
               //判断返回false的情况
               if (pollleft == null && pollright == null) continue;
               if (pollleft == null || pollright == null || pollleft.val != pollright.val) return false;
               
               queue.offer(pollleft.left);//左子树的左孩子
               queue.offer(pollright.right);//右子树的右孩子
               queue.offer(pollleft.right);//左子树的右孩子
               queue.offer(pollright.left);//右子树的左孩子
           }
           return true;
       }
   }
   ```

   

3. **100 相同的树  -- 与上一题的解法类似**

4. **572 另一棵树的子树 -- 这道题能看懂的解法是dfs+暴力求解 -- 深度优先搜索枚举 *s* 中的每一个节点，判断这个点的子树是否和 *t* 相等**

   

   ```
   	public boolean isSubtree(TreeNode root, TreeNode subRoot) {
           return  dfs(root,subRoot);
       }
   
       private boolean dfs(TreeNode s, TreeNode t) {
           if (s == null) return false;
           return check(s,t)||dfs(s.left,t)||dfs(s.right,t);
       }
   
       private boolean check(TreeNode cur,TreeNode subcur){
           Queue<TreeNode> queue = new LinkedList<>();
           if (cur == null && subcur == null) return true;
           if (cur == null || subcur == null || cur.val != subcur.val) return false;
           queue.offer(cur);
           queue.offer(subcur);
           while (!queue.isEmpty()) {
               TreeNode node1 = queue.poll();
               TreeNode node2 = queue.poll();
               if (node1 == null && node2 == null) continue;
               //判断为false的情况
               if (node1 == null || node2 == null || node1.val != node2.val) return false;
               queue.offer(node1.left);
               queue.offer(node2.left);
               queue.offer(node1.right);
               queue.offer(node2.right);
           }
           return true;
       }
   ```

   关于check的部分，用递归实现比较简单

   ```
   private boolean check(TreeNode cur,TreeNode subcur){
   	if(cur==null&&subcur==null) return true;
   	if(cur==null||subcur==null||cur.val!=subcur.val) return false;
   	return check(cur.left,subcur.left)&&check(cur.right,subcur.right);
   }
   ```

   

## day19：2025/2/12

### 二叉树的节点个数 -- 二叉树的所有路径  - -平衡二叉树 -- 二叉树的所有左叶子之和

1. **222 完全二叉树的节点个数     两种解法：1.  层序遍历记录节点数     2. 采用递归算法进行后序遍历**

   ```
   
   class Solution {
       public int countNodes(TreeNode root) {
   
   /*        //先采用层序遍历
           if (root == null) return 0;
           int count = 0;
           Queue<TreeNode> queue = new LinkedList<>();
           queue.offer(root);
           while (!queue.isEmpty()) {
   
               int size = queue.size();
               while (size > 0) {
                   TreeNode node = queue.poll();
                   count++;
                   if (node.left != null) queue.offer(node.left);
                   if (node.right != null) queue.offer(node.right);
                   size--;
               }
           }
           return count;*/
   
           //递归 后序遍历
           //二叉树的节点个数=左子树节点个数+右子树节点个数+1（这个1指的是中节点）
           if (root == null) return 0;
           int leftnum = countNodes(root.left);
           int rightnum = countNodes(root.right);
           int result = leftnum + rightnum + 1;
           return result;
       }
   }
   ```

2. ==**110平衡二叉树   -- 一棵高度平衡二叉树定义为：一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。*-- 递归算法常看***==

   求高度，还是从后序遍历入手，采用递归的方法

   强调**二叉树节点的高度和二叉树节点的深度的概念**：

   ![image-20250212140049124](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250212140049124.png)

   ```
   
   class Solution {
       public boolean isBalanced(TreeNode root) {
   
           //这道题采用dfs
           //后序遍历
           if (root == null) return true;
           //左右子树求高度
           int result = dfs(root);
           return result == -1 ? false : true;
       }
   
       private int dfs(TreeNode root) {
           if (root == null) return 0;
           int leftheight = dfs(root.left);
           //为什么要设置返回-1呢，因为递归的出口设置的是return 0，后面如果再设置0的话，就无法判断是正常递归到叶子节点还是本身就要返回
           //false的情况了，所以这个地方应该换一个数字
           if (leftheight == -1) return -1;
           
           int rightheight = dfs(root.right);
           
           if (rightheight == -1) return -1;
           
           return Math.abs(leftheight - rightheight) > 1 ? -1 : Math.max(leftheight, rightheight) + 1;
           //return Math.max(leftheight, rightheight) + 1;
   
       }
   }
   ```

   

3. ==**257 二叉树的所有路径 -- dfs--递归前序遍历  -- 回溯+递归，这道题简单题但我没有完全理解！！**==

   **回溯和递归是一一对应的，有一个递归，就要有一个回溯**

   ```
   //这道题是只需要判断到叶子节点进行return，而不是判断到空节点return
   class Solution {
       public List<String> binaryTreePaths(TreeNode root) {
   
           List<String> result = new ArrayList<>();
           if (root == null) return result;
           //递归前序遍历
           //构造一个路径集合，加入
           List<Integer> path = new ArrayList<>();
           dfs(root, result, path);
           return result;
       }
   
       private void dfs(TreeNode root, List<String> result, List<Integer> path) {
   
           path.add(root.val);//中
           if (root.left == null && root.right == null) {
               //当前遍历到了叶子节点
               StringBuilder stringBuilder = new StringBuilder();
               for (int i = 0; i < path.size() - 1; i++) {
                   stringBuilder.append(path.get(i)).append("->");
               }
               stringBuilder.append(path.get(path.size() - 1));
               result.add(stringBuilder.toString());//收集路径
               return;
           }//对中间节点
           
           if (root.left != null) {
               dfs(root.left, result, path);
               path.remove(path.size() - 1); //左
   
           }
           if (root.right != null) {
               dfs(root.right, result, path);
               path.remove(path.size() - 1); // 右
           }
       }
   }
   ```

   

4. **404 返回所有左叶子之和**   -- **用迭代法吧，自己写出来的是用迭代法**

   dfs -- 递归

   ```
   
   class Solution {
       public int sumOfLeftLeaves(TreeNode root) {
           //后序遍历
           //递归算法
           if (root == null) return 0;
           int leftvalue = sumOfLeftLeaves(root.left);
           int rightvalue = sumOfLeftLeaves(root.right);
   
           //遍历左子树左叶子
           //遍历右子树左叶子
           //遍历左右子树都是一样的做法，重点是判断左叶子节点，判断父节点的左叶子节点
           //一个根的左叶子之和等于左右子树的左叶子之和
           int temp = 0;
           if (root.left != null && root.left.left == null && root.left.right == null) {
               temp = root.left.val;
           }
           return temp + leftvalue + rightvalue;
   
       }
   }
   ```

   **dfs -- 迭代--这种方法更好理解也更好写出来，这是自己写出来的**

   ```
   
   class Solution {
       public int sumOfLeftLeaves(TreeNode root) {
           if (root == null) return 0;
           //用迭代法求解
           //前序遍历
           Stack<TreeNode> stack=new Stack<>();
           stack.push(root);
           int sum=0;
           while (!stack.isEmpty()){
               TreeNode node = stack.pop();
               if(node.left!=null&&node.left.left==null&&node.left.right==null){
                   sum+=node.left.val;
               }
               
               if(node.right!=null) stack.push(node.right);
   
               if(node.left!=null) stack.push(node.left);
           }
           return sum;
   
       }
   }
   ```

   



## day20：2025/2/13

### 路径总和-- 构造二叉树

**前序和后序不能唯一确定一棵二叉树！**，因为没有中序遍历无法确定左右部分，也就是无法分割。

1. **513 找树左下角的值**

   这道题我利用的是bfs层序遍历，这种方法我比较好理解也比较简洁易懂。只需要在层序遍历当中添加一部分逻辑就行

   ```
   class Solution {
       public int findBottomLeftValue(TreeNode root) {
           //采用层序遍历
           if (root == null) return 0;
           Queue<TreeNode> queue = new LinkedList<>();
           queue.offer(root);
           int temp = 0;
           int result = 0;
           while (!queue.isEmpty()) {
               int size = queue.size();
               for (int i = 0; i < size; i++) {
                   TreeNode node = queue.poll();
                   if (i == 0) temp = node.val;
                   if (node.left != null) queue.offer(node.left);
                   if (node.right != null) queue.offer(node.right);
               }
               if (queue.isEmpty()) result = temp;
           }
           return result;
       }
   }
   ```

   

2. **112 路径总和 -- 这道题的解题思路与 ==257二叉树所有路径==的解题思路一致 ，找出根节点到叶子节点的所有路径计算路径和**

   ```
   
   class Solution {
       public boolean hasPathSum(TreeNode root, int targetSum) {
           //这道题与昨天做的找出二叉树所有路径的题目类似，只不过增加了计算路径和的逻辑
           if (root == null) return false;
           List<Integer> path = new ArrayList<>();
           return dfs(root,targetSum,path);
       }
       private boolean dfs(TreeNode root, int targetSum, List<Integer> path) {
           //前序遍历
           path.add(root.val);
           if (root.left == null && root.right == null) {
               int sum = 0;
               for (int i = 0; i < path.size(); i++) {
                   sum += path.get(i);
               }
               if (sum == targetSum) return true;
           }
           if (root.left != null) {
               boolean result = dfs(root.left, targetSum, path);
               if (result) return true;
               path.remove(path.size() - 1);
           }
           if (root.right != null) {
               boolean result = dfs(root.right, targetSum, path);
               if (result) return true;
               path.remove(path.size() - 1);
           }
           return false;
       }
   }
   ```

   

3. **113路径总和ii -- 跟上述的思路一样，只不过将所有的路径给找出来**

   ==里面有一个注意点： result.add(new ArrayList<>(path)); 和 result.add(path)不同==

   ==应该使用result.add(new ArrayList<>(path))==

   **==`result.add(path)`，会将 `path` 列表的引用直接添加到 `result` 中。这意味着 `result` 中保存的实际上是对同一个 `path` 列表的引用，而不是它的副本。然而，`path` 在递归过程中会不断被修改（即，路径会添加节点的值，在回溯时移除节点的值）。==**这就意味着，如果你在遍历左子树和右子树的过程中使用 `result.add(path)`，所有的路径都会指向同一个 `path` 列表，并且随着递归的进行，`path` 会不断改变，导致 `result` 中的路径也会发生变化。

   ```
   
   class Solution {
       public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
           //112路径之和是判断有没有存在，这个是判断有没有并且把所有路径找出来
           //一样的思路
           List<List<Integer>> result = new ArrayList<>();
           if (root == null) return result;
           List<Integer> path = new ArrayList<>();
           dfs(root, targetSum, path, result);
           return result;
       }
   
       private void dfs(TreeNode root, int targetSum, List<Integer> path, List<List<Integer>> result) {
   
           path.add(root.val);
           //前序遍历
           //递归终止的条件
           if (root.left == null && root.right == null) {
               int sum = 0;
               for (int i = 0; i < path.size(); i++) {
                   sum += path.get(i);
               }
               if (sum == targetSum) {
                   result.add(new ArrayList<>(path));
               }
               return;
           }
           if (root.left != null) {
               dfs(root.left, targetSum, path, result);
               path.remove(path.size() - 1);
           }
           if (root.right != null) {
               dfs(root.right, targetSum, path, result);
               path.remove(path.size() - 1);
           }
   
   
       }
   
   }
   ```

   



4. ==**106 从中序遍历和后序遍历序列构造二叉树 -- 而且是唯一二叉树**==

   **所谓区间左闭右开，指的是索引会不会指向区间端点值，如果指向就是闭，不指向就是开**

   以 后序数组的最后一个元素为切割点，先切中序数组，根据中序数组，反过来再切后序数组。一层一层切下去，每次后序数组最后一个元素就是节点元素。

   大概步骤就是

   1. 找到后序数组的最后一个节点就是根节点
   2. 根据找到的根节点切割中序数组，分为中序左数组和中序右数组
   3. 根据中序左数组和右数组在后序中找到后序左数组和后序右数组
   4. 递归遍历中序左数组，后序左数组
   5. 递归遍历中序右数组，后序右数组
   6. 递归的终止条件是区间左端点>=右端点，因为区间控制的是左闭右开

   ```
   class Solution {
       Map<Integer,Integer> map=new HashMap<>();
       public TreeNode buildTree(int[] inorder, int[] postorder) {
           //根据中序遍历和后序遍历唯一构造一颗二叉树
           for (int i = 0; i < inorder.length; i++) {
               map.put(inorder[i],i);
           }
           //区间是左闭右开
            return build(inorder,0,inorder.length,postorder,0,postorder.length);
       }
       private TreeNode build(int[] inorder,int inbegin,int inend,int[] postorder,int postbegin,int postend){
           //左闭右开
           //递归终止条件
           if(inbegin>=inend||postbegin>=postend){
               return null;
           }
           //从后序中找到根节点在中序中的位置索引
           Integer index = map.get(postorder[postend - 1]);
           TreeNode root=new TreeNode(postorder[postend-1]);
           
           int lengthleft=index-inbegin;
           //递归遍历中序左子树后序左子树
           root.left=build(inorder,inbegin,index,postorder,postbegin,postbegin+lengthleft);
   
           //递归中序右子树 后序右子树
           root.right=build(inorder,index+1,inend,postorder,postbegin+lengthleft,postend-1);
   
           return root;
       }
   }
   ```

   

5. **105 从前序序列和中序序列构造唯一二叉树**

   逻辑思路和上述相同，但注意判断递归中起始

   preorder, ==prebegin + 1==, ==prebegin + leftlength+1==, inorder, inbegin, rootindex

   上述两个相减必须得是leftlength啊

   preorder, prebegin + leftlength+1, preend, inorder, rootindex + 1, inend

           root.left = build(preorder, prebegin + 1, prebegin + leftlength+1, inorder, inbegin, rootindex);
           //前序序列的右子树，中序序列的右子树
           root.right = build(preorder, prebegin + leftlength+1, preend, inorder, rootindex + 1, inend);

   ```
   
   class Solution {
       //构造哈希表
       private Map<Integer, Integer> map = new HashMap<>();
       public TreeNode buildTree(int[] preorder, int[] inorder) {
           //前序序列中第一个为根节点
           for (int i = 0; i < inorder.length; i++) {
               map.put(inorder[i], i);
           }
           return build(preorder, 0, preorder.length, inorder, 0, inorder.length);
   
       }
   
       private TreeNode build(int[] preorder, int prebegin, int preend, int[] inorder, int inbegin, int inend) {
           //区间还是左闭右开
           if (prebegin >= preend || inbegin >= inend) return null;
   
           final Integer rootindex = map.get(preorder[prebegin]);
           //构造根节点
           TreeNode root = new TreeNode(inorder[rootindex]);
           int leftlength = rootindex - inbegin;
           //前序序列的左子树，中序序列的左子树
           root.left = build(preorder, prebegin + 1, prebegin + leftlength+1, inorder, inbegin, rootindex);
           //前序序列的右子树，中序序列的右子树
           root.right = build(preorder, prebegin + leftlength+1, preend, inorder, rootindex + 1, inend);
           return root;
       }
   
   }
   ```

   

6. **654 最大二叉树 --** **==类似用数组构造二叉树的题目，每次分隔尽量不要定义新的数组，而是通过下标索引直接在原数组上操作，这样可以节约时间和空间上的开销。==**

   ```
   
   class Solution {
       private Map<Integer, Integer> map = new HashMap<>();
   
       public TreeNode constructMaximumBinaryTree(int[] nums) {
           for (int i = 0; i < nums.length; i++) {
               map.put(nums[i], i);
           }
           return maxTree(0, nums.length, nums);
       }
       //递归的算法
       private TreeNode maxTree(int begin, int end, int[] nums) {
   
           if (begin >= end) return null;
           int max = nums[begin];
           for (int i = begin; i < end; i++) {
               if (nums[i] > max) max = nums[i];
           }
           //构造节点
           TreeNode root = new TreeNode(max);
           //找到最大值所在的索引
           final Integer maxindex = map.get(max);
           //递归左边
           root.left = maxTree(begin, maxindex, nums);
           //递归右边
           root.right = maxTree(maxindex + 1, end, nums);
           return root;
       }
   }
   ```

   



## day21：2025/2/14

### 二叉搜索树  -- result.stream().mapToInt(Integer::intValue).toArray()

1. **617 合并二叉树** 

   ==**如果一个父节点的左节点为空，另一个树的父节点的左节点不为空，这个时候要合并的话怎么操作呢，利用指针的特性**==

   ==**node1.left=node2.left;**==

   ==**上述就是指针赋值，那么连带着下面的子树都被赋值过去了**==

   ```
   class Solution {
       public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
           //以root1作为基准树
           if (root1 == null && root2 == null) return root1;
           if (root1 == null && root2 != null) return root2;
           if (root1 != null && root2 == null) return root1;
           Queue<TreeNode> queue = new LinkedList<>();
           queue.offer(root1);
           queue.offer(root2);
           while (!queue.isEmpty()) {
               TreeNode node1 = queue.poll();
               TreeNode node2 = queue.poll();
               node1.val = node1.val + node2.val;
               //这里面控制入队列的条件是：当两个树的左右子节点均存在的时候入队列
               if (node1.left != null && node2.left != null) {
                   queue.offer(node1.left);
                   queue.offer(node2.left);
               }
               if (node1.right != null && node2.right != null) {
                   queue.offer(node1.right);
                   queue.offer(node2.right);
               }
               //两种情况 1. 树1要么左节点为空，
               //2. 树1要么右节点为空
   
               if (node1.left == null && node2.left != null) {
                   node1.left = node2.left;//直接赋值，节点指针赋值
               }
               if (node1.right == null && node2.right != null) {
                   node1.right = node2.right;//直接赋值，节点指针赋值
               }
   
           }
           return root1;
   
       }
   
   }
   ```

   

2. ==**700 二叉搜索树的搜索 -- 利用二叉搜索树(BST)的特性进行遍历**==

**二叉搜索树是一个有序树：**

- 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；
- 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；
- 它的左、右子树也分别为二叉搜索树

这就决定了，二叉搜索树，递归遍历和迭代遍历和普通二叉树都不一样。

**在二叉搜索树中找到某个值，并返回以这个值为节点根子树**

**迭代遍历  -- 不需要栈和队列**

如果当前值小于目标值，那么向右遍历

如果当前值大于目标值，那么向左遍历

```
        while (root != null) {
            if (root.val > val) root = root.left;
            else if (root.val < val) root = root.right;
            else return root;
        }
        return null;
```

递归遍历

```

       //使用递归法也可以
        TreeNode result=null;
        if(root==null||root.val==val) return root;
        if(root.val>val) {
             result=searchBST(root.left,val);
        }
        else if(root.val<val){
             result=searchBST(root.right,val);
        }
        return result;
```



3. **98 验证二叉搜索树 ，验证一棵树是不是二叉搜索树(BST)**

我的做法是比较一般的做法，就是利用中序遍历得到结果，如果是二叉搜索树，那么序列是个递增有序序列

遍历中序序列，如果后一个值大于等于前一个值，那么就不是二叉搜索树

```

class Solution {
    public boolean isValidBST(TreeNode root) {

        //利用中序遍历，存放结果
        List<Integer> result=new ArrayList<>();
        inorder(root,result);
        for (int i = 0; i < result.size()-1; i++) {
            if(result.get(i+1)<=result.get(i)) return false;
        }
        return true;
    }
    private void inorder(TreeNode root,List<Integer> result){
        //中序遍历 左中右
        if(root==null) return;;
        inorder(root.left,result);
        result.add(root.val);
        inorder(root.right,result);
    }
}
```

4. **530 二叉搜索树中的最小绝对差**

   利用二叉搜索树的性质：我的做法是中序遍历得到有序序列，然后根据有序序列前后相减得到判断

   ```
   
   class Solution {
       public int getMinimumDifference(TreeNode root) {
   
           //可以利用中序遍历得到中序序列
           if (root == null) return 0;
           List<Integer> result = new ArrayList<>();
           inorder(root, result);
           int min = Integer.MAX_VALUE;
           for (int i = 0; i < result.size() - 1; i++) {
               int temp = result.get(i + 1) - result.get(i);
               if (temp < min) min = temp;
           }
           return min;
   
       }
   
       private void inorder(TreeNode root, List<Integer> result) {
           if (root == null) return;
           //左中右
           inorder(root.left, result);
           result.add(root.val);
           inorder(root.right, result);
       }
   }
   ```

   **优化代码：==其实是在中序遍历的过程中就进行比较，这个时候需要定义一个pre指针和cur指针，因为最小绝对差肯定是这俩相减得到的==**

   ```
       private TreeNode pre = null;
       int result = Integer.MAX_VALUE;
       public int getMinimumDifference(TreeNode root) {
           if (root == null) return 0;
           inorder(root);
           return result;
       }
       private void inorder(TreeNode root) {
           if (root == null) return;
           //左中右
           inorder(root.left);
           if (pre != null) {
               if (result > root.val - pre.val) result = root.val - pre.val;
           }
           pre = root;
           inorder(root.right);
       }
   ```

   

5. **501 二叉搜索树中的众数 -- 这道题优化算法是  不使用额外的空间**

   有两个重要的代码：

   1. ==可以先用list集合去存放元素，然后将list集合转换成数组：==

   ==`return result.stream().mapToInt(Integer::intValue).toArray();`==

   2. ==result.clear()==

   ```
   class Solution {
       //构造前一个节点的指针
       TreeNode pre = null;
       int count = 1;
       int maxcount = Integer.MIN_VALUE;
       public int[] findMode(TreeNode root) {
           //按照常规做法遍历得到中序序列去做
           //进阶做法，不需要额外的空间，用指针
           List<Integer> result = new ArrayList<>();
           //if (root == null) return result;
           inorder(root, result);
           return result.stream().mapToInt(Integer::intValue).toArray();
   
       }
   
       private void inorder(TreeNode root, List<Integer> result) {
           if (root == null) return;
           inorder(root.left, result);
   
           if (pre != null) {
               if (pre.val == root.val) count++;
               if (pre.val != root.val) {
                   count = 1;
               }
           }
   
           if (count > maxcount) {
               result.clear();
               result.add(root.val);
               maxcount = count;
           } else if (count == maxcount) {
               result.add(root.val);
           }
   
           pre = root;
           inorder(root.right, result);
   
       }
   }
   ```

   



6. **==236 二叉树的最近公共祖先==**     不太会！！最好背下来

   **后序递归+回溯**

   **找到一个根，如果在这个根子树的左右子树找到了p和q，那么这个根节点就是最小公共祖先**

   ![image-20250214161750043](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250214161750043.png)

   ```
   class Solution {
       public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
           if (root == null || root == p || root == q) { // 递归结束条件
               return root;
           }
   
           // 后序遍历
           TreeNode left = lowestCommonAncestor(root.left, p, q);
           TreeNode right = lowestCommonAncestor(root.right, p, q);
           
           //递归函数有返回值，如何区分搜索一条边还是整棵树，这里是要搜索整棵树
   
           if(left == null && right == null) { // 若未找到节点 p 或 q
               return null;
           }else if(left == null && right != null) { // 若找到一个节点
               return right;
           }else if(left != null && right == null) { // 若找到一个节点
               return left;
           }else { // 如果找到了，那么当前根节点就是最近公共祖先
               return root;
           }
       }
   }
   
   ```

   

## day22：2025/2/16

### 二叉搜索树 -- 最近公共祖先 -- 节点插入 -- 节点删除

1. **235 二叉搜索树的最近公共祖先 -- 注意和236的对比**

   利用二叉搜索树的性质，常规求二叉树的最近公共祖先是从下到上回溯递归遍历，而**在二叉搜索树中，从上到下遍历，找到第一个节点的值位于[p.val,q.val]的节点，这个就是最近公共祖先；**因为是有序树，所以最近公共祖先的值肯定是在这个区间内的。

   ```
   
   class Solution {
       public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
   
           //利用二叉搜索树的性质，利用迭代法求解
           //从上到下遍历，找到第一个处于[p.val,q.val]的节点就是最近公共祖先
           while(root!=null){
               if(root.val>p.val&&root.val>q.val){
                   root=root.left;
               }
               if(root.val<p.val&&root.val<q.val){
                   root=root.right;
               }
               if(root.val>=p.val&&root.val<=q.val)
                   return root;
               if(root.val>=q.val&&root.val<=p.val)
                   return root;
           }
           return null;
       }
   }
   
   ```

   

2. **701 二叉搜索树中的插入操作--- 插入其实是遇到空节点插入，而不是遇到叶子节点插入**，比如看下面这个例子，现在要插入4，应该插到5的左节点，而5就不是叶子节点

   ![image-20250216182154058](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250216182154058.png)

   ==**循环迭代找到空节点擅长使用设置一个pre指针**==

   ```
   
   class Solution {
       public TreeNode insertIntoBST(TreeNode root, int val) {
           //如果是一个空节点
           if (root == null) {
               TreeNode node = new TreeNode(val);
               return node;
           }
           TreeNode pre = root;
           TreeNode newroot = root;
           //先找到空节点
           while (root != null) {
               pre = root;
               if (root.val > val)
                   root = root.left;
               else if (root.val < val)
                   root = root.right;
           }
           
           //然后再插入
           if (pre.val > val) {
               pre.left = new TreeNode(val);
           } else {
               pre.right = new TreeNode(val);
           }
           return newroot;
       }
   }
   
   ```

   

3. **450 删除二叉搜索树的节点  -- 删除比增加要复杂一些**

   递归做法：从上到下遍历

   讨论几种情况：

   1. 如果删除的节点没找到 返回root

   2. 删除的节点的左节点和右节点为空，返回null

   3. 删除的节点左节点为空，右节点不为空，返回以右节点为根的子树

   4. 删除的左节点不为空，右节点为空，返回以左节点为根的子树

   5. 如果左右节点都不为空，那么就把左节点安在右节点的树中最左节点的左节点

      ```
      
      class Solution {
          public TreeNode deleteNode(TreeNode root, int key) {
              //采用递归解法
              if (root == null) return root; //第一种情况，不存在
              if (root.val == key) {
                  if (root.left != null && root.right == null) //第二种情况，右节点为空，左节点不为空，返回左节点为根
                      return root.left;
                  else if (root.left == null && root.right != null) { //第三种情况，左节点为空，右节点不为空，返回右节点为根
                      return root.right;
                  } else if (root.left == null && root.right == null) return null;//第四种情况，叶子节点，直接删除，返回null为空节点
                  else {
                      //左右节点都不为空
                      //让左子树安在右子树最左节点的左节点
                      TreeNode cur = root.right;
                      while (cur.left != null) {
                          cur = cur.left;
                      }
                      cur.left = root.left;
                      root = root.right;
                      return root;
                      //
                  }
              }
              if (root.val > key) {
                  root.left = deleteNode(root.left, key);
              } else if (root.val < key) {
                  root.right = deleteNode(root.right, key);
              }
              return root;
      
      
          }
      }
      
      ```

      

## day23：2025/2/17

### 二叉搜索树  -- 修剪二叉搜索树 -- 根据有序数组构建平衡二叉搜索树

1. **669 修剪二叉搜索树 -- 使用递归方法 -- 分为三步走** 这道题关键是：删除节点的操作其实和450 删除二叉树节点的操作一样

   我自己写的代码，代码中尤其要注意if .. if .. if .. 和if .. else if .. else if .. else的代码逻辑的区别

   ```
   
   class Solution {
       public TreeNode trimBST(TreeNode root, int low, int high) {    
           //递归搜索
           if (root == null) return null;
           if (root.val > high) {
               //根节点的值大于high
               //递归搜索左子树
               root.left = trimBST(root.left, low, high);
               return root.left;
           } else if (root.val < low) {
               //根节点的值小于low
               //递归搜索右子树
               root.right = trimBST(root.right, low, high);
               return root.right;
           } else {
               //根节点的值正好处于区间内
               //递归搜索左右子树
               root.left = trimBST(root.left, low, high);
               root.right = trimBST(root.right, low, high);
           }
           return root;
       }
   }
   ```

   

2. **108 将有序数组转换为高度平衡二叉搜索树**

   不需要去刻意判断是否是平衡二叉树，因为数组是有序的，只需要从每次从中间分割，递归遍历左右区间，最终的二叉树一定是平衡二叉树

   ```
   
   class Solution {
       public TreeNode sortedArrayToBST(int[] nums) {
           int length = nums.length;
           if (length == 0) return null;
           //只要递归左右区间并且从左右区间中间位置分割就可以了
           TreeNode root = new TreeNode();
           root = midBST(0, length, nums, root);//区间就是左闭右开
           return root;
   
       }
       private TreeNode midBST(int begin, int end, int[] nums, TreeNode root) {
           if (begin >= end) return null;
           int mid = (end + begin) / 2;//分割点
           //int mid=end-(end-begin)/2;//一般防止溢出会这么写
           root = new TreeNode(nums[mid]);
           root.left = midBST(begin, mid, nums, root);
           root.right = midBST(mid + 1, end, nums, root);
           return root;
       }
   }
   ```

   

3. **538 把二叉搜索树转为累加树**

   反中序遍历

   按照右中左顺序递归遍历就行，递归遍历中，任何一个节点其实都是中节点，所以任何一个节点的操作都是一样的，千万不要被左节点右节点干扰

   ```
   
   class Solution {
       private int sum = 0;
       public TreeNode convertBST(TreeNode root) {
           //采用递归搜索
           if (root == null) return null;
           sumTree(root);
           return root;
       }
       private void sumTree(TreeNode root) {
           if (root == null) return ;
           //右中左
            sumTree(root.right);
            sum+=root.val;
            root.val=sum;
            sumTree(root.left);
       }
   
   }
   ```

   

## day24 2025/2/18

### 回溯算法 -- 子集

回溯法和递归法相辅相成，回溯法其实就是暴力查找，并不是什么高效的算法

==**回溯法，一般可以解决如下几种问题：**==

- 组合问题：N个数里面按一定规则找出k个数的集合
- 切割问题：一个字符串按一定规则有几种切割方式
- 子集问题：一个N个数的集合里有多少符合条件的子集
- 排列问题：N个数按一定规则全排列，有几种排列方式
- 棋盘问题：N皇后，解数独等等

回溯算法模板  - - 背下来最好

```
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```

1. ==**77 组合 --非常经典的回溯问题**==

   ![image-20250218163046627](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250218163046627.png)

   ```
   
   
   class Solution {
       public List<List<Integer>> combine(int n, int k) {
           //回溯算法的经典问题
           List<Integer> path = new ArrayList<>();
           List<List<Integer>> result = new ArrayList<>();
   
           //回溯函数
           backtracking(n, k, 1, path, result);
           
           return result;
       }
       private void backtracking(int n, int k, int startindex, List<Integer> path, List<List<Integer>> result) {
           if (path.size() == k) {
               result.add(new ArrayList<>(path));
               return;
           }
           for (int i = startindex; i <= n; i++) {
               path.add(i);
               backtracking(n, k, i + 1, path, result);
               path.remove(path.size()-1);
   
           }
   
       }
   
   }
   ```

   回溯算法有时候也是可以剪枝优化的，剪枝优化上述的遍历范围，举一个例子，n = 4，k = 4的话，那么第一层for循环的时候，从元素2开始的遍历都没有意义了。 在第二层for循环，从元素3开始的遍历都没有意义了。

   ![image-20250218163533287](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250218163533287.png)

   

   **可以剪枝的地方就在递归中每一层的for循环所选择的起始位置**。**如果for循环选择的起始位置之后的元素个数 已经不足 我们需要的元素个数了，那么就没有必要搜索了**。

   ```cpp
   for (int i = startIndex; i <= n - (k - path.size()) + 1; i++) 
   ```

2. **216 组合总和（iii）-- 和77组合题比较类似**

   这是我自己写出来的

   ```
   class Solution {
       List<Integer> path = new ArrayList<>();//路径
       List<List<Integer>> result = new ArrayList<>();//存放结果
       int sum = 0;
       public List<List<Integer>> combinationSum3(int k, int n) {
           if (n < k) return result;
           //回溯
           backtracking(k, n, 1);
           return result;
       }
       private void backtracking(int k, int n, int startindex) {
           if (path.size() == k && sum == n) {
               result.add(new ArrayList<>(path));
               return;
           }
           for (int i = startindex; i <= 9; i++) {
               path.add(i);
               sum = 0;
               for (int i1 = 0; i1 < path.size(); i1++) {
                   sum += path.get(i1);
               }
               backtracking(k, n, i + 1);
               path.remove(path.size() - 1);
           }
       }
   
   }
   ```

   

3.  **17 电话号码的字母组合**    **-- 创建StringBuilder对象，使用toString()方法转换为String类型**

   我自己写的答案

   我自己写的代码里面会涉及比较多的字符串的拼接，**所以其实可以把temp定义StringBuilder，**

   ```java
   StringBuilder temp = new StringBuilder();
   ```

   **字符串拼接就是append()**

   ```java
   temp.append(values[j]);
   ```

   **转换为String类型就是：String result=temp.toString();**

   ```
   String result=temp.toString();
   ```

   ```
   class Solution {
       List<String> result = new ArrayList<>();
       Map<Character, String[]> map = new HashMap<>();
       String temp="";
       public List<String> letterCombinations(String digits) {
   
           if (digits.length() == 0||digits==null) return result;
   
           map.put('2', new String[]{"a","b","c"});
           map.put('3', new String[]{"d","e","f"});
           map.put('4', new String[]{"g","h","i"});
           map.put('5', new String[]{"j","k","l"});
           map.put('6', new String[]{"m","n","o"});
           map.put('7', new String[]{"p","q","r","s"});
           map.put('8', new String[]{"t","u","v"});
           map.put('9', new String[]{"w","x","y","z"});
   
           char[] chars = digits.toCharArray();
           int length = chars.length;
           backtracking(chars,0,length);
           return result;
   
       }
       //回溯
       private void backtracking(char[] chars,int startindex,int length){
           if(temp.length()==length) {
               result.add(temp);
               return;
           }
           for (int i = startindex; i < length; i++) {
               String[] values = map.get(chars[i]);
               int size = values.length;
               for (int j = 0; j < size; j++) {
                   temp+=values[j];
                   backtracking(chars,i+1,length);
                    temp = temp.substring(0, temp.length() - 1);
               }
   
           }
   
       }
   }
   ```

   

4. **39 组合总和  **

   给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

   candidates 中的数字可以无限制重复被选取。

   能明白递归的调用，不要随便更改覆盖sum的值，因为可能会影响返回的值的调用

   ```
   class Solution {
       List<List<Integer>> result = new ArrayList<>();
       List<Integer> path = new ArrayList<>();
   
       public List<List<Integer>> combinationSum(int[] candidates, int target) {
           //首先对数组排序
           Arrays.sort(candidates);
           int length = candidates.length;
           backtracking(candidates, 0, target, length, 0);
           return result;
       }
   
       private void backtracking(int[] candidates, int startindex, int target, int length, int sum) {
           if (sum == target) { //等于的情况
               result.add(new ArrayList<>(path));
               return;
           }
           for (int i = startindex; i < length; i++) {
               if (sum + candidates[i] > target) break;//排完徐之后如果大于直接跳出循环，后面的都没必要遍历了
               //剩下的都是小于
               path.add(candidates[i]);
               //int temp = sum + candidates[i];
               sum = sum + candidates[i];
               backtracking(candidates, i, target, length, sum);
               sum -= candidates[i];
               path.remove(path.size() - 1);//移除路径的最后一个元素
   
           }
   
       }
   }
   ```

   

## day25 2025/2/19

### **回溯** -- 组合  -- 切割 -- 子集

1. **40 组合总和ii**  -- **数组里面有重复的元素，解集不能包含重复的组合，如何去重  -- 树枝数层**

   给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

   candidates 中的每个数字在每个组合中只能使用一次。

   说明： 所有数字（包括目标数）都是正整数。**解集不能包含重复的组合**。

   **==涉及一个标志数组：==**

   **如果`candidates[i] == candidates[i - 1]` 并且 `used[i - 1] == false`，就说明：前一个树枝，使用了candidates[i - 1]，也就是说同一树层使用过candidates[i - 1]**。

   `boolean[] used;//加一个标志数组，用来判断同一树层的元素是不是重复`

   `if (i > 0 && candidates[i] == candidates[i - 1] && !used[i - 1]) {`
                   `continue; //同一层的前一个节点相等并且被访问过，就可以直接跳过`
               }`

   - ==**used[i - 1] == true，说明同一树枝candidates[i - 1]使用过**==

   - ==**used[i - 1] == false，说明同一树层candidates[i - 1]使用过**==

     为什么 used[i - 1] == false 就是同一树层呢，因为同一树层，used[i - 1] == false 才能表示，当前取的 candidates[i] 是从 candidates[i - 1] 回溯而来的。

     而 used[i - 1] == true，说明是进入下一层递归，去下一个数，所以是树枝上

   ![image-20250219210847714](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250219210847714.png)

   

   ```
   class Solution {
   
       List<List<Integer>> result = new ArrayList<>();
       List<Integer> path = new ArrayList<>();
       boolean[] used;//加一个标志数组，用来判断同一树层的元素是不是重复
       int sum = 0;
       public List<List<Integer>> combinationSum2(int[] candidates, int target) {
   
           //组合总和ii
           //回溯
           //数组排序,这样大于目标值的后面都不用遍历了
           Arrays.sort(candidates);
           used = new boolean[candidates.length];//加一个标志数组，用来判断同一树层的元素是不是重复
           Arrays.fill(used, false);
           backtracking(candidates, target, 0);
           //用一个标记数组来去重
           return result;
   
       }
   
       private void backtracking(int[] candidates, int target, int startindex) {
           if (sum == target) { //相等的时候
               result.add(new ArrayList<>(path));
               return;
           }
           for (int i = startindex; i < candidates.length; i++) {
               //判断大于
               if (sum + candidates[i] > target) break;
               //剩下就是小于
               if (i > 0 && candidates[i] == candidates[i - 1] && !used[i - 1]) {
                   continue; //同一层的前一个节点相等并且被访问过，就可以直接跳过
               }
   
               used[i]=true;
               path.add(candidates[i]);
               sum += candidates[i];
               backtracking(candidates, target, i + 1);
               sum -= candidates[i];
               used[i]=false;
               path.remove(path.size() - 1);
   
           }
   
       }
   }
   ```

   

2. **131 分割回文串**   ==切割回溯+判断回文==

   **递归函数入参时，应该确保每次传的是新的StringBuilder对象，否则，temp 在不同递归路径之间会互相影响**

   //temp.setLength(0);和new StringBuilder()不一样，为了后面判断回文串方便
                   //应该在函数的入参中传入new StringBuilder()

   ```
   import java.util.ArrayList;
   import java.util.List;
   
   //leetcode submit region begin(Prohibit modification and deletion)
   class Solution {
   
       //和组合问题一致，截取
       List<List<String>> result = new ArrayList<>();
       List<String> path = new ArrayList<>();
       public List<List<String>> partition(String s) {
           //进入回溯
           backtracking(s, 0,new StringBuilder()); //每次递归都是新建一个新的StringBuilder
           return result;
       }
   
       //回溯代码
       private void backtracking(String s, int startindex,StringBuilder temp) {
           //递归终止条件，就是遍历到末尾了
           if (startindex == s.length()) {
               result.add(new ArrayList<>(path));//总是忘记这个！！
               return;
           }
   
           for (int i = startindex; i < s.length(); i++) {
               temp.append(s.charAt(i));
               if (huiwen(temp.toString())) {
                   //判断当前是回文串,进入回溯
                   path.add(temp.toString());
                   backtracking(s, i + 1,new StringBuilder());
                   //temp.setLength(0);和new StringBuilder()不一样，为了后面判断回文串方便
                   //应该在函数的入参中传入new StringBuilder()
                   //确保每次递归时都传递一个全新的 StringBuilder 对象。否则，temp 在不同递归路径之间会互相影响
                   path.remove(path.size() - 1);
               }
           }
   
       }
       //判断是否是回文串
       private boolean huiwen(String s) {
           //双指针判断是否是回文串
           int length = s.length();
           int begin = 0;
           int end = length - 1;
           while (begin < end) {
               if (s.charAt(begin) != s.charAt(end)) return false;
               begin++;
               end--;
           }
           return true;
       }
   }
   //leetcode submit region end(Prohibit modification and deletion)
   
   ```

   

3. **93 复原IP地址**

   我自己写的代码：一开始运行不过的原因是：我的count--的位置不对，其实我的count--应该在递归函数的下面，我错误的把count--放到了递归终止条件中了

   ```
   
   import java.util.ArrayList;
   import java.util.List;
   //leetcode submit region begin(Prohibit modification and deletion)
   class Solution {
       List<String> result = new ArrayList<>();
       int count = 0;
       List<String> path = new ArrayList<>();
   
       public List<String> restoreIpAddresses(String s) {
           //回溯
           backtracking(s, 0, new StringBuilder());
           return result;
       }
   
       //回溯算法递归代码
       private void backtracking(String s, int startindex, StringBuilder temp) {
           //字符串长度最小是4，最大是12
           if (startindex == s.length() && count == 4) {
               //将path转为String类型
               String join = String.join(".", path);
               result.add(join);
   
               return;
           }
           for (int i = startindex; i < s.length(); i++) {
               temp.append(s.charAt(i));
               if (temp.toString().length() < 4 && check(temp.toString())) {
                   //判断是合法的数字
                   //进入回溯
                   path.add(temp.toString());
                   count++;
                   backtracking(s, i + 1, new StringBuilder());
                   count--;
                   path.remove(path.size() - 1);
               }
           }
   
       }
   
       //判断是不是有效的数字
       private boolean check(String s) {
           if (s.length() > 1 && s.charAt(0) == '0') return false;
           Integer value = Integer.valueOf(s);
           if (value >= 0 && value <= 255) return true;
           return false;
       }
   }
   ```

   

4. **78子集  --  原始数组中不包含重复的元素**

    -- ==**要清楚子集问题和组合问题、分割问题的的区别，子集是收集树形结构中树的所有节点的结果**==。==

   ==**而组合问题、分割问题是收集树形结构中叶子节点的结果**==

   

   ![image-20250220151023319](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250220151023319.png)

  

```
class Solution {

    List<List<Integer>> result=new ArrayList<>();

    List<Integer> path=new ArrayList<>();

    public List<List<Integer>> subsets(int[] nums) {
        //收集遍历过程中所有节点就是求他的子集
        backtracking(nums,0);
        return  result;
    }
    private void backtracking(int[] nums,int startindex){
        result.add(new ArrayList<>(path));//遍历这颗树的时候，把所有的节点都记录下来，就是子集集合
        if(startindex>=nums.length) return;
        for (int i = startindex; i < nums.length; i++) {
            path.add(nums[i]);
            backtracking(nums,i+1);
            path.remove(path.size()-1);
        }
    }

}
```



## day26 2025/2/20

### 回溯 -- 子集

1. **90 子集II  -- 初始数组包含重复的元素**

   **==使用标记数组 、数组先排序进行去重==**

   或者使用标记数组和set方法去重：

               if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
                   //说明两个元素一样，而且前一个元素使用过了
                   continue;
               }

   ```
   //HashSet<List<Integer>> lists = new HashSet<>(result);
   //result = new ArrayList<>(lists);
   ```

   ```
   class Solution {
       List<List<Integer>> result = new ArrayList<>();
       List<Integer> path = new ArrayList<>();
       boolean[] used;
       public List<List<Integer>> subsetsWithDup(int[] nums) {
   
           //与子集不同的是这里面有重复的元素
           Arrays.sort(nums);
           used = new boolean[nums.length];
           Arrays.fill(used, false);
           backtracking(nums, 0);
           //难道这个地方要单独去重？不需要，只需要将初始数组排序即可
   
           return result;
       }
   
       //回溯代码
       private void backtracking(int[] nums, int startindex) {
           //递归终止条件
           result.add(new ArrayList<>(path));
           
           if (startindex >= nums.length) {
               return;
           }
           for (int i = startindex; i < nums.length; i++) {
               if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
                   //说明两个元素一样，而且前一个元素使用过了
                   continue;
               }
               used[i] = true;
               path.add(nums[i]);
               backtracking(nums, i + 1);
               used[i] = false;
               path.remove(path.size() - 1);
           }
   
   
       }
   }
   ```

   

2. **491 非递减子序列   -- 这道题不同的是，数组不是有序的而且也不能重新排序**

   ![image-20250220173635080](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250220173635080.png)

   求非递减子序列也是存储树中节点，只不过去重的逻辑就不同，就不再是将数组排序那种去重了

   1. **同一树层中相同的元素不能再次使用，使用set集合进行判断去重**

   `set.contains(nums[i])`,==哈希set集合定义在循环外面，就要考虑什么时候会进入循环，那么只有同一层才会进入循环，所以这个哈希Set是用来判断同一层的==

   2. **非递减子序列**  -- `!path.isEmpty()&&nums[i]<path.get(path.size()-1))`当前元素必须要大于等于path集合中最后一个元素，否则就不是

   ```
   class Solution {
       //不能对数组排序
       //去重也不能用used
       List<List<Integer>> result=new ArrayList<>();
       List<Integer> path =new ArrayList<>();
       public List<List<Integer>> findSubsequences(int[] nums) {
           //for循环是横向遍历
           //递归是纵向搜索
           backtracking(nums,0);
           return result;
   
       }
       private void backtracking(int[] nums,int startindex){
           //本题也是存储树的所有节点
           if(path.size()>1) result.add(new ArrayList<>(path));
           if(startindex>= nums.length) return;
           //同一树层上，相等的元素不可以重复使用,用set集合来判断是不是已经使用过
           HashSet<Integer> set = new HashSet<>();
           for (int i = startindex; i < nums.length; i++) {
               //判断continue的条件
               //如果当前的元素小于path的最后一个元素或者set中已经存在了相同的元素，同一树层不能使用相同的
               if((!path.isEmpty()&&nums[i]<path.get(path.size()-1))||set.contains(nums[i])){
                   continue;
               }
               set.add(nums[i]);
               path.add(nums[i]);
               backtracking(nums,i+1);
               path.remove(path.size()-1);
           }
   
   
       }
   }
   ```

   

## day27 2025/2/21

### 回溯--排列  -- N皇后

1. ==**46 全排列  -- 非常典型的回溯题目**==

   数组无重复元素，全排列

   **==使用used数组其实目的很简单，是为了判断从0开始遍历的时候，哪些元素不用再遍历了,==需要used数组记录path里都放了哪些元素了**

   

   **维护一个全局数组，used，对比上面一题，知道为什么不能用哈希set，上面的set只是需要维护同一层，而且本题遍历范围都是从0开始，不是i+1这种了**

   ```
   class Solution {
       List<List<Integer>> result=new ArrayList<>();
       List<Integer> path=new ArrayList<>();
       //维护一个全局used数组
       boolean[] used;
       public List<List<Integer>> permute(int[] nums) {
           //全排列
           //保存叶子结点
           used=new boolean[nums.length];
          Arrays.fill(used,false);
           backtracking(nums,0);
           return result;
       }
       private void backtracking(int[] nums, int index){
           if (path.size()== nums.length) {
               result.add(new ArrayList<>(path));
               return;
           }    
   
           for (int i = 0; i < nums.length; i++) {
               if(used[i]){
                   //说明已经使用过了
                   continue;
               }
               used[i]=true;
               //if(set.contains(nums[i])) continue;
               //set.add(nums[i]);
               path.add(nums[i]);
               backtracking(nums,0);
               used[i]=false;
               path.remove(path.size()-1);
           }
   
       }
   
   }
   ```

   

2. **47 全排列II -- 全排列的去重问题**

   1. ==**数组排序**==

   2. ==**全局used数组，判断同一层去重**==

      ```
      if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
          continue;
      }
      ```

​			**==3. 全排列的问题，遍历索引从0开始==**

```
class Solution {
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> result = new ArrayList<>();
    boolean[] used;

    public List<List<Integer>> permuteUnique(int[] nums) {
        if (nums.length == 0 || nums == null) return result;
        used = new boolean[nums.length];
        Arrays.fill(used, false);
        Arrays.sort(nums);
        backtracking(nums, 0);
        return result;

    }

    private void backtracking(int[] nums, int index) {
        if (path.size() == nums.length) {
            result.add(new ArrayList<>(path));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
                continue;
            }
            if (used[i] == false) {
                used[i] = true;
                path.add(nums[i]);
                backtracking(nums, 0);
                used[i] = false;
                path.remove(path.size() - 1);

            }
        }

    }
}

```

3. **==51 N皇后  -  ！！！！==**

   ![image-20250221173647242](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250221173647242.png)

   ![image-20250221173709059](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250221173709059.png)

   **我的误区：在判断斜线的时候，只判断了45度斜线，没有判断135度的斜线**

   反思的点：

   1. **设置一个二维数组，类型是char型，初始全为'.'**
   2. **如何构造String ,其实看下面的代码可以看出，就是把一行的字符拼起来就行**
   3. **棋盘的宽度也就是二维数组的列数就是for循环的宽度**
   4. **二维数组的行数就是递归的深度**

   下面给出代码随想录的参考代码：

   ```
   class Solution {
       List<List<String>> res = new ArrayList<>();
   
       public List<List<String>> solveNQueens(int n) {
           char[][] chessboard = new char[n][n];
           for (char[] c : chessboard) {
               Arrays.fill(c, '.');
           }
           backTrack(n, 0, chessboard);
           return res;
       }
   
       public void backTrack(int n, int row, char[][] chessboard) {
           if (row == n) {
               res.add(Array2List(chessboard));
               return;
           }
   
           for (int col = 0;col < n; ++col) {
               if (isValid (row, col, n, chessboard)) {
                   chessboard[row][col] = 'Q';
                   backTrack(n, row+1, chessboard);
                   chessboard[row][col] = '.';
               }
           }
   
       }
   
       public List Array2List(char[][] chessboard) {
           List<String> list = new ArrayList<>();
   
           for (char[] c : chessboard) {
               list.add(String.copyValueOf(c));
           }
           return list;
       }
   
   
       public boolean isValid(int row, int col, int n, char[][] chessboard) {
       
          //判断在同一行,在这一行上遍历所有的列，这是我自己加的，其实也可以不用判断
           for (int i = 0; i < col; i++) {
               if (board[row][i] == 1) return false;
           }
           // 检查列
           for (int i=0; i<row; ++i) { // 相当于剪枝
               if (chessboard[i][col] == 'Q') {
                   return false;
               }
           }
           // 检查45度对角线
           for (int i=row-1, j=col-1; i>=0 && j>=0; i--, j--) {
               if (chessboard[i][j] == 'Q') {
                   return false;
               }
           }
           // 检查135度对角线
           for (int i=row-1, j=col+1; i>=0 && j<=n-1; i--, j++) {
               if (chessboard[i][j] == 'Q') {
                   return false;
               }
           }
           return true;
       }
   }
   ```

   

## day28 2025/2/22

### **回溯- 解数独**

1. **37 解数独 --** 

   **一个for循环遍历棋盘的行，一个for循环遍历棋盘的列，一行一列确定下来之后，递归遍历这个位置放9个数字的可能性！**

   二维递归，并且这个递归是没有终止条件的，因为在题目中只有一个解

   **确定一行一列ij，然后在每个格子内实验1-9，如果1-9都不行那么就可以返回false了，说明根本没有解，如果在1-9找到了一个，那么就可以返回true**

   ==**和N皇后的区别在于：N皇后是for循环的长度是棋盘的宽度，递归的深度是棋盘的高度；**==

   ==**但是本题解数独，我觉得是递归的深度是1-9，双层for循环遍历每个格子**==

   ```
   class Solution {
       public void solveSudoku(char[][] board) {
           //二维递归
           backtrecking(board);
       }
       //回溯算法
       private boolean backtrecking(char[][] board) {
           //二维递归
           //确定一行一列，然后实验1-9
           for (int i = 0; i < 9; i++) {//行
   
               for (int j = 0; j < 9; j++) {//列
                   //确定好每一个格子
                   if (board[i][j] != '.') continue;
                   //尝试1-9
                   for (char k = '1'; k <= '9'; k++) {
                       if (isValid(k,board,i,j)) {
                           //如果是有效的
                           board[i][j] = k;
                           //如果有合适的一组立马返回
                           if (backtrecking(board)) return true;
                           board[i][j] = '.';//回溯回去
                       }
                   }
                   //如果9个数字都不行，按照题意就是没有解
                   return false;
               }
           }
           return true;
   
       }
   
       //判断是否有效
      private boolean isValid(char c, char[][] board, int row, int col) {
           //判断每一行只能出现一次
           for (int i = 0; i < 9; i++) {
               if (board[row][i] == c) return false;
           }
   
           //判断每一列只能出现一次
           for (int i = 0; i < 9; i++) {
               if (board[i][col] == c) return false;
           }
   
           //判断3x3只能出现一次
           //判断第几个格子
           int startrow = (row / 3) * 3;
           int startcol = (col / 3) * 3;
           for (int i = startrow; i < startrow + 3; i++) {
               for (int j = startcol; j < startcol + 3; j++) {
                   if (board[i][j] == c)
                       return false;
               }
           }
           return true;
       }
   
   
   }
   ```

   

## day29 2025/2/24

### 贪心算法

1. **455 分饼干**

   比较简单的一道贪心算法题目，总的思路来说就是对两个数组排序，然后指针移动

   **局部最优：**小饼干先喂小胃口；**全局最优：**尽可能满足更多孩子的胃口

   **我自己写的代码：**

   **要注意的地方是，sindex移动，当s[sindex]<g[gindex]的时候，不是立即返回，而是让sindex指针往右移动一个**

   ```
   class Solution {
       public int findContentChildren(int[] g, int[] s) {
           //对g和s排序
           Arrays.sort(g);
           Arrays.sort(s);
           int length = g.length;
           int slength = s.length;
           int gindex = 0;
           int sindex = 0;
           int count=0;
           while (gindex < length && sindex < slength) {//当有两个指针的时候，我们要考虑while循环，并且这里面其实从指针的移动可以看出来优先考虑饼干
               if(s[sindex]<g[gindex]){
                   sindex++;
               }else {
                   gindex++;
                   sindex++;
                   count++;
               }
           }
           return count;
       }
   }
   ```

   

2. **376 摆动序列    --- 代码不难，难在挺难想的，情况没有考虑全**

   将摆动序列想成坡

   ![image-20250224200931894](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250224200931894.png)

   

   考虑三种情况：

   - 上下坡有平坡
   - 数组首尾两端
   - 单调的坡但是有平坡

   ```
   class Solution {
       public int wiggleMaxLength(int[] nums) {
           //将序列想成一个上下坡
           //定义两个指针
           if (nums.length == 1) return 1;
           int presub = 0;
           int cursub = 0;
           int count = 1;//初始设成1
           
           for (int i = 1; i < nums.length; i++) {
               cursub = nums[i] - nums[i - 1];//cursub为当前与前一个差值，这个差值一直在更新
               //但是presub不是一直在更新，它只在一正一负的时候进行更新赋值，否则它将一直维护在未更新阶段的值
               //只需要在 这个坡度 摆动变化的时候，更新 presub 就行
               //等于0的情况是初始时候的presub
               if ((cursub > 0 && presub <= 0) || (cursub < 0 && presub >= 0)) {
                   count++;
                   presub = cursub;
               }
           }
           return count;
   
       }
   }
   ```

   

## day30 2025/2/25

### 贪心算法

1. **53最大子数组和    --- 也许最开始就想到两层循环甚至双指针，但其实用贪心算法一层for循环就可以解决**，这也是一道dp问题 

   遍历 nums，从头开始用 count 累积，如果 count 一旦加上 nums[i]变为负数，那么就应该从 nums[i+1]开始从 0 累积 count 了，因为已经变为负数的 count，只会拖累总和。

   1. **sum要初始化为最小负数，因为防止数组中数全为负数的形式**
   2. **不是遇到 负数就选择起始位置，而是连续和为负选择起始位置。**

   ```
   class Solution {
       public int maxSubArray(int[] nums) {
   
           //局部最优，推出整体最优
           if(nums.length==1) return nums[0];
   
           //这道题不同的地方在于，不是遇到负数就停止相加，而是如果发现累加和变为负数就要停止相加
           int sum=Integer.MIN_VALUE;
           int count=0;
           for (int i = 0; i < nums.length; i++) {
               count+=nums[i];
               sum=Math.max(count,sum); // 取区间累计的最大值（相当于不断确定最大子序终止位置）
               if(count<0){
                   //如果连续和变为负数，就要停止往后的相加，因为负数只会拖累累计和
   
                  count=0;// 相当于重置最大子序起始位置，因为遇到负数一定是拉低总和
               }
           }
           return sum;
           
       }
   }
   ```

   

2. **122 买卖股票的最佳时机II   - 这道题重点在于==理解拆分利润==  --- 也是一道动态规划的问题**

   ==prices[3] - prices[0] = (prices[3] - prices[2]) + (prices[2] - prices[1]) + (prices[1] - prices[0])==

   ==哪天买入，哪天卖出，这里面的利润其实可以拆解为每天为单位的维度，数学方法==

   **此时就是把利润分解为每天为单位的维度，而不是从 0 天到第 3 天整体去考虑！**

   ![image-20250225195943635](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250225195943635.png)

   ```
   class Solution {
       public int maxProfit(int[] prices) {
           //不能排序
           int length = prices.length;
           if (length == 1) return 0;
   
           //拆分利润
           int result = 0;
           //prices[3] - prices[0]=
           // (prices[3] - prices[2]) 
           // + (prices[2] - prices[1]) + 
           // (prices[1] - prices[0])
           //从第二天开始，只收集每天的正利润,然后累加
           for (int i = 1; i < length; i++) {
               if (prices[i] - prices[i - 1] > 0)
                   result += prices[i] - prices[i - 1];
           }
           return result;
       }
   }
   ```

   

3.  **55 跳跃游戏**

   这道题的思路就是去看每个下标跳跃的范围，如果能cover到末尾元素就可以

   我自己写的与参考答案不同的地方是for循环，参考答案的for循环控制其实是coverRange

   ![image-20250225203643141](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250225203643141.png)

   ```
   class Solution {
       public boolean canJump(int[] nums) {
           int length = nums.length;
           int pathLen = 0;
           if (length == 1) return true;
           int coverRange = 0;
           int currentcover = 0;
           //取每一个下标的最大跳跃范围，只要最大跳跃范围能够覆盖到终点，那么就可以跳跃到终点
           for (int i = 0; i < length - 1; i++) {
               if (i > coverRange) return false;//这一步判断很重要，比如[0,2,3]
               currentcover = i + nums[i];
               coverRange = Math.max(coverRange, currentcover);
               if (coverRange >= length - 1) return true;
           }
           return false;
       }
   }
   ```

   

4. **==45 跳跃游戏II   -- 这道题也需要利用覆盖范围的知识 ，比较难，没有想起来==**

   具体需要看代码去理解，**需要统计两个覆盖范围，当前这一步的最大覆盖和下一步最大覆盖**

   ```
   //需要统计两个覆盖范围，当前这一步的最大覆盖和下一步最大覆盖class Solution {
   
       public int jump(int[] nums) {
           if (nums.length == 1) return 0;
           int jumpcount = 0;
           int coverRange = 0;
   
           //当前下标的最远覆盖距离
           int currentRange = 0;
           //
           int nextRange = 0;
   
           for (int i = 0; i < nums.length; i++) {
               // nextRange = nums[i] + i;这种写法不对
               nextRange = Math.max(nextRange, nums[i] + i);//这个地方要取最大值
               if (nextRange >= nums.length - 1) return jumpcount + 1;
               if (i == currentRange) {
                   jumpcount++;
                   currentRange = nextRange;
               }
   
           }
           return jumpcount;
   
       }
   }
   ```

   

## day31 2025/2/26

### 贪心算法   -- 学会使用java的Stream流

1. **1005 k次取反后最大化的数组和**    **==整个数组求和要学会使用： Arrays.stream(nums).sum()==**

   下面是给出的题解

   ```
           //官方题解：将元素按照绝对值值大小，从大到小排序，
           //然后遍历数组，如果遇到是负数，那么就转为正数，如果负数都转完毕了，这个时候的k还是不为0
           //那么就要对数组最后一个元素反复取反最后累加即可   
           
           
         nums = IntStream.of(nums)
                   .boxed() //封装成integer
                   .sorted((o1, o2) -> Math.abs(o2) - Math.abs(o1))
                   .mapToInt(Integer::intValue)
                   .toArray();
   
           for (int i = 0; i < nums.length; i++) {
               if (nums[i] < 0) {
                   k--;
                   nums[i] = -nums[i];
               }
               if (k == 0) break;
           }
           if (k % 2 == 1) {
               nums[nums.length - 1] = -nums[nums.length - 1];
           }
           //调用这个函数方法求和
           return Arrays.stream(nums).sum();
   ```

   这是我自己的思路，其实有点复杂，不过也是一种答案，就是对数组k次排序，每次都取第一个元素让它变为自己的相反数，最后再遍历数组进行相加求和即可

   ```
   class Solution {
       public int largestSumAfterKNegations(int[] nums, int k) {
   
           //首先对数组进行排序
           //然后遍历数组，如果当前值小于0，那么就将当前值取反，
           //局部最优：尽可能把负数都变为正数，减去的话也要减去当前最小的那个
           int sum = 0;
           while (k > 0) {
               Arrays.sort(nums);
               nums[0] = -nums[0];
               k--;
           }
           for (int i = 0; i < nums.length; i++) {
               sum += nums[i];
           }
           return sum;
       }
   }
   ```

   

2. **134 加油站**

   这道题用暴力求解是严重超时的，这道题又涉及到相减，累加

   可以换一个思路，首先如果总油量减去总消耗大于等于零那么一定可以跑完一圈，说明 各个站点的加油站 剩油量rest[i]相加一定是大于等于零的。

   每个加油站的剩余量rest[i]为gas[i] - cost[i]。

   i从0开始累加rest[i]，和记为curSum，一旦curSum小于零，说明[0, i]区间都不能作为起始位置，因为这个区间选择任何一个位置作为起点，到i这里都会断油，那么起始位置从i+1算起，再从0计算curSum。

   ![image-20250226211415644](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250226211415644.png)

   ```
   class Solution {
       public int canCompleteCircuit(int[] gas, int[] cost) {
   
           //贪心算法
           int curSum = 0;
           int totalSum = 0;//这个是为了判断如果所有gas[i]-cost[i]累加和小于0，那么肯定不能绕一圈
           int index = 0;
           for (int i = 0; i < gas.length; i++) {
               curSum += gas[i] - cost[i];
               totalSum += gas[i] - cost[i];
               if (curSum < 0) {
                   //更新位置
                   index = (i + 1) % (gas.length);
                   curSum=0;
               }
           }
           if(totalSum<0) return -1;
           return index;
   
   /*        //双层暴力循环严重超时,严重超过
           int length = gas.length;
           int rest = 0;
           for (int i = 0; i < length; i++) {
               rest = gas[i] - cost[i];
               int j = (i + 1) % length;
               while (j != i && rest > 0) {
                   rest += gas[j] - cost[j];
                   j = (j + 1) % length;
               }
               if (rest >= 0 && j == i) return i;
           }
   
           return -1;*/
   
       }
   }
   ```

   

## day32 2025/2/27

### 贪心算法

1. **135 分发糖果**  -- 相邻中比较更多，从左到右，从右到左

   要求相邻的孩子中评分高的孩子获得的糖果数更多

   1. 先是从左到右比较，相当于从前到后遍历
   2. 最后再从右到左比较，相当于从后到前遍历

   ```
   class Solution {
       public int candy(int[] ratings) {
           //先从左向右
           //只要右边的孩子评分比左边的孩子评分高，那么糖果数量就加一
           //再从右向左
           int[] candy = new int[ratings.length];
           candy[0] = 1;
           for (int i = 1; i < ratings.length; i++) {
               if (ratings[i] > ratings[i - 1]) {
                   candy[i] = candy[i - 1] + 1;
               } else candy[i] = 1;
           }
           //从右向左
           //
           for (int i = ratings.length - 2; i >= 0; i--) {
               if (ratings[i] > ratings[i + 1]) {
                   //candy[i] = candy[i+1] + 1;//这地方这样写不对，应该是再和自己比较，取最大值
                   candy[i] = Math.max(candy[i], candy[i + 1] + 1);
               }
   
           }
           int result = Arrays.stream(candy).sum();
           return result;
       }
   }
   ```

   

2. **860 柠檬水找零**

   这道题属于比较简单的题目，数组中每个数值要么是5，要么是10，要么是20

   **而且找钱的方式也比较简单，比如10，只能是找一张5，比如20，那就是两种情况：找一张10和一张5，找三张5；而且这种情况下，我们要优先消耗掉10**

   以下是我自己写的答案：

   ```
   class Solution {
       public boolean lemonadeChange(int[] bills) {
   
           if (bills[0] != 5) return false;//判断异常的情况
           int five = 0;
           int ten = 0;
           for (int i = 0; i < bills.length; i++) {
               if (bills[i] == 5) five++; //5元的情况
               else if (bills[i] == 10) {//10元的情况
                   if (five == 0) return false;
                   else {
                       five--;
                       ten++;
                   }
               } else {//20元的情况
                   if (five == 0) return false;
                   //再来判断一种false情况
                   if (ten == 0 && five < 3) return false;
                   //20元就是两种情况，要么3张5元，要么一张10元+一张5元
                   //首先先消耗10元
                   if (ten > 0) {
                       ten--;
                       five--;
                   } else if (ten == 0 && five >= 3) {
                       five = five - 3;
                   }
               }
           }
           return true;
       }
   }
   ```

   

3. **406 根据身高重建队列    -- 学会用LinkedList，学会用链表，并且学会反转回int型数组**

   **本题有两个维度，h和k，看到这种题目一定要想如何确定一个维度，然后再按照另一个维度重新排列。**

   先按照身高h来排序呢，身高一定是从大到小排（身高相同的话则k小的站前面），让高个子在前面。然后只需要按照k为下标重新插入队列就可以了

   **关键代码：**

   //先按照身高排序降序排列，身高相同，k小的站在前面
           ==**Arrays.sort(people, (o1, o2) -> o1[0] == o2[0] ? o1[1] - o2[1] : o2[0] - o1[0]);**==

   **==LinkedList<int[]> result=new LinkedList<>();==**

    int[][] ints = result.toArray(new int   [[people.length]][2]);

   ```
   class Solution {
       public int[][] reconstructQueue(int[][] people) {
   
   
           //二维数组的行数
           int row = people.length;
           //二维数组的列数
           int col = people[0].length;
   
           //构建一个链表
           LinkedList<int[]> result=new LinkedList<>();
   
           //两个维度，先固定一个维度
           //先按照身高排序降序排列，身高相同，k小的站在前面
           Arrays.sort(people, (o1, o2) -> o1[0] == o2[0] ? o1[1] - o2[1] : o2[0] - o1[0]);
           //遍历数组，按照k坐标插入到链表当中
           for (int[] person : people) {
               result.add(person[1],person);//add(index,value)将value插入到指定index中
           }
           int[][] ints = result.toArray(new int[people.length][2]);
           return ints;
   
       }
   }
   ```

   

4. **452 用最小数量的箭引爆气球** 

   按照起始位置排序，那么就从前向后遍历气球数组，**如果气球重叠了，重叠气球中右边边界的最小值 之前的区间一定需要一个弓箭**。

   ![image-20250227172035007](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250227172035007.png)

   不好理解，这个其实我没大想明白，可以过一段时间重新想想

   ```
   class Solution {
       public int findMinArrowShots(int[][] points) {
   
           //先将数组按照第一个元素进行从小到大排序
           //这里是要观察右边界
           Arrays.sort(points, (a, b) -> Integer.compare(a[0],b[0]));//防止溢出
           //然后从第二个元素开始遍历
           int count = 1;//只有一个元素的时候也要给自己射一箭
           for (int i = 1; i < points.length; i++) {
   
               if (points[i][0] > points[i - 1][1]) {//这里必须是大于，不能是等于
                   count++;//最小的右边界之前必须会射一箭
               } else {
                   //如果不大于它
                   points[i][1] = Math.min(points[i][1], points[i - 1][1]);
               }
           }
   
           return count;
   
       }
   }
   ```

   

5. **435 无重复区间**

   我自己写的答案，其实思路和上一题一样，只不过判断的时候这里面是大于等于，弓箭的数量就相当于是非重叠区间的数量

   ```
   class Solution {
       public int eraseOverlapIntervals(int[][] intervals) {
           //数组从小到大排序
           Arrays.sort(intervals, (o1, o2) -> o1[0] == o2[0] ? o1[1] - o2[1] : o1[0] - o2[0] );
           int count = 1;//初始的
           if (intervals.length == 1) return 0;
           
           for (int i = 1; i < intervals.length; i++) {
               if (intervals[i][0] >= intervals[i-1][1]) {
                   count++;//这个是计算有多少个不重复区间
               }else {
                   intervals[i][1]=Math.min(intervals[i-1][1],intervals[i][1]);//赋值最小右边界
               }
           }
           if (count == 0) {
               return intervals.length - 1;
           }
           int result = 0;
           result = intervals.length - count;//总区间减去不重复的区间，剩下的就是重复的区间，剔除就可以
           return result;
   
       }
   ```

   

6. **763 划分字母区间    ==学会在遍历过程中维护一个max或者min，很多时候可以避免使用双重循环暴力求解==**

   这道题一上来我的思路是利用双重循环，不断地扩展区间，但其实不需要，只需要维护一个max就行，在遍历地过程中不断比较max，如果你当前的坐标与这个max相等，那么就说明分割点到了，这样避免了双重循环暴力求解

   ```
   class Solution {
       public List<Integer> partitionLabels(String s) {
           //存储每个字符的最大索引
           //遍历这个字符串
           //遍历当前字符到它最大索引之间的所有字符，不断更改这个最大区间，直到遍历到子区间最大值
           List<Integer> result = new ArrayList<>();
           if (s.length() == 1) {
               result.add(1);
               return result;
           }
           int length = s.length();
           char[] charArray = s.toCharArray();
           int[] maxindex = new int[26];//存储每个字符的做大索引
           int index = 0;
           for (int i = 0; i < length; i++) {
               index = charArray[i] - 'a';
               maxindex[index] = i;
           }
   
           int max = 0;
           int last = 0;
           //遍历这个字符串，记录最大值，如果当前下标与最大值相等，那么就是分割点
           //这样就不用双重循环遍历了，只需要维护一个最大值即可
           for (int i = 0; i < length; i++) {
               //得到最大索引
               max = Math.max(max, maxindex[charArray[i] - 'a']);
               if (i == max) {
                   //说明找到了分割点
                   result.add(i - last + 1);
                   last = i + 1;
               }
           }
           return result;
   
       }
   }
   
   ```

   



## day33 2025/2/28

### 贪心算法   将int转变为String String.valueOf(n)

1. **56 合并区间**

   与上面重复区间的解法一样，思路相同，先排序，合并重复区间的关键是更新区间的begin和end

   ```
   class Solution {
       public int[][] merge(int[][] intervals) {
           //数组按照第一个元素从小到大排序
           Arrays.sort(intervals, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
   
           LinkedList<int[]> result = new LinkedList<>();
   
           if (intervals.length == 1) {
               return intervals;
           }
           int i = 0;
           
           for (i = 1; i < intervals.length; i++) {
               if (intervals[i][0] <= intervals[i - 1][1]) {
                   //说明区间重叠
                   intervals[i][0] = Math.min(intervals[i - 1][0], intervals[i][0]);
                   intervals[i][1] = Math.max(intervals[i - 1][1], intervals[i][1]);
               } else {
                   //这个时候向链表集合中添加
                   result.add(intervals[i - 1]);
                   
               }
   
           }
           result.add(intervals[i - 1]);
           return result.toArray(new int[result.size()][2]);
   
       }
   }
   
   ```

   

2.  **738 单调递增的数字     ==将int类型数字转换为字符串   -- String.valueOf(n)==**

   这道题并没有想象的那么复杂，只需要从后向前遍历，如果发现当前数字比前一个要小，就把前一个大小-1，然后记录当前索引，在遍历的过程中，如果有一样的情况，也这样做同时更新i

   ```
   class Solution {
       public int monotoneIncreasingDigits(int n) {
           //从末尾向前遍历
           String s = String.valueOf(n);
           char[] chars = s.toCharArray();
           int start = s.length();
           for (int i = s.length() - 2; i >= 0; i--) {
               if (chars[i] > chars[i + 1]) {
                   chars[i]--;
                   start = i + 1;
               }
           }
           for (int i = start; i < s.length(); i++) {
               chars[i] = '9';
           }
           return Integer.parseInt(String.valueOf(chars));
       }
   
   
   }
   ```

   

3. **968 监控摄像头 --  hard 不太会做**

   从下到上遍历-  首选后序遍历 --- 左右中

   

   ```
   //leetcode submit region begin(Prohibit modification and deletion)
   /**
    * Definition for a binary tree node.
    * public class TreeNode {
    *     int val;
    *     TreeNode left;
    *     TreeNode right;
    *     TreeNode() {}
    *     TreeNode(int val) { this.val = val; }
    *     TreeNode(int val, TreeNode left, TreeNode right) {
    *         this.val = val;
    *         this.left = left;
    *         this.right = right;
    *     }
    * }
    */
   class Solution {
       int  res=0;
       public int minCameraCover(TreeNode root) {
           // 对根节点的状态做检验,防止根节点是无覆盖状态 .
           if(minCame(root)==0){
               res++;
           }
           return res;
       }
       /**
        节点的状态值：
        0 表示无覆盖
        1 表示 有摄像头
        2 表示有覆盖
        后序遍历，根据左右节点的情况,来判读 自己的状态
        */
       public int minCame(TreeNode root){
           if(root==null){
               // 空节点默认为 有覆盖状态，避免在叶子节点上放摄像头
               return 2;
           }
           int left=minCame(root.left);
           int  right=minCame(root.right);
   
           // 如果左右节点都覆盖了的话, 那么本节点的状态就应该是无覆盖,没有摄像头
           if(left==2&&right==2){
               //(2,2)
               return 0;
           }else if(left==0||right==0){
               // 左右节点都是无覆盖状态,那 根节点此时应该放一个摄像头
               // (0,0) (0,1) (0,2) (1,0) (2,0)
               // 状态值为 1 摄像头数 ++;
               res++;
               return 1;
           }else{
               // 左右节点的 状态为 (1,1) (1,2) (2,1) 也就是左右节点至少存在 1个摄像头，
               // 那么本节点就是处于被覆盖状态
               return 2;
           }
       }
   }
   
   ```

   



## day34 2025/3/2

### 动态规划dp

动态规划中每一个状态一定是由上一个状态推导出来的，**这一点就区分于贪心**，贪心没有状态推导，而是从局部直接选最优的，

**对于动态规划问题，我将拆解为如下五步曲，这五步都搞清楚了，才能说把动态规划真的掌握了！**

1. **确定dp数组（dp table）以及下标的含义**
2. **确定递推公式**
3. dp数组如何初始化
4. 确定遍历顺序
5. 举例推导dp数组

其实可以自己先思考这三个问题：

- 这道题目我举例推导状态转移公式了么？
- 我打印dp数组的日志了么？
- 打印出来了dp数组和我想的一样么？

1. **509 斐波那契数列**

   这道题递归和dp都可以做

   ```
   class Solution {
       public int fib(int n) {
           if (n <= 1) return n;             
           int[] dp = new int[n + 1];
           dp[0] = 0;
           dp[1] = 1;
           for (int index = 2; index <= n; index++){
               dp[index] = dp[index - 1] + dp[index - 2];
           }
           return dp[n];
       }
   }
   ```

   

## day35 2025/3/3

### dp

1. **70 爬楼梯**

   状态转移：dp[i]=dp[i-1]+dp[i-2]

   ```
   class Solution {
       public int climbStairs(int n) {
   
           //状态转移公式
           //dp[i]=dp[i-1]+dp[i-2];
           int[] dp=new int[n+1];
           if(n==1) return 1;
           dp[0]=1;
           dp[1]=1;
           for (int i = 2; i <= n; i++) {
               dp[i]=dp[i-1]+dp[i-2];
           }
           return dp[n];
       }
   }
   ```

   

2. **746 如何使用最小花费爬楼梯**

   这里面的dp含义是==**dp[i]的定义：到达第i台阶所花费的最少体力为dp[i]**。==

   **可以有两个途径得到dp[i]，一个是dp[i-1] 一个是dp[i-2]**。两者取最小

   dp[i - 1] 跳到 dp[i] 需要花费 dp[i - 1] + cost[i - 1]。

   dp[i - 2] 跳到 dp[i] 需要花费 dp[i - 2] + cost[i - 2]。

   ```
   class Solution {
       public int minCostClimbingStairs(int[] cost) {
           int length = cost.length;//楼梯的总长度
           //dp[i]=min(dp[i-1],dp[i-2]);到达当前楼梯的最小花费
           int[] dp = new int[length + 1];
           dp[0] = 0;
           dp[1] = 0;
           for (int i = 2; i <= length; i++) {
               //从dp[i-1]跳到dp[i]需要花费dp[i-1]+cost[i-1]
               //dp[i-2]跳到dp[i]需要花费dp[i-2]+cost[i-2]
               dp[i] = Math.min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2]);
           }
           return dp[length];
   
       }
   }
   ```

3. **62 不同路径**

   这是我自己写的题解

   ```
   class Solution {
       public int uniquePaths(int m, int n) {
           if (m == 1 || n == 1) return 1;//边界判断，只有一种情况
           int[][] dp = new int[m][n];//二维数组记录dp[i][j]时有多少种走法
           int start = 0;
           int endRow = m - 1;
           int endCol = n - 1;
           //开始初始化
           dp[0][0] = 0;
           dp[0][1] = 1;
           dp[1][0] = 1;
           for (int i = 0; i < m; i++) {
               for (int j = 0; j < n; j++) {
   
                   if (i >0 && j > 0) {//去掉第一行第一列，到达当前的坐标有两种选择
                       dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
                   } else if (i == 0 && j > 1) {//第一行
                       dp[i][j] = dp[i][j - 1];
                   } else if (i > 1 && j == 0) {//第一列
                       dp[i][j] = dp[i - 1][j];
                   }
               }
           }
           return dp[endRow][endCol];
   
       }
   }
   ```

   

4. **63 不同路径II -- -与上题不同的是，这道题的方格中存在障碍物**

   我自己写的答案

   只要遇到障碍物，就把那个方格的dp设置为0就行

   ==其实只要考虑到，遇到障碍dp[i][j]保持0就可以了。==

   ==也有一些小细节，例如：初始化的部分，很容易忽略了障碍之后应该都是0的情况。==

   ```
   class Solution {
       public int uniquePathsWithObstacles(int[][] obstacleGrid) {
           final int row = obstacleGrid.length;
           final int col = obstacleGrid[0].length;
           if(obstacleGrid[0][0]==1) return 0;
           if(row==1&&col==1) {
               return 1;
           }
           int[][] dp=new int[row][col];
           dp[0][0]=1;
           //第一列
           for (int i = 1; i < row; i++) {
               if(obstacleGrid[i][0]==1){
                   dp[i][0]=0;
               }else {
                   dp[i][0]=dp[i-1][0];
               }
           }
           //第一行
           for (int i = 1; i < col; i++) {
               if(obstacleGrid[0][i]==1){
                   dp[0][i]=0;
               }else {
                   dp[0][i]=dp[0][i-1];
               }
           }
   
           for (int i = 1; i < row; i++) {
               for (int j = 1; j < col; j++) {
                   if(obstacleGrid[i][j]==1){
                       //如果遇到了障碍物
                       dp[i][j]=0;
                   }
                   else {
                       dp[i][j]=dp[i-1][j]+dp[i][j-1];
                   }
               }
           }
           return dp[row-1][col-1];
   
       }
   }
   
   ```

   

5. **343 整数拆分**

   递推公式：

    **==//dp[i] = max({dp[i], (i - j) * j, dp[i - j] * j});==**

   其实第二层循环的范围控制在j<=i-j就可以了，只不过是下面的是dp[i - j] * j

   ```
   class Solution {
       public int integerBreak(int n) {
           int[] dp = new int[n + 1];
           if (n == 2) return 1;
           dp[2] = 1;
           int max = 0;
           //递推公式
           //dp[i] = max({dp[i], (i - j) * j, dp[i - j] * j});
           for (int i = 3; i <= n; i++) {
               for (int j = 1; j <= i - 1; j++) {
                   dp[i] =Math.max(dp[i],Math.max(dp[j]*(i-j),j*(i-j)));
               }
           }
           return dp[n];
       }
   }
   ```

   

6. **96 不同的二叉搜索树**

   这道题的递推公式优点复杂，需要好好想一想，而且这道题用的也是双层循环

   ==递推公式： dp[i] += dp[j - 1] * dp[i - 1 - (j - 1)];== 其实就是以每个节点为根节点的时候相加的二叉搜索树

   **dp[3]，就是 元素1为头结点搜索树的数量 + 元素2为头结点搜索树的数量 + 元素3为头结点搜索树的数量**

   元素1为头结点搜索树的数量 = 右子树有2个元素的搜索树数量 * 左子树有0个元素的搜索树数量

   元素2为头结点搜索树的数量 = 右子树有1个元素的搜索树数量 * 左子树有1个元素的搜索树数量

   元素3为头结点搜索树的数量 = 右子树有0个元素的搜索树数量 * 左子树有2个元素的搜索树数量

   所以dp[3] = dp[2] * dp[0] + dp[1] * dp[1] + dp[0] * dp[2]

   ```
   class Solution {
       public int numTrees(int n) {
   
           //确定递推公式
           if (n == 1) return 1;
           if (n == 2) return 2;
           int[] dp = new int[n + 1];
           dp[0] = 1;
           dp[1] = 1;
           dp[2] = 2;
           for (int i = 3; i <= n; i++) {
               for (int j = 1; j <= i; j++) {
                   dp[i] += dp[j - 1] * dp[i - 1 - (j - 1)];
               }
           }
           return dp[n];
       }
   }
   ```

   

## day36 2025/3/4

### 动态规划 dp - 01背包

1. **01背包问题  -- 这个问题是经典的动态规划问题**

   设置好二维数组dp，**dp[i][j] 表示从下标为[0-i]的物品里任意取，放进容量为j的背包，价值总和最大是多少**

   假如物品：

   ![image-20250304144353164](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250304144353164.png)

   确定好递推公式：

   ```
   dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);
   ```

   

   ![image-20250304144323822](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250304144323822.png)

​	==**物品当作行数，背包重量当作列数**==

==**可以先遍历物品再遍历背包容量：**==

遍历的顺序是从第二行第一列开始遍历：

```
// weight数组的大小 就是物品个数
for(int i = 1; i < weight.size(); i++) { // 遍历物品
    for(int j = 0; j <= bagweight; j++) { // 遍历背包容量
        if (j < weight[i]) dp[i][j] = dp[i - 1][j];
        else dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);

    }
}
```

**==关于dp数组初始化: 第一列初始化为0，第一行中，从weight[0]到bagweight初始化为value[0]，因为只能装下第0个物品==**

```
for (int i = 1; i < weight.size(); i++) {  // 当然这一步，如果把dp数组预先初始化为0了，这一步就可以省略，但很多同学应该没有想清楚这一点。
    dp[i][0] = 0;
}
// 正序遍历
for (int j = weight[0]; j <= bagweight; j++) {
    dp[0][j] = value[0];
}
```



2. **01背包问题  --- 滚动数组**

   滚动数组，其实就是一维数组，将一维数组设置为滚动数组的前提是，数组元素可以重复使用，一维dp数组，其实就上上一层 dp[i-1] 这一层 拷贝的 dp[i]来。

   使用一维数组来进行求解，**一维数组的使用和二维数组有很大不同**

   ```
   在一维dp数组中，dp[j]表示：容量为j的背包，所背的物品价值可以最大为dp[j]。
   ```

   ```
   递推公式为：dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
   ```

   ```
   dp数组初始化的时候，都初始为0就可以了。
   ```

   ```
   for(int i = 0; i < weight.size(); i++) { // 遍历物品
       for(int j = bagWeight; j >= weight[i]; j--) { // 遍历背包容量
           dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
   
       }
   }
   ```

   1. ==一维数组遍历背包地时候，是从大到小遍历，而且范围是[bagweight, weight[i]]，和上面那道题中二维数组不同，==**倒序遍历是为了保证物品i只被放入一次！**。但如果一旦正序遍历了，那么物品0就会被重复加入多次！对于二维dp，dp[i][j]都是通过上一层即dp[i - 1][j]计算而来，本层的dp[i][j]并不会被覆盖！

   2. ==for循环嵌套的顺序也不能变，只能是先遍历物品再遍历背包容量==,因为一维dp的写法，背包容量一定是要倒序遍历（原因上面已经讲了），如果遍历背包容量放在上一层，那么每个dp[j]就只会放入一个物品，即：背包里只放入了一个物品。

      

3. **416 分割等和子集**

   就是比较典型的01背包问题，这里面背包容量是sum/2，物品的重量和价值都是nums[i]

   ==注意的地方是dp数组的初始化大小， int[] dp = new int[sum / 2 + 1];==

   ```
   class Solution {
       public boolean canPartition(int[] nums) {
           //背包容量就是数组和的一半
           final int sum = Arrays.stream(nums).sum();
           if (sum % 2 != 0) return false;
           int[] dp = new int[sum / 2 + 1];
           //背包就是数组的长度
           //length = nums.length;
           //一维dp遍历
           //dp[j]=max(dp[j],dp[j-weight[i]]+value[i])
   
           for (int i = 0; i < nums.length; i++) {//相当于背包个数
   
               for (int j = sum / 2; j >= nums[i]; j--) {//相当于背包容量
                   dp[j] = Math.max(dp[j], dp[j - nums[i]] + nums[i]);
               }
               if (dp[sum/2] == sum / 2) return true;
           }
           return false;
   
       }
   }
   ```

   

4. **1049 最后一块石头的重量II** 

   这道题和上述题目类型完全一致，旨在找到重量最接近的两堆石头，进行撞击，这样剩余的重量才是最小的

   最后相减的时候有个小tips，是`diff-dp[target]`，而不是`diff-target`

   ```
   class Solution {
       public int lastStoneWeightII(int[] stones) {
           //理解本题的核心含义：其实是让石头分成重量差不多的两堆，相撞之后，剩下的就是最小的
           //计算数组总和
           final int sum = Arrays.stream(stones).sum();
           //if (sum / 2 == 0) return 0;
           int target = sum / 2;
           int[] dp = new int[target + 1];
   
           for (int i = 0; i < stones.length; i++) {
   
               for (int j = target; j >= stones[i]; j--) {
                   dp[j] = Math.max(dp[j], dp[j - stones[i]] + stones[i]);
               }
   
           }
           int diff = sum - dp[target];
           return Math.abs(diff - dp[target]);
       }
   }
   
   ```

   

5. **494 目标和**

   这道题有点难想，主要还有个推导，而且递推公式跟上面的01背包问题也不相同

   本题要如何使表达式结果为target，

   既然为target，那么就一定有 ==left组合 - right组合 = target。==

   ==left + right = sum==，而sum是固定的。right = sum - left

   left - (sum - left) = target 推导出 ==left = (target + sum)/2 。==

   target是固定的，sum是固定的，left就可以求出来。

   ==**此时问题就是在集合nums中找出和为left的组合。**==

   **递推公式**：`dp[j] = dp[j] + dp[j - nums[i]]` 

   **dp[0] 初始为1 ,即装满背包为0的方法有一种，放0件物品**

   - **不放物品i**：即背包容量为j，里面不放物品i，装满有dp[i - 1][j]中方法。
   - **放物品i**： 即：先空出物品i的容量，背包容量为（j - 物品i容量），放满背包有 dp[i - 1][j - 物品i容量] 种方法。

   ![image-20250304195848596](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250304195848596.png)

   ```
   class Solution {
       public int findTargetSumWays(int[] nums, int target) {
           //有数学功底
           final int sum = Arrays.stream(nums).sum();
           if (Math.abs(target) > sum) return 0;//如果比总和大，肯定是没有的
           if ((sum + target) % 2 != 0) return 0;
   
           //这样推导公式：
           //left-right=target;
           //left+right=sum;
           //left=(sum+target)/2;
           //找到组合等于left,转化成了背包问题
           //递推公式也比较难想，dp[j]=dp[j]+dp[j-nums[i]]
           //dp[j]代表背包容量为j时有多少种方法
           int left = (sum + target) / 2;
           int[] dp = new int[left + 1];
           dp[0] = 1;//这部分的初始化也很重要
           for (int i = 0; i < nums.length; i++) {
               for (int j = left; j >= nums[i]; j--) {
                   dp[j] = dp[j] + dp[j - nums[i]];
               }
           }
           return dp[left];
       }
   }
   ```

   



6. **474 一和零**

   这道题比较难，主要在于这个背包的重量有两个维度。不再是以前的一个维度

   //而且这个是三层循环

   **如果是往常一维dp数组，外层for循环遍历物品，内层for循环遍历背包容量，而且要倒叙**

   ==**在这里面，外层for循环就是字符串，内层for循环就是背包两个维度的容量，而且是倒叙遍历，仔细去看，其实这里面的二维dp数组就是相当于以往的一维dp数组**==

   ```
   class Solution {
       public int findMaxForm(String[] strs, int m, int n) {
   
   
           //这道题还是01背包问题，只不过背包问题有两个维度
           int[][] dp=new int[m+1][n+1];
           //这个初始化都是0就行了
           int count0=0;
           int count1=0;
           for (String str : strs) {
               final char[] chars = str.toCharArray();
               count0=0;
               count1=0;
               for (char aChar : chars) {
                   if(aChar=='1') count1++;else count0++;
               }
               //遍历背包
               //双层循环
               //倒序遍历
               for (int i=m;i>=count0;i--){//控制循环范围
                   for (int j=n;j>=count1;j--){//控制循环范围
   
                       dp[i][j]=Math.max(dp[i][j],dp[i-count0][j-count1]+1);
                   }
               }
           }
           return dp[m][n];
   
       }
   }
   ```

   

## day37 2025/3/5

### 动态规划 dp  -- 完全背包问题   -- 组合排列（对于一维dp数组来说）

1. **完全背包问题：**    **==完全背包问题就是每种物品有无限个，从二维数组出发==**

   **递推公式：**

   ```
   dp[i][j] = max(dp[i - 1][j], dp[i][j - weight[i]] + value[i]);
   ```

   ==注意，完全背包二维dp数组 和 01背包二维dp数组 递推公式的区别，01背包中是 `dp[i - 1][j - weight[i]] + value[i])`==

   **初始化：**

   ```java
   
   // 初始化
   //把i=0的这一行初始化， 从大于等于weight[0]的开始遍历
   //第一列还是都是0，所以也不用初始化
           for (int j = weight[0]; j <= bagWeight; j++) {
               dp[0][j] = dp[0][j - weight[0]] + value[0];
           } //这个代表，只要能装下他，就一直装
   
   		// 动态规划
           for (int i = 1; i < n; i++) {
               for (int j = 0; j <= bagWeight; j++) {
                   if (j < weight[i]) {
                       dp[i][j] = dp[i - 1][j];
                   } else {
                       dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - weight[i]] + value[i]);
                   }
               }
           }
   ```

2. **518 零钱兑换II**----- **组合 -- 完全背包问题**   **-- 注意组合数和排列数的区别**

   - 一维dp的时候，==如果求组合数就是外层for循环遍历物品，内层for遍历背包。==
   - 一维dp的时候，==如果求排列数就是外层for遍历背包，内层for循环遍历物品。==

   是一道完全背包问题，但是与完全背包问题又不一样。**背包问题是小于等于背包容量的情况下统计最大价值**

   这道题是**计算并返回可以凑成总金额的硬币组合数**。是**==统计组合的数量==**，还要注意要凑成总金额，相当于**==背包容量要装满==**

   **这道题和494目标和的递推公式是一样的，初始化也是类似的**

   ==初始化：==

   ==第一行：==

   ```
   for (int i = coins[0]; i <= amount; i++) {
               //题目中要求是装满背包的最大组合方式
               if (i % coins[0] == 0) dp[0][i] = 1;//如果可以整除就说明可以装满，就一种组合方式
               //剩下的都装不满就说明没有组合方式
           }
   ```

   ==第一列：初始化为1，因为背包容量为0的时候，装满的方式只有一种，就是什么都不装==

           for (int i = 0; i < coins.length; i++) {
               dp[i][0] = 1;//容量为0的时候，装满就只有一种组合方式，就是不装
           }

   ```
   class Solution {
       public int change(int amount, int[] coins) {
           //完全背包问题
           int[][] dp = new int[coins.length][amount + 1];
           //开始初始化,初始化第一行
           for (int i = coins[0]; i <= amount; i++) {
               //题目中要求是装满背包的最大组合方式
               if (i % coins[0] == 0) dp[0][i] = 1;//如果可以整除就说明可以装满，就一种组合方式
               //剩下的都装不满就说明没有组合方式
           }
           //初始化第一列
           for (int i = 0; i < coins.length; i++) {
               dp[i][0] = 1;//容量为0的时候，装满就只有一种组合方式，就是不装
           }
           for (int i = 1; i < coins.length; i++) {
               for (int j = 0; j <= amount; j++) {
                   if (j < coins[i]) dp[i][j] = dp[i - 1][j];
                   else {
                       //递推公式的构造要从装它和不装它两个方面考虑
                       dp[i][j] = dp[i - 1][j] + dp[i][j - coins[i]];
                   }
               }
           }
   
           return dp[coins.length - 1][amount];
   
   
       }
   }
   
   ```

   **==注意！！！！：==**完全背包本题一维dp的for循环的内层遍历顺序不太一样，内层循环就不是倒序，就可以正序，因为无限个。**完全背包的物品是可以添加多次的，所以遍历背包容量要从小到大去遍历**

   ```
   dp[0] = 1; // 只有一种方式达到0
   for (int i = 0; i < coins.size(); i++) { // 遍历物品
       for (int j = coins[i]; j <= amount; j++) { // 遍历背包容量
           dp[j] += dp[j - coins[i]];
       }
   }
   ```

   **==一维数组中，如果是排列，外循环是容量，内循环是物品==**

   ```
   for (int j = 0; j <= amount; j++) { // 遍历背包容量
       for (int i = 0; i < coins.size(); i++) { // 遍历物品
           if (j - coins[i] >= 0) dp[j] += dp[j - coins[i]];
       }
   }
   ```

   **对于二维dp数组来说，外循环和内循环，不管是容量还是物品，解决的都是组合问题**

   

3. **377组合总和IV**

   这道题就是排列问题

   所以这道题：采用的是一维dp数组，外循环是容量，内循环是物品，要注意里面有一个判断条件

   ```
   class Solution {
       public int combinationSum4(int[] nums, int target) {
   
           //完全背包问题
           //其实是个排列问题
           int[] dp=new int[target+1];
           dp[0]=1;
           //一维数组
   
           //循环顺序，外循环是背包容量，内循环是物品
           for (int i = 0; i <= target; i++) {
               for (int j=0;j<nums.length;j++){
                   if(i>=nums[j]){
                       dp[i]=dp[i]+dp[i-nums[j]];
                   }
   
               }
   
           }
           return dp[target];
       }
   }
   ```

   

4. **爬楼梯 -- 进阶版**     

   这道题将原来爬楼梯的题目稍微变化一下，每次不是只能爬一阶或者两阶。而是可以爬[1,m]阶，那么这个1，2，3，4，，m就是物品，n阶台阶就是背包容量，这样这道题目就转换成一道排列问题的完全背包问题

   ```
   dp[0]=1;
   //For循环的嵌套顺序
   for(int i=1,i<=target;i++){
   	for(int j=1,j<m;j++){
   	if(i>=j) dp[i]=dp[i]+dp[i-j];
   	}
   }
   ```

   

## day38 2025/3/6

### 动态规划dp  -- 完全背包- 求最小的个数问题-- 遍历顺序   -- 打家劫舍



1. **322 零钱兑换**

   这道题目求的是最少的硬币数

   **==没有通过的原因在于使用二维dp的时候 对第一行的初始化失败，这道题的关键在于第一行的初始化==**

   **，第一行中除了能够整除第一个硬币的，剩下都设置为最大值，因为如果默认为0，后面在找最小值的时候容易被覆盖，只需要对第一行中部分赋值并且设置最大值即可**

   第一列都是设置为0

   ```
           //第一列
           for (int i = 0; i < coins.length; i++) {
               dp[i][0] = 0;
           }
           //第一行
           for (int i = 0; i <= amount; i++) {
               if (i % coins[0] == 0) {
                   dp[0][i] = i / coins[0];
               } else dp[0][i] = Integer.MAX_VALUE;
           }
   ```

   ```
   class Solution {
       public int coinChange(int[] coins, int amount) {
   
   
           //完全背包问题
           int[][] dp = new int[coins.length][amount + 1];
           //初始化
           if (amount == 0) return 0;
           //初始化dp为最大值
           //第一列
           for (int i = 0; i < coins.length; i++) {
               dp[i][0] = 0;
           }
           //第一行
           for (int i = 0; i <= amount; i++) {
               if (i % coins[0] == 0) {
                   dp[0][i] = i / coins[0];
               } else dp[0][i] = Integer.MAX_VALUE;
           }
           //遍历
           for (int i = 1; i < coins.length; i++) {
   
               for (int j = 1; j <= amount; j++) {
   
                   if (j < coins[i]) dp[i][j] = dp[i - 1][j];
                   else {
                       if (dp[i][j - coins[i]] != Integer.MAX_VALUE)
                           dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - coins[i]] + 1);
                           
                       else dp[i][j] = dp[i - 1][j];
                   }
               }
           }
   
           if (dp[coins.length - 1][amount] == Integer.MAX_VALUE) return -1;
           else return dp[coins.length - 1][amount];
       }
   }
   ```

   上面遍历的过程中，`判断dp[i][j - coins[i]] != Integer.MAX_VALUE`，如果是最大值的话，那么就不能按照min那个公式，就得还要赋值是上一个的，因为没有意义，而且加一肯定是溢出的了

   

2.  **279 完全平方数**  **- - ==学会用Arrays.fill()填充一维dp数组==**

   **这道题就是只能用一维dp数组去做，为什么呢，因为行数根本是不知道的，所以只能用一维dp数组**

   这是我自己写的答案

   ```
   class Solution {
       public int numSquares(int n) {
           int[] dp = new int[n + 1];
           //初始化
   		Arrays.fill(dp, Integer.MAX_VALUE);
           dp[0] = 0;//因为n>=1
           int start = 1;
           int sqrt = start * start;
           while (sqrt <= n) {
   
               for (int i = sqrt; i <= n; i++) {
                   if (dp[i - sqrt] != Integer.MAX_VALUE) {
                       dp[i] = Math.min(dp[i], dp[i - sqrt] + 1);
                   }
               }
               start++;
               sqrt = start * start;
           }
           return dp[n];
       }
   }
   ```

   

3. **139 单词拆分**

   没看懂，这道题不会做

   ```
   class Solution {
       public boolean wordBreak(String s, List<String> wordDict) {
   
           HashSet<String> set = new HashSet<>(wordDict);
           boolean[] valid = new boolean[s.length() + 1];
           valid[0] = true;
   
           for (int i = 1; i <= s.length(); i++) {
               for (int j = 0; j < i && !valid[i]; j++) {
                   if (set.contains(s.substring(j, i)) && valid[j]) {
                       valid[i] = true;
                   }
               }
           }
   
           return valid[s.length()];
           
       }
   }
   ```

   

4. **==198 打家劫舍    --经典dp问题==**

   这道题不是背包问题，不要套用背包问题的公式

   **确定dp[i]**

   **当前房屋偷还是不偷取决于上一个房屋和上上一个房屋**

   **如果当前不偷，dp[i]=dp[i-1]**

   **如果当前偷,dp[i]=dp[i-2]+nums[i]**

   **两者取最大值**

   ```
   class Solution {
       public int rob(int[] nums) {
           if(nums.length==1) return nums[0];
   
           //这道题不是背包问题
           //当前房屋偷还是不偷取决于第i-1房屋和第i-2房屋偷还是不偷
           int[] dp=new int[nums.length];
           //初始化
           dp[0]=nums[0];
           dp[1]=Math.max(nums[0],nums[1]);
           for (int i = 2; i < nums.length; i++) {
               dp[i]=Math.max(dp[i-2]+nums[i],dp[i-1]);
           }
           return dp[nums.length-1];
   
       }
   }
   ```

   

5. **213 打家劫舍II --  区别在于房屋是环状结构**

   这道题综合起来考虑两种情况

   重点强调了情况一二三是“考虑”的范围，而具体房间偷与不偷交给递推公式去抉择。

   ==环状结构下面三种情况合起来就是两种情况，就是情况二和情况三==

   1. ==考虑不包含尾元素，也就是说假如房屋1考虑在偷的范围里==
   2. ==考虑不包含首元素，也就是最后一个房屋考虑在偷的范围里==

   ![image-20250306203452253](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250306203452253.png)

   ```
   class Solution {
       public int rob(int[] nums) {
   
           //打家劫舍的第一个升级版
           if (nums.length == 1) return nums[0];
   
           final int length = nums.length;
           //初始化
           //环的话：考虑两种情况
           //考虑第一种情况：不包含尾元素
           int result1 = getInts(nums, 0, length - 2);
           //考虑第二种情况：不包含首元素
           int result2 = getInts(nums, 1, length - 1);
           //最大值
           return Math.max(result1, result2);
       }
       private int getInts(int[] nums, int start, int end) {
           if (start == end) return nums[start];//如果只有一个元素，直接返回
           int[] dp = new int[nums.length];
           dp[start] = nums[start];
           dp[start + 1] = Math.max(nums[start], nums[start + 1]);
           for (int i = start + 2; i <= end; i++) {
               dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
           }
           return dp[end];
       }
   
   }
   ```

   

6. **337 打家劫舍III**  

   **房屋是树形结构，这道题目是==树形dp==**

   首先确定树的遍历：后序遍历

   还是挺难的，一方面忘了树的遍历，另一方面不知道怎么dp

   **dp数组就是一个长度为2的数组**

   如果是偷当前节点，那么左右孩子就不能偷，val1 = cur->val + left[0] + right[0]; （**如果对下标含义不理解就再回顾一下dp数组的含义**）

   如果不偷当前节点，那么左右孩子就可以偷，至于到底偷不偷一定是选一个最大的，所以：val2 = max(left[0], left[1]) + max(right[0], right[1]);

   最后当前节点的状态就是{val2, val1}; 即：{不偷当前节点得到的最大金钱，偷当前节点得到的最大金钱}

   ```
   class Solution {
       public int rob(TreeNode root) {
           //树的遍历采用后序遍历左右中
           //状态标记递归
           int[] result = dfs(root);
           return Math.max(result[0], result[1]);
   
       }
       public int[] dfs(TreeNode root) {
   
           if (root == null) return new int[]{0, 0};//空节点，递归出口
           //后序遍历
           int[] left = dfs(root.left);
   
           int[] right = dfs(root.right);
           //中
           //对中间节点做处理
           //如果不偷，那么可以考虑偷左右孩子节点,可以偷也可以不偷，具体取最大值
           int[] result = new int[2];
           result[0] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
           //如果偷，那么左右孩子节点不能偷
           result[1] = root.val + left[0] + right[0];
           return result;
   
   
       }
   
   }
   ```

   

## day39 2025/3/7

### dp -- 买卖股票全集

1. **121 买卖股票的最佳时机** ，**只能买一次只能卖一次     --- 有两种解决方法**  

   **==因为股票全程只能买卖一次，所以如果买入股票，那么第i天持有股票即dp[i][0]一定就是 -prices[i]。==**

   `dp[i][0]` `dp[i][1]` 代表当前持有和不持有

   递推公式：

   如果第i天持有股票即dp[i][0]， 那么可以由两个状态推出来

   - 第i-1天就持有股票，那么就保持现状，所得现金就是昨天持有股票的所得现金 即：dp[i - 1][0]
   - 第i天买入股票，所得现金就是买入今天的股票后所得现金即：-prices[i]

   如果第i天不持有股票即dp[i][1]， 也可以由两个状态推出来

   - 第i-1天就不持有股票，那么就保持现状，所得现金就是昨天不持有股票的所得现金 即：dp[i - 1][1]
   - 第i天卖出股票，所得现金就是按照今天股票价格卖出后所得现金即：prices[i] + dp[i - 1][0]

   ```
   class Solution {
       public int maxProfit(int[] prices) {
   
           //二维表示持有和不持有
           if(prices.length==1) return 0;
           int[][] dp=new int[prices.length][2];
           //数组初始化
           dp[0][0]=-prices[0];//第一天持有就是买入股票
           dp[0][1]=0;//第一天不持有，不考虑买入，就不会花钱
           //持有不代表买入，也可能是前一天买入，今天继续保持已有的状态
           for (int i = 1; i < prices.length; i++) {
               //持有的状态
               dp[i][0]=Math.max(dp[i-1][0],-prices[i]);//只能买一次
               //不持有
               dp[i][1]=Math.max(dp[i-1][1],dp[i-1][0]+prices[i]);
           }
           return dp[prices.length-1][1];
           
       }
   }
   ```

   还可以用别的方法，买卖各自就只有一次，所以我们可以记录当前遍历到的最小值，然后用当前数值减去最小值，不断更新

   ```
      int min = Integer.MAX_VALUE;
           int result = 0;
           if(prices.length==1) return 0;
           for (int i = 0; i < prices.length; i++) {
               min = Math.min(min, prices[i]);//获取到当前最小值
               //找到右边最大值
               result=Math.max(result,prices[i]-min);
           }
           return result;
   ```

   

2.  **122 买卖股票时机II   --- 一支股票可以买卖多次** 

   推导公式与上述不同的地方在于，**因为一只股票可以买卖多次，所以当第i天买入股票的时候，所持有的现金可能有之前买卖过的利润。**

   如果第i天持有股票即dp[i][0]， 那么可以由两个状态推出来

   - 第i-1天就持有股票，那么就保持现状，所得现金就是昨天持有股票的所得现金 即：dp[i - 1][0]

   - 第i天买入股票，所得现金就是昨天不持有股票的所得现金减去 今天的股票价格 即：dp[i - 1][1] - prices[i]

   -             dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
                 dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] + prices[i]);

   ```
          if (prices.length == 1) return 0;
           int[][] dp = new int[prices.length][2];
           //初始化
           dp[0][0] = -prices[0];
           dp[0][1] = 0;
           for (int i = 1; i < prices.length; i++) {
               dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
               dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
           }
           if (dp[prices.length - 1][1] < 0) return 0;
           else return dp[prices.length - 1][1];
   
   ```

   

3. **123 买卖股票III  挺难的一道题**

   设置五个状态

   ```
   class Solution {
       public int maxProfit(int[] prices) {
   
           //每天股票都只有五种状态
           //0：不操作，1：第一次买入，2：第一次卖出 3：第二次买入 4：第二次卖出
           if(prices.length==1) return 0;
           int[][] dp=new int[prices.length][5];
   
           //初始化
           dp[0][1]=-prices[0];
           dp[0][3]=-prices[0];
           for (int i = 1; i < prices.length; i++) {
               //第一次买入
               dp[i][1]=Math.max(dp[i-1][1],-prices[i]);
               //第一次卖出
               dp[i][2]=Math.max(dp[i-1][2],dp[i-1][1]+prices[i]);
               //第二次买入
               dp[i][3]=Math.max(dp[i-1][3],dp[i-1][2]-prices[i]);
               //第二次卖出
               dp[i][4]=Math.max(dp[i-1][4],dp[i-1][3]+prices[i]);
           }
           if(dp[prices.length-1][4]<0) return 0;
           else  return dp[prices.length-1][4];
       }
   }
   ```

   

4. **188买卖股票IV**

   **与上道题思路相同，主要就是在遍历过程中，初始化过程中，注意长度是2*k+1!!!不是dp.length，这个是求行数**

   ```
   class Solution {
       public int maxProfit(int k, int[] prices) {
           //多维状态
           if (prices.length == 1) return 0;
           int[][] dp = new int[prices.length][k * 2 + 1];
           //无操作，第一次买入，第一次卖出；第二次买入，第二次卖出；。。。。第k次买入，第k次卖出
           //初始化
           for (int i = 1; i < k * 2 + 1; i++) {
               if (i % 2 == 1)
                   dp[0][i] = -prices[0];
           }
           for (int i = 1; i < prices.length; i++) {
   
               for (int j = 1; j < k * 2 + 1; j++) {
   
                   if (j == 1) {
                       dp[i][j] = Math.max(dp[i - 1][j], -prices[i]);
                   } else {
                       if (j % 2 == 0) {
                           //偶数代表卖出
                           dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - 1] + prices[i]);
                       } else {
                           //奇数代表买入
                           dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - 1] - prices[i]);
                       }
                   }
               }
           }
           return  dp[prices.length - 1][k*2];
       }
   }
   
   ```

   

## day40 2025/3/9

### 动态规划 -- 含有冷冻期、手续费

1. **309买卖股票（含有冷冻期）**

   每天就分为四个状态

   ![image-20250309180253664](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250309180253664.png)

   ```
   class Solution {
       public int maxProfit(int[] prices) {
   
           if (prices.length == 1) return 0;
           //设置四个状态
           int[][] dp = new int[prices.length][4];
           //初始化
           dp[0][0]=-prices[0];//持有状态
           dp[0][1]=0;//保持卖出状态
           dp[0][2]=0;//今天就卖出
           dp[0][3]=0;//今天是冷冻期
           for (int i = 1; i < prices.length; i++) {
               //持有状态的选择
               dp[i][0]=Math.max(dp[i-1][0],Math.max(dp[i-1][1]-prices[i],dp[i-1][3]-prices[i]));
               //保持卖出的状态选择
               dp[i][1]=Math.max(dp[i-1][1],dp[i-1][3]);//前一天卖出，前一天是冷冻期
               //今天就卖出
               dp[i][2]=dp[i-1][0]+prices[i];
               //今天是冷冻期哦
               dp[i][3]=dp[i-1][2];//说明前一天卖出
           }
   return Math.max(Math.max(dp[prices.length-1][0],dp[prices.length-1][1]),
           Math.max(dp[prices.length-1][2],dp[prices.length-1][3]));
       }
   }
   
   ```

   

2.  **714 买卖股票的最佳时机含手续费**

   每一天有三个状态

   ```
   class Solution {
       public int maxProfit(int[] prices, int fee) {
           //设置三种状态
           if (prices.length == 1) return 0;
           int[][] dp = new int[prices.length][3];
           //1. 持有状态
           //2 保持卖出状态
           //3. 今天卖出
           dp[0][0] = -prices[0];
           dp[0][1] = 0;
           dp[0][2] = 0;
           for (int i = 1; i < prices.length; i++) {
               //持有状态
               dp[i][0] = Math.max(dp[i - 1][0], Math.max(dp[i - 1][1] - prices[i], dp[i - 1][2] - prices[i]));
               //保持卖出状态
               dp[i][1] = Math.max(dp[i - 1][2], dp[i - 1][1]);
               //今天卖出
               dp[i][2] = dp[i - 1][0] + prices[i] - fee;
           }
           return Math.max(dp[prices.length-1][1],dp[prices.length-1][2]);
   
       }
   }
   ```



## day41 2025/3/10

### dp  -- 最长递增子序列 -- 最长==连续==递增子序列  -- ==两个数组比较的重复部分 涉及dp二维数组==

1. **300 最长递增子序列**      **==非常典型dp子序列问题==**

   我没有想到的是双层循环，因为需要去比较nums[j]与nums[i] （j是在0到i之间遍历）

   递推公式：

   `if(nums[i]>nums[j])`{`
                       dp[i]=Math.max(dp[i],dp[j]+1);`

   dp[i]并不是代表从0-i的最长递增子序列，而是代表从0-i的里面，每个以nums[i]结尾的序列中最长递增子序列

   **注意，数组初始化为1**

   ```
   class Solution {
       public int lengthOfLIS(int[] nums) {
   
           if (nums.length == 1) return 1;
           int[] dp = new int[nums.length];
           int result=0;
           Arrays.fill(dp,1);
           for (int i = 1; i < nums.length; i++) {
   
               for (int j = 0; j < i; j++) {
                   if(nums[i]>nums[j]){
                       dp[i]=Math.max(dp[i],dp[j]+1);
                   }
               }
               result=Math.max(dp[i],result);
           }
           return Math.max(result,dp[nums.length-1]);
       }
   }
   ```

   

2. **674 最长连续递增序列**  

   我自己写的不用dp的做法

   ```
   class Solution {
       public int findLengthOfLCIS(int[] nums) {
           int len = 1;
           if (nums.length == 1) return 1;
           int left = 0;
           int maxLen = 1;
           int right = 1;
           while (right < nums.length) {
               if (nums[right] > nums[left]) {
                   len++;
                   right++;
                   left++;
               } else {
                   left = right;
                   right++;
                   maxLen = Math.max(maxLen, len);
                   len = 1;
               }
           }
           return Math.max(maxLen, len);
       }
   }
   ```

   **采用dp做法：这道题的dp比较简单，主要是与上一个进行比较，最后输出的结果，其实/对dp数组进行从小到大的排序，输出最大的那个就可以**

   ```
       public int findLengthOfLCIS(int[] nums) {
           if (nums.length == 1) return 1;
           int[] dp = new int[nums.length];
           Arrays.fill(dp, 1);
           for (int i = 1; i < nums.length; i++) {
               if (nums[i] > nums[i - 1]) {
                   dp[i] =  dp[i - 1] + 1;
               }
           }
           Arrays.sort(dp);
           return dp[nums.length-1];
       }
   
   ```

   

3. **718 最长重复子数组 -- 这个其实是连续比较**

   **比较两个数组的最长重复子序列，==涉及到比较两个数组==，那么应该想到==设计二维dp数组==**

   <img src="https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250310160255240.png" alt="image-20250310160255240" style="zoom:80%;" />

   二维dp数组的行和列的长度其实是nums1.length + 1和nums2.length + 1

   下面是递推公式，`nums[i-1]和nums2[j-1]`是因为索引多了1，防止越界

     ==`dp[i][j]`  `的状态只能由dp[i-1][j-1]推导出来`==  如果你发现当前两个字符相等，`那么就是只需要拿dp[i-1][j-1]`的结果加1就行，因为只需要比较去掉当前字符的前面字符串的情况就行

   ```
                   if (nums1[i - 1] == nums2[j - 1]) {//根据nums1和nums2的索引来的
                       dp[i][j] = dp[i - 1][j - 1] + 1; //dp[i][j]的状态只能由dp[i - 1][j - 1]推导出来
                   }
   ```

   ```
   class Solution {
       public int findLength(int[] nums1, int[] nums2) {
           //找到两个数组的重复部分
           //需要定义一个二维数组
           int[][] dp = new int[nums1.length + 1][nums2.length + 1];
           //初始化
           //第一行和第一列都是没有意义的
           for (int i = 0; i <= nums2.length; i++) {
               dp[0][i] = 0;
           }
           for (int i = 0; i <= nums1.length; i++) {
               dp[i][0] = 0;
           }
           //不断记录dp数组的最大值
           int maxResult = 0;
           for (int i = 1; i <= nums1.length; i++) {
   
               for (int j = 1; j <= nums2.length; j++) {
                   if (nums1[i - 1] == nums2[j - 1]) {//根据nums1和nums2的索引来的
                       dp[i][j] = dp[i - 1][j - 1] + 1;
                   }
                   maxResult = Math.max(maxResult, dp[i][j]);
               }
   
           }
           return maxResult;
   
       }
   }
   ```

   

4.  **1143 最长公共子序列  -  这道题不是连续**

   但是比较到相等字符的时候，所做的比较是一样的

   ```
   class Solution {
       public int longestCommonSubsequence(String text1, String text2) {
   
           //设置二维数组
           int[][] dp = new int[text1.length() + 1][text2.length() + 1];
           final char[] chars1 = text1.toCharArray();
           final char[] chars2 = text2.toCharArray();
           //初始化第一行
           for (int i = 0; i < text2.length() + 1; i++) {
               dp[0][i] = 0;
   
           }
           //初始化第一列
           for (int i = 0; i < text1.length(); i++) {
               dp[i][0] = 0;
           }
           //记录最大值
           int maxLen=0;
           for (int i = 1; i <= chars1.length; i++) {
   
               for (int j = 1; j <= chars2.length; j++) {
   
                   if (chars1[i - 1] == chars2[j - 1]) {
                       dp[i][j] = dp[i-1][j-1]+1; //如果相等的话，是斜上方+1，d
                       // p[i][j]的状态只能由dp[i - 1][j - 1]推导出来
   
                   } else {
                       dp[i][j]=Math.max(dp[i-1][j],dp[i][j-1]);
                   }
                   maxLen=Math.max(maxLen,dp[i][j]);
               }
           }
           return maxLen;
   
   
       }
   }
   ```

   

​		



## day42 2025/3/11

### dp  --不相交的线(最长公共子序列)  最大子数组和 -- 判断子序列 -- 不同子序列

1. ==**1035 不相交的线  -- 1143最长公共子序列的变体，和这道题目一样**==

   线不相交意味着找到公共子序列，并且子序列的相对顺序不改变，只要相对顺序不改变，那么线就不会相交

   所以这道题的代码跟1143最长公共子序列的代码其实是一样的

   ```
   class Solution {
       public int maxUncrossedLines(int[] nums1, int[] nums2) {
           //就是再找最长公共子序列，相对顺序不变
           //直线不能相交的意思就是子序列相对顺序不能改变
           //就变成了最长公共子序列,并且不是连续的
           int[][] dp = new int[nums1.length + 1][nums2.length + 1];
           //初始化
           for (int i = 0; i <= nums1.length; i++) {
               dp[i][0] = 0;
           }
           for (int i = 0; i <= nums2.length; i++) {
               dp[0][i] = 0;
           }
           //记录最大值
           int maxResult=0;
           for (int i = 1; i <= nums1.length; i++) {
   
               for (int j = 1; j <= nums2.length; j++) {
                   if (nums1[i - 1] == nums2[j - 1]) {
                       dp[i][j] = dp[i - 1][j - 1] + 1;
                   } else {
                       dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                   }
                   maxResult=Math.max(dp[i][j],maxResult);
               }
           }
           return maxResult;
   
       }
   }
   ```

   

2. **==53 最大子数组和==   -- 这道题之前用的是贪心解法，但他是一道很好的dp问题**

   最大连续子数组和，这里面要求连续子数组和，还要求最大，如何确定递推公式

   dp[i]是依赖于dp[i - 1]的状态，dp[i]定义是包括i 的最大子序列的和

   `dp[i]=dp[i-1]+nums[i]`

   `dp[i]=nums[i]`

   dp[i]要么加入前一个，要么自己独立，往后递推，不用想后面，只需要想开头怎么确定

   ```
   
           //确定dp递推公式
           if (nums.length == 1) return nums[0];
           int[] dp = new int[nums.length];
           //dp[i]=Math.max(nums[i-1]+nums[i],nums[i]);//保持连续
           //初始化
           dp[0] = nums[0];
           //记录最大值
           int maxResult = dp[0];
           for (int i = 1; i < nums.length; i++) {
               dp[i] = Math.max(dp[i - 1] + nums[i], nums[i]);
               maxResult = Math.max(dp[i], maxResult);
           }
           return maxResult;
   
   ```

   

3. **392 判断子序列 **   -- 编辑距离的入门题目，只需要计算删除的情况，不用考虑增加和替换的情况

   判断s是不是t的子序列，**==区别于1143最长公共子序列的地方在于：删除是只能删除字符串t的元素==**，所以 `dp[i][j]=dp[i][j-1]`

   dp解法：

   ```
   class Solution {
       public boolean isSubsequence(String s, String t) {
   
           //判断s是否是t的子序列
           int[][] dp = new int[s.length() + 1][t.length() + 1];
           for (int i = 0; i <= s.length(); i++) {
               dp[i][0] = 0;
           }
           for (int i = 0; i <= t.length(); i++) {
               dp[0][i] = 0;
           }
           int maxResult = 0;
           for (int i = 1; i <= s.length(); i++) {
               for (int j = 1; j <= t.length(); j++) {
                   if (s.charAt(i - 1) == t.charAt(j - 1)) {
                       dp[i][j] = dp[i - 1][j - 1] + 1;
                   } else {
                       dp[i][j]=dp[i][j-1];//这个地方只能删除t的字符，而 1143.最长公共子序列 是两个字符串都可以删元素
                   }
                   maxResult = Math.max(dp[i][j], maxResult);
               }
           }
           if (maxResult == s.length()) return true;
           else return false;
       }
   }
   ```

   双指针的解法：

   ```
           //定义两个双指针
           int sindex = 0;
           int tindex = 0;
           int count = 0;
           if(s.length()>t.length()) return false;
           while (sindex < s.length()) {
               char c = s.charAt(sindex);
               while (tindex < t.length()) {
                   if (t.charAt(tindex) == c) {
                       tindex++;
                       count++;
                       break;
                   } else tindex++;
               }
               sindex++;
   
           }
           if (count == s.length()) return true;
           else return false;
   ```

   

4. **115 不同的子序列**

   求解s中包含了几个t

   **这道题比较难**

   索引问题，i-1,j-1

   `dp[i][j]`：以i-1为结尾的s子序列中出现以j-1为结尾的t的个数为 `dp[i][j]`

   这一类问题，基本是要分析两种情况

   - s[i - 1] 与 t[j - 1]相等
   - s[i - 1] 与 t[j - 1] 不相等

   当s[i - 1] 与 t[j - 1]相等时，dp[i][j]可以有两部分组成。

   一部分是用s[i - 1]来匹配，那么个数为 `dp[i-1][j-1]`。即不需要考虑当前s子串和t子串的最后一位字母，所以只需要  `dp[i-1][j-1]`。

   一部分是不用s[i - 1]来匹配，个数为 `dp[i-1][j]`。

   <img src="https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250311173450367.png" alt="image-20250311173450367" style="zoom:80%;" />

   ```
   class Solution {
       public int numDistinct(String s, String t) {
   
           //这道题挺难的，需要好好理解
           int[][] dp = new int[s.length() + 1][t.length() + 1];
           //dp[i][j]的含义是si中包含了多少个tj
           //初始化
           //初始化列，这个意思代表t是空字符,s中包含了1个空字符
           for (int i = 0; i <= s.length(); i++) {
               dp[i][0] = 1;
           }
   
           //剩下的不用初始化了
           for (int i = 1; i <= s.length(); i++) {
               for (int j = 1; j <= t.length(); j++) {
                   if (s.charAt(i - 1) == t.charAt(j - 1)) {
                       dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];//这跟以往不一样，这个不是判断长度
                       //这个是判断s中包含几个t
                   } else {
                       dp[i][j] = dp[i - 1][j];
                   }
   
               }
           }
           //这道题就不是找最大值，而是输出最后一个
           //可以拿"eee"和"eee"来举例
           return dp[s.length()][t.length()];
       }
   }
   ```

   

## day43  2025/3/12

### DP    编辑距离   回文子串

1. **583 两个字符串的删除操作**

   本质是就是找两个字符串的最长公共子序列，然后分别计算每个字符串要想变为这个子序列需要删除几个字符。

   ，只要求出两个字符串的最长公共子序列长度即可，那么除了最长公共子序列之外的字符都是必须删除的，最后用两个字符串的总长度减去两个最长公共子序列的长度就是删除的最少步数。

   ```
   class Solution {
       public int minDistance(String word1, String word2) {
           //找到最长公共子序列
   
           int[][] dp = new int[word1.length() + 1][word2.length() + 1];
   
           //进行初始化
           //第一行初始化为0
           //第一列初始化为0
           for (int i = 0; i <= word2.length(); i++) {
               dp[0][i] = 0;
           }
           for (int i = 0; i <= word1.length(); i++) {
               dp[i][0] = 0;
           }
   
           int maxLength = 0;
           for (int i = 1; i <= word1.length(); i++) {
   
               for (int j = 1; j <= word2.length(); j++) {
                   if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                       dp[i][j] = dp[i - 1][j - 1] + 1;
                   } else {
                       dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                   }
                   maxLength = Math.max(dp[i][j], maxLength);
               }
           }
           int len1 = word1.length() - maxLength;
           int len2 = word2.length() - maxLength;
           return len1 + len2;
       }
   }
   
   ```

   

2.  ==**72 编辑距离**    一道DP的经典题目==

   **！！！这道题涉及到增删改，仔细看代码，而且要好好想想dp数组的含义，如果当前字符不相等，比如word1删除一个字符，那就是变为word[i-1]，那么就是判断word[i-1]与word[j]的最小编辑距离，那么现在推理公式不就是 `dp[i-1][j]+1`, 这是个推理的公式，所有的值都有初始值推理而来了，这样就找到了一个，那么如果word2删除一个元素呢, word2[j-1]和word[i]来找最小编辑距离，所以这时候推理公式就是 `dp[i][j]=dp[i][j-1]+1`，另外还需要想明白就是，一个字符串的删除可以看成另一个字符串的增加，最终操作都是一样的！！！**

   注意的地方：

   1. 递推的公式
   2. 数组初始化

   ```
   class Solution {
       public int minDistance(String word1, String word2) {
           //编辑距离
           //一个单词可以进行的操作：增、删、改
           //注意点：增的操作可以映射成删的操作，一个单词的删除操作等于另一个单词的增加操作
           int[][] dp = new int[word1.length() + 1][word2.length() + 1];
           //注意初始化
           //第一列 dp[i][0]=i;因为需要i次操作才可以变为空字符串或者从空字符串变为当前字符串
           //第一行 dp[0][i]=i;
           for (int i = 0; i <= word1.length(); i++) {
               dp[i][0] = i;
           }
           for (int i = 0; i <= word2.length(); i++) {
               dp[0][i] = i;
           }
   
           for (int i = 1; i <= word1.length(); i++) {
               for (int j = 1; j <= word2.length(); j++) {
                   //如果字符相等，那么编辑距离直接等于斜上方的编辑距离
                   if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                       dp[i][j] = dp[i - 1][j - 1];
                   } else {
                       //如果不相等，增删改
                       //1. word1删除一个字符（其实也等于word2增加一个字符，最终的操作是一样），dp[i-1][j]+1,删也是一次操作
                       //2. word2删除一个字符（其实也等于word1增加一个字符，最终的操作是一样的）,dp[i][j-1]+1，删也是一次操作
                       //3. 替换，dp[i-1][j-1]+1，就是斜上方的最小编辑距离+1，因为当前替换操作一次
                       dp[i][j] = Math.min(dp[i - 1][j] + 1, Math.min(dp[i][j - 1] + 1, dp[i - 1][j - 1] + 1));
                   }
   
               }
           }
           return dp[word1.length()][word2.length()];
   
       }
   }
   ```

   

3.  **647 回文子串**   -- 值得好好想一想

   二维dp数组，可以利用回文串的性质

   <img src="https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250312163142824.png" alt="image-20250312163142824" style="zoom:80%;" />

   ```
           //用动态规划的算法来做
           //二维dp数组
           boolean[][] dp = new boolean[s.length() ][s.length() ];
           //dp初始化就是false
           //如果s[i]和s[j]相等，判断i到j是不是回文串，直接判断i+1到j-1是不是回文串
           //如果不相等，肯定就不是
           //注意遍历顺序，遍历顺序是从下到上，从左到右
           int result=0;
           for (int i = s.length()-1; i >= 0; i--) {
               for (int j = i; j < s.length(); j++) {
                   if(s.charAt(i)==s.charAt(j)){
                       //如果相等，有两种情况
                       if(j-i<=1) {
                           //相邻或者自身
                           result++;
                           dp[i][j]=true;
                       }else {
                           //中间间隔大于1个，那么就判断i+1到j-1
                           if(dp[i+1][j-1]) {
                               result++;
                               dp[i][j]=true;
                           }
                       }
                   }
                   //不相等就不需要操作，直接默认false就行
   
               }
   
           }
           return result;
   ```

   也可以利用双指针，我自己的写的解法，耗时太高

   ```
           if (s.length() == 1) return 1;
           int[] dp = new int[s.length()];
           Arrays.fill(dp, 1);
           //dp[i]代表i的回文串的数量，其实本质是双指针的做法
           for (int i = 1; i < s.length(); i++) {
               //判断从头到i是不是回文串
               for (int j = 0; j < i; j++) {
                   boolean result = isSubstring(j, i, s);
                   if (result) {
                       //说明是回文子串
                       dp[i] += 1;
                   }
               }
           }
           int sum = Arrays.stream(dp).sum();
           return sum;
   ```

   

4. **516 最长回文子序列  -- 子序列是不连续的**

   我自己的写的题解

   可以好好看看

   ```
   class Solution {
       public int longestPalindromeSubseq(String s) {
   
           //二维数组需要考虑多种情况，从下往上，从左到右
           //1. s[i]==s[j] 如果i==j自身，肯定是1
           //如果j-i==1 相邻，肯定是2
           //如果j-i>1 不相邻，dp[i][j]=d[i+1][j-1]+2;
           //2。s[i]!=s[j]
           //如果是j-i==1 说明是相邻，肯定是1
           //如果j-i>1 dp[i][j]=dp[i][j-1] dp[i][j]=dp[i+1][j-1] dp[i+1][j]
           int[][] dp = new int[s.length()][s.length()];
           int maxResult=0;
           for (int i = s.length() - 1; i >= 0; i--) {
   
               for (int j = i; j < s.length(); j++) {
                   if (s.charAt(i) == s.charAt(j)) {
                       if (i == j) dp[i][j] = 1;
                       else if (j - i == 1) dp[i][j] = 2;
                       else dp[i][j] = dp[i + 1][j - 1] + 2;
                   } else {
                       if (j - i == 1) dp[i][j] = 1;
                       else {
                           dp[i][j] = Math.max(dp[i + 1][j - 1], Math.max(dp[i][j - 1], dp[i + 1][j]));
                       }
                   }
                   maxResult=Math.max(maxResult,dp[i][j]);
   
               }
   
           }
           return maxResult;
   
   
       }
   }
   ```

   



## day44 2025/3/18

### LRU  -- 高频算法题-- `LinkedHashMap` 的 **有序性** 和 **自动移除最久未使用元素的特性**

1. **146 LRU缓存**

   **每每对元素进行一次操作就把他放到双向链表的头部，我采用的方法是HashMap和LinkedList**

   **get操作需要，put操作也需要，同时需要注意在put操作中即使有这个key的值了，需要更新value的时候，也是一次使用，也需要添加到双向链表的头部**

   而在面试中，面试官一般会期望读者能够自己实现一个简单的双向链表，而不是使用语言自带的、封装好的数据结构。

   我自己写的，耗时太长1032ms

   ```
   class LRUCache {
   
       private int capacity;
       private Map<Integer, Integer> result = new HashMap<>();
   
       private LinkedList<Integer> num = new LinkedList<>();
   
       public LRUCache(int capacity) {
           this.capacity = capacity;
           this.result=new HashMap<>();
           this.num=new LinkedList<>();
       }
   
       public int get(int key) {
           if (result.containsKey(key)) {
               //将节点移动到头部，表示最近访问
               removeToHead(key);
               return result.get(key);
           } else return -1;
   
       }
   
       public void removeToHead(int key) {
           //自动装箱将int变为integer
           Integer keynum = key;
           // 先删掉这个值
           num.remove(keynum);
           // 先添加到头部
           num.addFirst(key);
       }
       public void put(int key, int value) {
           //自动装箱
           Integer keynum = key;
           Integer valuenum = value;
   
           if (result.containsKey(key)) {
               result.put(key,value);
               //把这个移动到链表头部去
               removeToHead(key);
   
           } else {
               if (result.size() < capacity) {
                   //如果小于最大容量，可以一直添加
                   result.put(keynum, valuenum);
                   num.addFirst(key);
   
               } else {
                   //如果等于最大容量了，需要移除
                   Integer lastnumber = num.getLast();
                   final Integer removevalue = result.remove(lastnumber);
                   num.removeLast();
                   if (removevalue != null) {
                       result.put(key, value);
                       num.addFirst(key);
                   }
               }
           }
       }
   }
   
   ```

   官方给出的题解，采用**LinkedHashMap**封装好的数据结构，LinkedHashMap结合了哈希表和双向链表，`LinkedHashMap` 的 **有序性** 和 **自动移除最久未使用元素的特性**

   ```
   class LRUCache extends LinkedHashMap<Integer, Integer>{
       private int capacity;
       
       public LRUCache(int capacity) {
           super(capacity, 0.75F, true); // true 表示 按照访问顺序 (Access Order) 维护键值对。
                                         // false（默认值）表示 按照插入顺序 (Insertion Order) 维护键值对。
           this.capacity = capacity;
       }
   
       public int get(int key) {
           return super.getOrDefault(key, -1);
       }
   
       public void put(int key, int value) {
           super.put(key, value);
       }
   
       @Override // 在每次 put() 操作后，都会调用 removeEldestEntry() 来检查是否需要删除 最旧的元素（即 访问最少的元素），这里面判断如果超过了最大容量就返回true，意味着删除，否则就是false
       protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
           return size() > capacity; 
       }
   }
   
   ```

   

## day45 2025/3/19

### 单调栈 双指针 -- 接雨水 --高频算法题

1. **42 接雨水** 

   思路：

   1. 以列为单位，遍历每一列

   2. 找到当前列左边列的最大值

   3. 找到当前列右边列的最大值

   4. 取其两者最小值，然后与自身长度相减

   5. 如果结果大于0，那么相加

      **解法：**

      1. **暴力求解，实际也是用双指针，但是这种已经超时了**

      2. **双指针解法**

      3. **单调栈**

         可以用两个数组来记录左边最大值和右边最大值

         
              int[] maxleft = new int[height.length];
              int[] maxright = new int[height.length];
         

      ```
      class Solution {
          public int trap(int[] height) {
              
              if (height.length == 1) return 0;
      
              // 可以用两个数组记录每一个高度左边的最大值和右边的最大值
              int[] maxleft = new int[height.length];
              int[] maxright = new int[height.length];
              int sum = 0;
      
              maxleft[0] = height[0];
              for (int i = 1; i < height.length; i++) {
                  maxleft[i] = Math.max(maxleft[i - 1], height[i]);
              }
              maxright[height.length - 1] = height[height.length - 1];
              for (int i = height.length - 2; i >= 0; i--) {
                  maxright[i] = Math.max(height[i], maxright[i + 1]);
              }
              for (int i = 0; i < height.length; i++) {
                  int h = Math.min(maxleft[i], maxright[i]) - height[i];
                  if (h > 0) sum += h;
              }
              return sum;
          }
      
      }
      
      ```



## day46 2025/3/20

### 多线程    -- 单调栈 - 每日温度

假设有4个线程，打出一长串字符串ABCDABCD.......，每个线程只能打出一个字符，确保按照顺序输出，怎么实现。

`ReentrantLock` 是 Java `java.util.concurrent.locks` 包中的**可重入锁**；

`Condition` 是 `ReentrantLock` 提供的**等待/通知**机制，用于线程间通信：

​	`	await()`：线程进入等待状态（类似 `wait()`）。

​	`signal()`：唤醒等待的线程（类似 `notify()`）。

​	`signalAll()`：唤醒所有等待线程（类似 `notifyAll()`）

```
package testleetcode;


import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

// 3.20字节后端一面代码题
public class CodeFirst {
    private final ReentrantLock reentrantLock = new ReentrantLock();
    private final Condition[] conditions = new Condition[4];
    private volatile int state = 0;

    public CodeFirst() {
        for (int i = 0; i < 4; i++) {
            conditions[i] = reentrantLock.newCondition();
        }
    }

    public void printChar(int thread, char ch) {
        for (int i = 0; i < 10; i++) {
            reentrantLock.lock();
            try {
                while (state % 4 != thread) {
                    conditions[thread].await();
                }
                System.out.println(ch);
                state++;
                conditions[(thread + 1) % 4].signal();
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                reentrantLock.unlock();
            }
        }
    }
    public static void main(String[] args) {
        CodeFirst codeFirst = new CodeFirst();
        new Thread(() -> codeFirst.printChar(0, 'A')).start();
        new Thread(() -> codeFirst.printChar(1, 'B')).start();
        new Thread(() -> codeFirst.printChar(2, 'C')).start();
        new Thread(() -> codeFirst.printChar(3, 'D')).start();
    }
}

```



2. **739 每日温度   单调栈**

   单调栈使用的情况：**通常是一维数组，要寻找任一个元素的右边或者左边第一个比自己大或者小的元素的位置，此时我们就要想到可以用单调栈了**

   在使用单调栈的时候首先要明确如下几点：

   1. 单调栈里存放的元素是什么？

   单调栈里只需要存放元素的下标i就可以了，如果需要使用对应的元素，直接T[i]就可以获取。

   1. 单调栈里元素是递增呢？ 还是递减呢？

      如果求一个元素右边第一个更大元素，单调栈从栈底到栈顶就是递减的，如果求一个元素右边第一个更小元素，单调栈就是递增的。

   ```
   
   import java.util.Stack;
   
   //leetcode submit region begin(Prohibit modification and deletion)
   class Solution {
       public int[] dailyTemperatures(int[] temperatures) {
           //要找到右边第一个大于的
           //单调栈，保证从栈底到栈顶是递减的
           Stack<Integer> stack = new Stack();
           final int length = temperatures.length;
           int[] result = new int[length];
           stack.push(0);//栈中存放的是元素的下标
   
           for (int i = 1; i < length; i++) {
               if (temperatures[i] <= temperatures[stack.peek()]) //如果当前元素小于等于栈顶的元素，那么直接放进去
                   stack.push(i);
               else {//如果是大于的话，就要一直出栈
   
                   while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
   
                       result[stack.peek()] = i - stack.peek();
                       stack.pop();
                   }
                   stack.push(i);
               }
           }
           return result;
       }
   }
   
   
   ```

   ==**单调栈的解法：**==

   栈中存放的还是下标，先放下标0的元素

   1. 如果当前元素小于栈顶下标对应的元素，可以直接入栈
   2. 如果当前的元素等于栈顶下标对应的元素，把栈顶元素弹出，入栈
   3. 如果当前元素大于栈顶下标对应的元素，循环弹出栈顶元素，直到小于栈顶对应的元素，再入栈

   ![image-20250321153937328](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250321153937328.png)

   ```
           Stack<Integer> stack = new Stack<>();//存放下标
           final int length = height.length;
           if (length <= 2) return 0;
           stack.push(0);
           int sum = 0;
           for (int i = 1; i < length; i++) {
               if (height[i] < height[stack.peek()]) {
                   //入栈
                   stack.push(i);
               } else if (height[i] == height[stack.peek()]) {
                   stack.pop();
                   stack.push(i);
               } else {
                   //大于开始弹
                   while (!stack.isEmpty() && height[i] > height[stack.peek()]) {
                       int mid = stack.peek();
                       stack.pop();
                       if (!stack.isEmpty()) {
                           int h = Math.min(height[stack.peek()], height[i]) - height[mid];
                           int w = i - stack.peek() - 1;
                           if (h * w > 0) sum += h * w;
                       }
   
                   }
                   stack.push(i);
               }
           }
           return sum;
   
       }
   
   }
   ```



## day47 2025/3/21

### 单调栈 --柱状图中最大的矩形

1. **84  柱状图中最大的矩形   -- 没有完全理解**

   ```
   class Solution {
       public int largestRectangleArea(int[] heights) {
   
           Stack<Integer> st = new Stack<Integer>();
   
           // 数组扩容，在头和尾各加入一个元素
           int [] newHeights = new int[heights.length + 2];
           newHeights[0] = 0;
           newHeights[newHeights.length - 1] = 0;
           for (int index = 0; index < heights.length; index++){
               newHeights[index + 1] = heights[index];
           }
   
           heights = newHeights;
   
           st.push(0);
           int result = 0;
           // 第一个元素已经入栈，从下标1开始
           for (int i = 1; i < heights.length; i++) {
               // 注意heights[i] 是和heights[st.top()] 比较 ，st.top()是下标
               if (heights[i] > heights[st.peek()]) {
                   st.push(i);
               } else if (heights[i] == heights[st.peek()]) {
                   st.pop(); // 这个可以加，可以不加，效果一样，思路不同
                   st.push(i);
               } else {
                   while (heights[i] < heights[st.peek()]) { // 注意是while
                       int mid = st.peek();
                       st.pop();
                       int left = st.peek();
                       int right = i;
                       int w = right - left - 1;
                       int h = heights[mid];
                       result = Math.max(result, w * h);
                   }
                   st.push(i);
               }
           }
           return result;
   
   
       }
   }
   
   ```

   

## day48 2025/3/22

### 最长连续序列

1. **128 最长连续序列**

   使用数组排序，这道题也可以用哈希表来做

   ```
   class Solution {
       public int longestConsecutive(int[] nums) {
           
           //sort
           if(nums.length==1) return 1;
           if(nums.length==0) return 0;
           Arrays.sort(nums);
           int count=1;
           int max=0;
           for(int i=1;i<nums.length;i++){
               
               if(nums[i]-nums[i-1]==0){
                   continue;
               }else if(nums[i]-nums[i-1]==1) count++;
               else{
                   max=Math.max(max,count);
                   count=1;
               }    
           }
           return Math.max(max,count);
       }
   }
   ```

   





## day49 2025/3/23

## 子串、前缀和、旋转图像

1. **560 和为k的子数组**

   ==注意：这道题中数组取值允许正数，负数，0的出现==

   **前缀和：**对于数组中的任何位置 j，前缀和 pre[j] 是数组中从第一个元素到第 j 个元素的总和。这意味着如果你想知道从元素 i+1 到 j 的子数组的和，你可以用 pre[j] - pre[i] 来计算。

   **使用 Map 来存储前缀和：**
   在代码中，我们用一个 Map（哈希表）来**存储每个前缀和出现的次数**。这是为了快速检查某个特定的前缀和是否已经存在，以及它出现了多少次。

   

   ```
   class Solution {
       public int subarraySum(int[] nums, int k) {
           //前缀和
           Map<Integer, Integer> map = new HashMap<>();
           map.put(0, 1);
           int pre = 0;//前缀和
           int count = 0;
           for (int i = 0; i < nums.length; i++) {
               pre += nums[i];
               if (map.containsKey(pre - k)) {
                   count += map.get(pre - k);
               }
               map.put(pre, map.getOrDefault(pre, 0) + 1);
           }
           return count;
   
       }
   }
   ```



## day50 2025/3/24



2. **48 旋转图像**

   ==把二维矩阵顺时针旋转90°= **先水平翻转+主对角线翻转**==

   ```
   class Solution {
       public void rotate(int[][] matrix) {
           //用翻转代替顺时针90°旋转
   
           //水平翻转+对角线翻转=顺时针90°翻转
           //先进行水平翻转
           int row = matrix.length;
           int col = matrix[0].length;
           for (int i = 0; i <row/2; i++) {
               for (int j = 0; j < col; j++) {
                   //水平翻转
                   int temp=matrix[i][j];
                   matrix[i][j]=matrix[row-1-i][j];
                   matrix[row-1-i][j]=temp;
               }
           }
           //主对角线翻转
           for (int i = 0; i < row; i++) {
               for (int j = i; j < col; j++) {
                   int temp=matrix[i][j];
                   matrix[i][j]=matrix[j][i];
                   matrix[j][i]=temp;
               }
           }
   
       }
   }
   ```

   

3. **240 搜索二维矩阵**

   快速在一个m*n的矩阵中搜索到一个元素，这个矩阵每行元素递增，每列元素也是递增

   这道题有超时限制，直接遍历搜索肯定超时，每行二分查找也超时，

   ==所以从矩阵右上角元素开始查找，每次重新的矩阵是*matrix* 的左下角为左下角、以 (*x*,*y*) 为右上角的矩阵中进行搜索==

   ```
   class Solution {
       public boolean searchMatrix(int[][] matrix, int target) {
           int row = matrix.length;
           int col = matrix[0].length;
   
           //直接遍历比较，肯定不是这道题的初衷
           //按照对角线搜索,其实不对，放弃
           //每行进行二分查找,超时，放弃
         //从矩阵右上角搜索,Z字形查找
           int x = 0;
           int y = col - 1;
           while (x < row && y >= 0) {
               if (matrix[x][y] == target) return true;
               if (matrix[x][y] > target) {
                   y--;
               } else {
                   x++;
               }
           }
           return false;
       }
   }
   ```

   

## day 51 2025/3/25



## day 52 2025/3/26

### 148 排序链表 归并排序

1. **148 排序链表**

   思路：用的是归并排序，如果自己单独设置一个头结点一个链表利用插入排序的话最后会超时

   **从上到下的归并排序： 只是这种空间复杂度是On，不是常数级**

```
 public ListNode sortList(ListNode head) {
        return sortList(head, null);
    }

    public ListNode sortList(ListNode head, ListNode tail) {
        if (head == null) {
            return head;
        }
        if (head.next == tail) {
            head.next = null;
            return head;
        }
        ListNode slow = head, fast = head;
        while (fast != tail) {
            slow = slow.next;
            fast = fast.next;
            if (fast != tail) {
                fast = fast.next;
            }
        }
        ListNode mid = slow;
        ListNode list1 = sortList(head, mid);
        ListNode list2 = sortList(mid, tail);
        ListNode sorted = merge(list1, list2);
        return sorted;
    }

    public ListNode merge(ListNode head1, ListNode head2) {
        ListNode dummyHead = new ListNode(0);
        ListNode temp = dummyHead, temp1 = head1, temp2 = head2;
        while (temp1 != null && temp2 != null) {
            if (temp1.val <= temp2.val) {
                temp.next = temp1;
                temp1 = temp1.next;
            } else {
                temp.next = temp2;
                temp2 = temp2.next;
            }
            temp = temp.next;
        }
        if (temp1 != null) {
            temp.next = temp1;
        } else if (temp2 != null) {
            temp.next = temp2;
        }
        return dummyHead.next;
    }


```



## day 53 2025/4/3

### 437 路径总和iii - 前缀和

这道题用的是前缀和prefix

```
class Solution {
    public int pathSum(TreeNode root, int targetSum) {
        if (root == null) return 0;
        //考察节点的前缀和
        //
        Map<Long, Integer> prefix = new HashMap<>();
        prefix.put(0L, 1);
        return dfs(root, prefix, 0, targetSum);
    }

    public int dfs(TreeNode root, Map<Long, Integer> prefix, long curr, int targetSum) {
        //前序遍历
        //前缀和
        if (root == null) return 0;
        int ret = 0;
        curr += root.val;
        ret = prefix.getOrDefault(curr - targetSum, 0);
        prefix.put(curr, prefix.getOrDefault(curr, 0) + 1);
        ret += dfs(root.left, prefix, curr, targetSum);
        ret += dfs(root.right, prefix, curr, targetSum);
        prefix.put(curr, prefix.getOrDefault(curr, 0) - 1);
        return ret;
    }

}

```

 

### 200 岛屿数量 -- 图论

可以利用深度优先搜索，不断搜索当前前后左右的1，最后深度优先搜索的次数就是岛屿的数量

```
class Solution {
    public int numIslands(char[][] grid) {

        //图论
        //先进行异常判断
        if (grid == null || grid.length == 0) return 0;
        int row = grid.length;
        int col = grid[0].length;
        int numlands = 0;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (grid[i][j] == '1') {
                    numlands++;
                    dfs(grid, i, j);
                }
            }
        }
        //岛屿的数量就是最后深度搜索的次数
        return numlands;

    }

    private void dfs(char[][] grid, int row, int col) {
        int gridrow = grid.length;
        int gridcol = grid[0].length;
        if (row < 0 || row >= gridrow || col < 0 || col >= gridcol || grid[row][col] == '0')
            return;

        grid[row][col] = '0';
        dfs(grid, row - 1, col);
        dfs(grid, row + 1, col);
        dfs(grid, row, col - 1);
        dfs(grid, row, col + 1);

    }

}
```

### 207 课程表 -- 图论 -- 拓扑排序 - 有向无环图(DAG)

听说是拼多多一面、饿了么一面

要清楚拓扑排序的概念

![image-20250403160234254](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250403160234254.png)

这道题每个顶点设置三种状态0 1 2 分别代表未被访问、正在访问、已完成访问

```
class Solution {
    List<List<Integer>> edges;
    int[] visited;
    boolean valid=true;
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        //拓扑排序
        //有向无环图

        edges=new ArrayList<>();
        for (int i = 0; i < numCourses; i++) {
            edges.add(new ArrayList<Integer>());
        }
        visited=new int[numCourses];
        for (int[] prerequisite : prerequisites) {
            edges.get(prerequisite[1]).add(prerequisite[0]);

        }
        for (int i = 0; i < numCourses&&valid; i++) {
            if(visited[i]==0){
                dfs(i);
            }
        }
        return valid;

    }
    private  void dfs(int point){
        visited[point]=1;//1代表正在访问中
        for (int v : edges.get(point)) {
            if(visited[v]==0){//0代表还未访问
                dfs(v);
                if(!valid) return;
            }else if(visited[v]==1){
                //说明该节点正在被访问，形成了环
                valid=false;
                return;
            }
        }
        visited[point]=2;//2代表该顶点访问已经完成
    }

}
```



## day54 2025/4/7

### 215 数组中第K个最大元素-- 小顶堆

用的是小顶堆，优先队列来实现堆

```
class Solution {
    public int findKthLargest(int[] nums, int k) {


        Map<Integer, Integer> map = new HashMap<>();

        //就让用堆实现
        //最小堆
        for (int i = 0; i < nums.length; i++) {
            //key：index
            //value：相应的值
            map.put(i, nums[i]);

        }
        PriorityQueue<int[]> pq = new PriorityQueue<>((pair1, pair2) ->
            pair1[1] - pair2[1] == 0 ? pair1[0] - pair2[0] : pair1[1] - pair2[1]
        );
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (pq.size() < k) {
                pq.add(new int[]{entry.getKey(), entry.getValue()});
            } else {
                if (entry.getValue() > pq.peek()[1]) {
                    pq.poll();
                    pq.add(new int[]{entry.getKey(), entry.getValue()});
                }
            }
        }

        
        return pq.peek()[1];


    }
}
```



### 153 寻找旋转排序数组的最小值

这道题采用的是二分法查找数组的最小值，**二分的思想：每次淘汰一半**

基于这个思想，我们要去想淘汰策略。我们发现本题中，有：
最小元素 m 的左边所有元素都比数组的最后一个元素 x大，右边所有元素（不含x）都比 x 小
于是我们的淘汰策略为：对于每一对low high，比较中间元素值和x的大小：
1.nums[mid]<x：说明 mid 在 m 的右边，即目标 m 在 mid 的左边，故可淘汰右半边；
2.nums[mid]>x：同理淘汰左半边；
3.nums[mid]==x: 不可能，因为数组无重复值，如果成立，则必然有mid==n-1，则必然有low==high==n-1。但当low==high时，我们已经找到m

![image-20250407200525891](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250407200525891.png)

只是这道题我觉得需要注意的是，它每次是拿pivot对应的元素与high对应的元素来比较，然后来移动指针，那么可以拿pivot对应的元素与low对应的元素比较吗？我觉得不行，那样不能保证指针移动的方向是对的，或许也可以，但需要修改代码

```
class Solution {
    public int findMin(int[] nums) {

        //利用二分查找找到原本有序数组的最小值
        int low = 0;
        int high = nums.length - 1;
        int pivot = 0;

        while (low <= high) {
            pivot = (high - low) / 2 + low;
            if (nums[pivot] > nums[high]) {
                low = pivot + 1;
            } else if (nums[pivot] < nums[high]) {
                high = pivot;
            } else return nums[pivot];
        }
        return nums[pivot];

    }
}
```

## day 55 2025 4/11

### 394 字符串编码 - 栈



## day56 2025-8/26

### 221 最大正方形 - 动态规划

在一个由 `'0'` 和 `'1'` 组成的二维矩阵内，找到只包含 `'1'` 的最大正方形，并返回其面积。

可以使用动态规划降低时间复杂度。我们**用 dp(i,j) 表示以 (i,j) 为右下角，且只包含 1 的正方形的边长最大值**。如果我们能计算出所有 dp(i,j) 的值，那么其中的最大值即为矩阵中只包含 1 的正方形的边长最大值，其平方即为最大正方形的面积。

```
class Solution {
    public int maximalSquare(char[][] matrix) {
        int maxSide = 0;
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return maxSide;
        }
        int rows = matrix.length, columns = matrix[0].length;
        int[][] dp = new int[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                if (matrix[i][j] == '1') {
                    if (i == 0 || j == 0) {
                        dp[i][j] = 1;
                    } else {
                        dp[i][j] = Math.min(Math.min(dp[i - 1][j], dp[i][j - 1]), dp[i - 1][j - 1]) + 1;
                    }
                    maxSide = Math.max(maxSide, dp[i][j]);
                }
            }
        }
        int maxSquare = maxSide * maxSide;
        return maxSquare;
    }
}
```

### 301 删除无效的括号  - BFS

给你一个由若干括号和字母组成的字符串 `s` ，删除最小数量的无效括号，使得输入的字符串有效。

返回所有可能的结果。答案可以按 **任意顺序** 返回。

```
class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> ans = new ArrayList<>();
        Set<String> currSet = new HashSet<>();
        currSet.add(s);

        while (true) {
            for (String str : currSet) {
                if (isValid(str)) {
                    ans.add(str);
                }
            }
            if (ans.size() > 0) {
                return ans;
            }
            Set<String> nextSet = new HashSet<String>();
            for (String str : currSet) {
                for (int i = 0; i < str.length(); i++) {
                    if (i > 0 && str.charAt(i) == str.charAt(i - 1)) {
                        continue;
                    }
                    if (str.charAt(i) == '(' || str.charAt(i) == ')') {
                        nextSet.add(str.substring(0, i) + str.substring(i + 1));
                    }
                }
            }
            currSet = nextSet;
        }

    }

    public boolean isValid(String str) {
        char[] ss = str.toCharArray();
        int count = 0;
        for (char s : ss) {
            if (s == '(') {
                count++;
            } else if (s == ')') {
                count--;
                if (count < 0) {
                    return false;
                }
            }
        }
        return count == 0;

    }
}
```

## day57- 2025-8/27

### 399 除法求值



## day58 - 2025 - 9/1

### 4  寻找两个正序数组的中位数

我的思路就是用**==优先级队列（最小堆），堆顶是最小元素==**，最小堆只能保证部分有序，把两个数组都塞到堆里面，然后一点点弹出堆顶的元素，就组成了一个正序的队列，再求中位数就行。

```
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {

        //设计一个存储结果的数组
        int m = nums1.length;
        int n = nums2.length;
        int[] result = new int[m + n];
        // 定义一个优先级队列
        int count = 0;
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int i = 0; i < m; i++) {
            pq.offer(nums1[i]);
            count++;
        }
        for (int i = 0; i < n; i++) {
            pq.offer(nums2[i]);
            count++;
        }
        //把堆顶一点点弹出来
        int j = 0;
        while (count > 0 && !pq.isEmpty()) {
            result[j] = pq.poll();
            count--;
            j++;
        }
        double midNum = 0;
        int index = result.length / 2;
        if (result.length % 2 == 0) {
            midNum =(double) (result[index-1] + result[index]) / 2;
        } else {
            midNum =(double)result[index];
        }
        return midNum;
    }
}
```



## day 59 2025 9-2

### 581 最短无序连续子数组

思路，可以拷贝一个新的数组，然后从左向右比较，第一个不同的元素就是左边界；从右向左遍历，第一个不同的元素就是右边界；但这并不是最优解法。最优解法是一次遍历

或者本质原理：从左往右，找到比左边最大值还小的最右下标，从右往左，找到比右边最小值还大的最左下标

```
// 拷贝数组
 System.arraycopy(nums, 0, numsCopy, 0, nums.length);// 原数组，拷贝的起点，新数组，拷贝的起点，拷贝多少
```



```
class Solution {
    public int findUnsortedSubarray(int[] nums) {

        int[] numsCopy = new int[nums.length];

        System.arraycopy(nums, 0, numsCopy, 0, nums.length);

        Arrays.sort(numsCopy);// 对拷贝的数组进行排序
        // 从前往后遍历，找到第一个不同的
        int left = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != numsCopy[i]) {
                left = i;
                break;
            }
        }
        int right = 0;
        for (int i = nums.length - 1; i >= 0; i--) {
            if (nums[i] != numsCopy[i]) {
                right = i;
                break;
            }
        }
        if (right == left) return 0;
        return right - left + 1;
    }
}
```

一次遍历

```
class Solution {
    public int findUnsortedSubarray(int[] nums) {
        int n = nums.length;
        int maxn = Integer.MIN_VALUE, right = -1;
        int minn = Integer.MAX_VALUE, left = -1;
        for (int i = 0; i < n; i++) {
            if (maxn > nums[i]) {
                right = i;
            } else {
                maxn = nums[i];
            }
            if (minn < nums[n - i - 1]) {
                left = n - i - 1;
            } else {
                minn = nums[n - i - 1];
            }
        }
        return right == -1 ? 0 : right - left + 1;
    }
}
```

## day 60 2025 9-3

### 42 接雨水

单调栈的做法

```
class Solution {
    public int trap(int[] height) {
    
    // 第二次做
        Stack<Integer> stack = new Stack<>(); // 用来存放下标的
        int lenght = height.length;
        if (lenght <= 2) return 0;

        stack.push(0);
        int sum = 0;
        for (int i = 1; i < lenght; i++) {
            if (height[i] < height[stack.peek()]) {
                stack.push(i);
            } else if (height[i] == height[stack.peek()]) {
                stack.pop();
                stack.push(i);
            } else {
                // 开始弹
                while (!stack.isEmpty() && height[i] > height[stack.peek()]) {
                    int temp = stack.peek();
                    stack.pop();
                    if (!stack.isEmpty()) {
                        int h = Math.min(height[i], height[stack.peek()]) - height[temp];
                        int w = i - stack.peek() - 1;
                        if (h * w > 0) sum += h * w;
                    }
                }
                stack.push(i);
            }

        }
        return sum;
    }
}
    
```

### 3 无重复字符的最长子串

用滑动窗口

```
class Solution {
    public int lengthOfLongestSubstring(String s) {
          public int lengthOfLongestSubstring(String s) {
        // set去重
        // 滑动窗口
        Set<Character> result = new HashSet<>();//去重
        char[] charArray = s.toCharArray();
        int maxLen = 0;

        int left = 0;
        int right = 0;
        while (right < s.length()) {
            if (result.contains(charArray[right])) {
                result.remove(charArray[left]);
                left++;
            } else {
                result.add(charArray[right]);
                right++;
            }
            maxLen = Math.max(maxLen, right - left);
        }
        return maxLen;

    }
}
```

## day61 2025-9-4

### 5 最长回文子串

**动态规划。**我们用 *P*(*i*,*j*) 表示字符串 *s* 的第 *i* 到 *j* 个字母组成的串（下文表示成 *s*[*i*:*j*]）是否为回文串：只有 *s*[*i*+1:*j*−1] 是回文串，并且 *s* 的第 *i* 和 *j* 个字母相同时，*s*[*i*:*j*] 才会是回文串。

```
class Solution {
    public String longestPalindrome(String s) {

        final int length = s.length();
        if (length < 2) return s;
        int maxLen = 1;
        int begin = 0;
        boolean[][] dp = new boolean[length][length];
        //初始化，所有长度为1的子串都是回文串
        for (int i = 0; i < length; i++) {
            dp[i][i] = true;
        }
        final char[] chars = s.toCharArray();
        // 递推开始
        for (int L = 2; L <= length; L++) {

            for (int i = 0; i < length; i++) {
                int j = L + i - 1;
                //如果右边界越界，就可以退出当前循环
                if (j >= length) break;
                if (chars[i] != chars[j]) {
                    dp[i][j] = false;
                } else {
                    if (j - i < 3) {
                        dp[i][j] = true;
                    } else {
                        dp[i][j] = dp[i + 1][j - 1];
                    }
                }
                if (dp[i][j] && j - i + 1 > maxLen) {
                    maxLen = j - i + 1;
                    begin = i;
                }
            }


        }
        return s.substring(begin, begin + maxLen);

    }
}
```

## day62 2025-9-8

### 21 合并两个有序链表

采用递归的方式合并两个有序链表

![](https://store-image-mj.oss-cn-beijing.aliyuncs.com/img/image-20250908212845115.png)

```
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {

        // 用递归的解法
        if (list1 == null) {
            return list2;
        } else if (list2 == null) {
            return list1;
        } else if (list1.val <= list2.val) {
            list1.next = mergeTwoLists(list1.next,list2);
            return list1;
        } else {
            list2.next = mergeTwoLists(list1, list2.next);
            return list2;
        }
    }
}
```

### 143   重排链表

找到链表中点+反转后半段链表+合并两部分的链表

```

class Solution {
    public void reorderList(ListNode head) {

        // 找到链表的中点
        // 反转后半端的链表
        // 合并两个部分的链表

        if (head == null) return;
        ListNode list2 = head;

        // 找到链表的中点
        ListNode midNode = getMidNode(head);

        ListNode list1 = midNode.next;
        midNode.next = null;
        // 反转后半段的链表
        list1 = reverse(list1);
        // 合并两个部分的链表
        mergeList(list2, list1);
    }

    private ListNode getMidNode(ListNode head) {
        // 找到链表的中点
        // 快慢指针
        ListNode fast = head;
        ListNode slow = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    // 反转链表
    private ListNode reverse(ListNode list) {
        ListNode pre = null;
        ListNode cur = list;
        while (cur != null) {
            ListNode temp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = temp;
        }
        return pre;
    }

    private void mergeList(ListNode list1, ListNode list2) {

        ListNode l1;
        ListNode l2;
        while (list1 != null && list2 != null) {
            l1 = list1.next;
            l2 = list2.next;

            list1.next = list2;
            list1 = l1;

            list2.next = list1;
            list2 = l2;

        }


    }

}
```

## day63 2025-9-11

### 146 LRU缓存 -- 虾皮爱考

这道题本意是让你**自己实现一个双向链表**，**这道题需要一个hashMap和一个双向链表**

```
class LRUCache {
    // 实现双向链表
    class DoubleLinkedlist {
        int key;
        int value;
        DoubleLinkedlist prev;
        DoubleLinkedlist next;

        public DoubleLinkedlist() {

        }

        public DoubleLinkedlist(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    private Map<Integer, DoubleLinkedlist> map = new HashMap<>();
    private int size;
    private int capacity;
    private DoubleLinkedlist head, tail;

    public LRUCache(int capacity) {

        this.size = 0;
        this.capacity = capacity;
        head = new DoubleLinkedlist();
        tail = new DoubleLinkedlist();
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        DoubleLinkedlist node = map.get(key);
        if (node == null) {
            return -1;
        }
        // 如果存在，需要先通过哈希表定位，再移到头部
        moveToHead(node);
        return node.value;
    }

    public void put(int key, int value) {

        DoubleLinkedlist node = map.get(key);
        if (node == null) {
            //如果不存在
            //创建一个新的节点
            DoubleLinkedlist newNode = new DoubleLinkedlist(key, value);
            map.put(key, newNode);
            //添加到双向链表的头部
            addToHead(newNode);
            size++;
            if (size > capacity) {
                //如果超出容量
                // 把双向链表的尾部移除
                DoubleLinkedlist tail1 = removeTail();
                //
                map.remove(tail1.key);
                size--;
            }
        } else {
            //如果key存在
            node.value = value;
            moveToHead(node);
        }


    }

    public void removeNode(DoubleLinkedlist node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    public void addToHead(DoubleLinkedlist node) {
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }

    public void moveToHead(DoubleLinkedlist node) {
        removeNode(node);
        addToHead(node);
    }

    public DoubleLinkedlist removeTail() {
        final DoubleLinkedlist res = tail.prev;
        removeNode(res);
        return res;

    }


}


```

##  day 64 2025-9-15

### 239 滑动窗口的最大值

用优先队列的思想，优先队列（最大值）也就是最大堆的思想，这种最值思想是最适合用优先级队列，优先级队列默认是最小堆，这里面重写那个Comparator方法，让其变成最大堆

```java
import java.util.Comparator;
import java.util.PriorityQueue;

class Solution {

    public int[] maxSlidingWindow(int[] nums, int k) {
        //优先队列，最大堆
        int length = nums.length;
        PriorityQueue<int[]> pq = new PriorityQueue<>(new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                return o1[0] != o2[0] ? o2[0] - o1[0] : o2[1] - o1[1];
            }
        });
        for (int i = 0; i < k; i++) {
            pq.offer(new int[]{nums[i], i});
        }
        //从索引k开始往后移动
        int[] res = new int[length - k + 1];
        res[0] = pq.peek()[0];
        for (int i = k; i < length; i++) {
            pq.offer(new int[]{nums[i], i});
            //还要看最大堆的堆顶元素在不在当前的滑动窗口种
            while (pq.peek()[1] <= i - k) {
                pq.poll();
            }
            res[i - k + 1] = pq.peek()[0];

        }
        return res;
    }

}
```

### 124 二叉树中的最大路径和

思想：直接看代码的思想就是递归，maxGain函数是一个递归函数，该节点的最大贡献值等于节点的值+max(左节点的最大贡献值，右节点的最大贡献值)

```
class Solution {
    int maxSum = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        // 从根节点开始递归
        maxGain(root);
        return maxSum;
    }

    //递归函数
    public int maxGain(TreeNode node) {
        if (node == null) return 0;
        //递归计算左右子节点的最大贡献值
        int leftGain = Math.max(maxGain(node.left), 0);
        int rightGain = Math.max(maxGain(node.right), 0);

        //节点的最大路径和取决于该节点的值与该节点的左右子节点的最大贡献值
        int priceNewPath = node.val + leftGain + rightGain;
        //更新答案
        maxSum = Math.max(maxSum, priceNewPath);
        return node.val + Math.max(leftGain, rightGain);


    }
}
```

## day 65 2025-9-17

### 295 数据流的中位数

用最大堆和最小堆，优先队列默认是最小堆

用两个优先队列记录分别记录大于中位数的最小值和小于中位数的最大值

```java
import java.util.PriorityQueue;


class MedianFinder {
    // 两个优先级队列，一个是大堆，一个是小堆
    PriorityQueue<Integer> pqLeft;
    PriorityQueue<Integer> pqRight;//默认是小堆

    public MedianFinder() {
        pqLeft = new PriorityQueue<>((a, b) -> (b - a));
        pqRight = new PriorityQueue<>();
    }

    public void addNum(int num) {
        if (pqLeft.isEmpty() || num <= pqLeft.peek()) {
            pqLeft.offer(num);
            if (pqLeft.size() > pqRight.size() + 1) {
                pqRight.offer(pqLeft.poll());
            }
        } else {
            pqRight.offer(num);
            if (pqRight.size() > pqLeft.size()) {
                pqLeft.offer(pqRight.poll());
            }
        }

    }

    public double findMedian() {
        double result;
        if (pqLeft.size() == pqRight.size()) {
            result = (double) (pqLeft.peek() + pqRight.peek()) / 2;
        } else {
            result = pqLeft.peek();
        }
        return result;

    }
}

```

## day66-2025-9-19

### mysql - 每位教师所教授的科目种类的数量

-- 按照教师来分组，

```
# Write your MySQL query statement below
-- 按照老师分组 
-- DISTINCT 去重
select teacher_id,count(DISTINCT subject_id) as cnt from Teacher group by teacher_id; 
```

### mysql-查询近30天活跃的用户

--主要是时间的判断，最近20天的活跃用户，小于等于2019-07-27

可以这么写：==activity_date between date_add('2019-07-27',interval -29 day) and '2019-07-27'==

```
-- 主要是时间的判断
select activity_date as day,count(distinct user_id) as active_users
from Activity
where activity_date between date_add('2019-07-27',interval -29 day) and '2019-07-27'
group by activity_date
```

### mysql-部门工资前三高的所有员工 - hard

-- 学习sql的窗口函数  **dense_rank() over(partition by sth order by sth)**

- ==`rank` 是跳次排序 `1,1,1,4`, `dense_rank`是不跳次排序`1,1,1,2`, `row_number`是顺序`1,2,3,4`==

```
select Department,Employee,Salary
from
(
    select t2.name Department,t1.name Employee,t1.salary Salary,dense_rank() over(partition by departmentId order by salary desc) ranks
    from  Employee t1
    left join Department t2
    on t1.departmentId=t2.id
) t
where ranks<=3
```

### 32 最长有效括号

**采用动态规划，==dp[i]代表以i结尾的字符串的最长有效括号的长度，必须是以i结尾的。而且只有在遇到')'的时候才会有最长有效括号配对的情况出现。==**

除了用动态规划，**还可以用栈来实现**，第一种做法用动态规划，第二种用栈，我觉得用动态规划其实更好理解。。。

```java
class Solution {
    public int longestValidParentheses(String s) {
        if (s.length() == 0) {
            return 0;
        }
        //动态规划
        int maxLen = 0;
        int[] dp = new int[s.length()];
        
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == ')') {
                if (s.charAt(i - 1) == '(') {
                    dp[i] = (i - 2 >= 0 ? dp[i - 2] : 0) + 2;
                } else {
                    if (i - dp[i - 1] - 1 >= 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                        dp[i] = dp[i - 1] + (i - dp[i - 1] - 2 >= 0 ? dp[i - dp[i - 1] - 2] : 0) + 2;
                    }
                }
                maxLen = Math.max(maxLen, dp[i]);
            }
        }
        return maxLen;
    }

}
```

我们始终==保持栈底元素为当前已经遍历过的元素中「最后一个没有被匹配的右括号的下标」==，这样的做法主要是考虑了边界条件的处理，栈里其他元素维护左括号的下标：

- 对于遇到的每个 ‘(’ ，我们将它的下标放入栈中

- 对于遇到的每个 ‘)’ ，我们先弹出栈顶元素表示匹配了当前右括号：

   如果栈为空，说明当前的右括号为没有被匹配的右括号，我们将其下标放入栈中来更新我们之前提到的「最后一个没有被匹配的右  括号的下标」

  如果栈不为空，当前右括号的下标减去栈顶元素即为「以该右括号为结尾的最长有效括号的长度」

```java
class Solution {
    public int longestValidParentheses(String s) {
        if (s.length() == 0) {
            return 0;
        }
        // 利用栈来实现
        int maxLen = 0;
        Deque<Integer> stack = new LinkedList<>();
        stack.push(-1);

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (stack.isEmpty()) {
                    stack.push(i);
                } else {
                    maxLen = Math.max(maxLen, i - stack.peek());
                }
            }
        }
        return maxLen;
    }
}
```



## day67 2025-9-21

### mysql- 至少有5名直接下属的经理

有一张表，自身连接，having

首先查询每个人的下属员工数。将两份 Employee 表用 join 操作连接。Manager 表代表经理，Report 表代表下属，每对 Manager.Id=Report.ManagerId 的情况代表此经理的一名下属。再根据 Manager.Id 分组，直接使用 having 字句筛选下属大于 5 的经理

```
# Write your MySQL query statement below
select Manager.name as name 
from Employee as Manager join Employee as Report
on Manager.Id = Report.ManagerId
group by Manager.Id
having count(Report.Id) >= 5

```

### mysql-确认率

这道题其实我觉得是考察**AVG函数**的使用。
根据需求可以看出，答案也就是一个公式：confirmed消息的数量 / 总数。
可以考虑使用AVG函数，需要注意的是AVG函数是可以写条件判断的。

1. 使用**AVG函数计算confirmed的平均值，如果不存在则为NULL**
2. 使用**IFNULL把NULL值转换为0**
3. 最后使用**ROUND精确到小数点后两位**

```
# Write your MySQL query statement below
select 
    s.user_id ,
    ROUND(IFNULL(AVG(c.action='confirmed'), 0), 2) as confirmation_rate
from
    Signups as s
left join
    Confirmations as c
on
    s.user_id=c.user_id
group by
    s.user_id
```

## Day68 2025-9-22

### 704 二分查找 - 快手爱出变形的题目

数组原本就是有序的，并且是升序的；**也就是说二分查找适合于有序的数组查找**

```java
class Solution {
    public int search(int[] nums, int target) {

        int left = 0;
        int right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;

            int num = nums[mid];

            if (num == target) {
                return mid;

            } else if (num > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }

        }
        return -1;


    }
}
```

### 二分查找变形题-找出目标元素出现的次数

```
使用二分查找在某个有序的数组中查找出目标元素出现的次数
```

```java
package testcode;

public class Solution2 {

    // 使用二分查找在某个有序的数组中查找出目标元素出现的次数

   
    public int countNum(int[] nums, int target) {

        if (nums == null || nums.length == 0) {
            return 0;
        }
        // 查找左边界
        int leftIndex = findLeftIndex(nums, target);
        if (leftIndex == -1) return 0;
        int rightIndex = findRightiIndex(nums, target);

        return rightIndex - leftIndex + 1;
    }

    private int findLeftIndex(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        int firstIndex = -1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) {
                firstIndex = mid;
                high = mid - 1;//继续向左
            } else if (nums[mid] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }

        }
        return firstIndex;
    }

 // 查找右边界
    private int findRightiIndex(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        int firstIndex = -1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) {
                firstIndex = mid;
                low = mid + 1;// 继续向右查找

            } else if (nums[mid] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return firstIndex;


    }

    public static void main(String[] args) {
        Solution2 solution2=new Solution2();
        int[] nums=new int[]{
                1,2,2,3,3,3,4,4,4,4
        };
        int target=4;
        int result=solution2.countNum(nums,target);
        System.out.println(result);
    }


}
```

## day69 2025-9-23

### 合并两个有序链表 - 递归

```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        //递归解法
        if (list1 == null) {
            return list2;
        } else if (list2 == null) {
            return list1;
        } else if (list1.val <= list2.val) {
            list1.next = mergeTwoLists(list1.next, list2);
            return list1;
        } else if (list2.val <= list1.val) {
            list2.next = mergeTwoLists(list2.next, list1);
            return list2;
        }
        return null;


    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

### mysql- 1045 买下所有产品的客户

==**用到group by分组，distinct（）作用于列上，主要是去重；having是过滤操作**==

用户不重复的product_key数量等于Product表的product_key数量即为买下所有产品的客户

先按照用户id分组，然后计数等于Product表中的product_key数量。

```mysql
select customer_id
from Customer
group by customer_id
having count(distinct(product_key))=(select count(product_key) from Product)
```

## Day70 2025-9-24

### 56 合并区间

先给数组排序；

这个不是官方解法，应该是我看某个题解写的

```java


import java.util.Arrays;
import java.util.LinkedList;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public int[][] merge(int[][] intervals) {
        if (intervals.length == 1) return intervals;
        // 先排序
        Arrays.sort(intervals, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
        //
        LinkedList<int[]> result = new LinkedList<>();
        int count = 0;
        // 开始遍历
        int i=0;
        for ( i = 1; i < intervals.length; i++) {
            if (intervals[i][0] <= intervals[i - 1][1]) {
                //说明区间是有重叠的
                intervals[i][0] = Math.min(intervals[i][0], intervals[i - 1][0]);
                intervals[i][1] = Math.max(intervals[i][1], intervals[i - 1][1]);
            } else {
                result.add(intervals[i - 1]);
                count++;
            }
        }
        result.add(intervals[i - 1]);
        return result.toArray(new int[count + 1][2]);
    }
}
//leetcode submit region end(Prohibit modification and deletion)
```



## day71 2025-9-25

### 230 二叉搜索树中第k小的元素

二叉搜索树的性质：中序遍历得到的是一个递增的序列，就可以从中序序列中找到第k小的元素

```java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        //中序遍历 从小到大 （二叉搜索树的性质）
        // 找到第k小的元素
        Deque<TreeNode> stack = new ArrayDeque<TreeNode>();
        while (root != null || !stack.isEmpty()) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            --k;
            if (k == 0) {
                break;
            }
            root = root.right;
        }
        return root.val;
    }
}
```

## Day 72 2025-10-10

### 399 除法求值

这是一道并查集的解答思路，一边查询一边修改结点是并查集的特色

```java
import java.util.HashMap;
import java.util.List;
import java.util.Map;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    Map<String,Double> weight=new HashMap<>();
    Map<String,String> f=new HashMap<>();
    public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {

        // 并查集的解法
        //一边查询一边修改结点指向是并查集的特色
        for (int i = 0; i < values.length; i++) {
            List<String> strs=equations.get(i);
            String a=strs.get(0);
            String b=strs.get(1);

            if(!weight.containsKey(a)){
                f.put(a,a);
                weight.put(a,1.0);
            }
            if(!weight.containsKey(b)){
                f.put(b,b);
                weight.put(b,1.0);
            }
            add(a,b,values[i]);
        }
        int m=queries.size();
        double[] ans=new double[m];
        for (int i = 0; i < m; i++) {
            List<String> strs=queries.get(i);
            String a=strs.get(0);
            String b=strs.get(1);
            if(!weight.containsKey(a)||!weight.containsKey(b)||!find(a).equals(find(b))){
                ans[i]=-1.0;
            }else {
                ans[i]=weight.get(a)/weight.get(b);
            }

        }
        return ans;

    }
    public void  add(String x,String y,double value){
        String fx=find(x);
        String fy=find(y);
        if(fx.equals(fy)) return;
        f.put(fx,fy);
        weight.put(fx,value*weight.get(y)/weight.get(x));
    }
    public String find(String x){
        if(x==f.get(x)) return x;
        String y=f.get(x);
        f.put(x,find(y));
        weight.put(x,weight.get(x)*weight.get(y));
        return f.get(x);
    }

}
```

## day73 2025-10-11

### 621 任务调度器

这里是使用贪心算法，

```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;
class Solution {
    public int leastInterval(char[] tasks, int n) {
        // 使用贪心算法来做
        int[] map = new int[26];
        for (int i = 0; i < tasks.length; i++) {
            // 计算每个字母出现的次数
            map[tasks[i] - 'A']++;
        }
        Arrays.sort(map);// 排序，从小到大: 0,0,0,0,3,5,6,7
      // AXXAXXA
      // 如果A和B出现次数相同，那么就是ABX ABX AB
        int minLen = (n + 1) * (map[25] - 1) + 1;
        for (int i = 24; i >= 0; i--) {
            if (map[i] == map[25]) {
                minLen++;
            }
        }
        return Math.max(minLen, tasks.length);
    }
}
```

## day 74. 2025-10-13

### 312 戳气球

没太看懂，一道动态规划的题目。。。。。。。

```java
//有 n 个气球，编号为0 到 n - 1，每个气球上都标有一个数字，这些数字存在数组 nums 中。 
//
// 现在要求你戳破所有的气球。戳破第 i 个气球，你可以获得 nums[i - 1] * nums[i] * nums[i + 1] 枚硬币。 这里的 i -
// 1 和 i + 1 代表和 i 相邻的两个气球的序号。如果 i - 1或 i + 1 超出了数组的边界，那么就当它是一个数字为 1 的气球。 
//
// 求所能获得硬币的最大数量。 
//
// 
//示例 1：
//
// 
//输入：nums = [3,1,5,8]
//输出：167
//解释：
//nums = [3,1,5,8] --> [3,5,8] --> [3,8] --> [8] --> []
//coins =  3*1*5    +   3*5*8   +  1*3*8  + 1*8*1 = 167 
//
// 示例 2： 
//
// 
//输入：nums = [1,5]
//输出：10
// 
//
// 
//
// 提示： 
//
// 
// n == nums.length 
// 1 <= n <= 300 
// 0 <= nums[i] <= 100 
// 
//
// Related Topics 数组 动态规划 👍 1464 👎 0


//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public int maxCoins(int[] nums) {

        // 用动态规划

        int n = nums.length;
        int[][] rec = new int[n + 2][n + 2];
        int[] val = new int[n + 2];

        val[0] = val[n + 1] = 1;

        for (int i = 1; i <= n; i++) {
            val[i] = nums[i - 1];
        }
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i + 2; j <= n + 1; j++) {
                for (int k = i + 1; k < j; k++) {
                    int sum = val[i] * val[k] * val[j];
                    sum += rec[i][k] + rec[k][j];
                    rec[i][j] = Math.max(rec[i][j], sum);
                }
            }
        }
        return rec[0][n + 1];

    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

## day75 2025-10-14

### 10 正则表达式匹配

这道题用了动态规划，没太看懂。。。

```java
//给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配。 
//
// 
// '.' 匹配任意单个字符 
// '*' 匹配零个或多个前面的那一个元素 
// 
//
// 所谓匹配，是要涵盖 整个 字符串 s 的，而不是部分字符串。 
//
// 示例 1： 
//
// 
//输入：s = "aa", p = "a"
//输出：false
//解释："a" 无法匹配 "aa" 整个字符串。
// 
//
// 示例 2: 
//
// 
//输入：s = "aa", p = "a*"
//输出：true
//解释：因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
// 
//
// 示例 3： 
//
// 
//输入：s = "ab", p = ".*"
//输出：true
//解释：".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
// 
//
// 
//
// 提示： 
//
// 
// 1 <= s.length <= 20 
// 1 <= p.length <= 20 
// s 只包含从 a-z 的小写字母。 
// p 只包含从 a-z 的小写字母，以及字符 . 和 *。 
// 保证每次出现字符 * 时，前面都匹配到有效的字符 
// 
//
// Related Topics 递归 字符串 动态规划 👍 4121 👎 0


//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public boolean isMatch(String s, String p) {
        // 是用了动态规划，但是这道题挺难，没有看懂。。。。
        int m = s.length();
        int n = p.length();

        boolean[][] f = new boolean[m + 1][n + 1];
        f[0][0] = true;
        for (int i = 0; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (p.charAt(j - 1) == '*') {
                    f[i][j] = f[i][j - 2];
                    if (matches(s, p, i, j - 1)) {
                        f[i][j] = f[i][j] || f[i - 1][j];
                    }
                } else {
                    if (matches(s, p, i, j)) {
                        f[i][j] = f[i - 1][j - 1];
                    }
                }
            }
        }
        return f[m][n];
    }

    public boolean matches(String s, String p, int i, int j) {
        if (i == 0) {
            return false;
        }
        if (p.charAt(j - 1) == '.') {
            return true;
        }
        return s.charAt(i - 1) == p.charAt(j - 1);
    }
}

//leetcode submit region end(Prohibit modification and deletion)
```

### mysql - 查询小题 - 584 寻找用户推荐人

不等于不使用!= 而是使用**<>** ，判断是不是null不是用=而是**用is null 和is not null**

```mysql
# Write your MySQL query statement below
select name from Customer where referee_id <> 2 or referee_id is null;
```

## Day 76 2025-10-15

### 26 删除有序数组中重复项

这道题用的是**快慢指针**，先让快慢指针同时指向下标1,然后快指针向前移动，如果发现当前元素和前一个元素不同，就把当前元素的值复制给慢指针下标的元素，然后慢指针下标+1

```java
//给你一个 非严格递增排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 
//一致 。然后返回 nums 中唯一元素的个数。 
//
// 考虑 nums 的唯一元素的数量为 k ，你需要做以下事情确保你的题解可以被通过： 
//
// 
// 更改数组 nums ，使 nums 的前 k 个元素包含唯一元素，并按照它们最初在 nums 中出现的顺序排列。nums 的其余元素与 nums 的大小不
//重要。 
// 返回 k 。 
// 
//
// 判题标准: 
//
// 系统会用下面的代码来测试你的题解: 
//
// 
//int[] nums = [...]; // 输入数组
//int[] expectedNums = [...]; // 长度正确的期望答案
//
//int k = removeDuplicates(nums); // 调用
//
//assert k == expectedNums.length;
//for (int i = 0; i < k; i++) {
//    assert nums[i] == expectedNums[i];
//} 
//
// 如果所有断言都通过，那么您的题解将被 通过。 
//
// 
//
// 示例 1： 
//
// 
//输入：nums = [1,1,2]
//输出：2, nums = [1,2,_]
//解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
// 
//
// 示例 2： 
//
// 
//输入：nums = [0,0,1,1,1,2,2,3,3,4]
//输出：5, nums = [0,1,2,3,4]
//解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
// 
//
// 
//
// 提示： 
//
// 
// 1 <= nums.length <= 3 * 10⁴ 
// -10⁴ <= nums[i] <= 10⁴ 
// nums 已按 非严格递增 排列 
// 
//
// Related Topics 数组 双指针 👍 3852 👎 0


//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public int removeDuplicates(int[] nums) {
        // 快慢指针
        if (nums.length == 1) return 1;
        int fast = 1;
        int slow = 1;
        while (fast <= nums.length - 1) {
            if (nums[fast] != nums[fast - 1]) {
                nums[slow] = nums[fast];
                slow++;
            }
            fast++;
        }
        return slow;

    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

### 80 删除有序数组中重复项II

也是用快慢指针

```java
//给你一个有序数组 nums ，请你 原地 删除重复出现的元素，使得出现次数超过两次的元素只出现两次 ，返回删除后数组的新长度。 
//
// 不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。 
//
// 
//
// 说明： 
//
// 为什么返回数值是整数，但输出的答案是数组呢？ 
//
// 请注意，输入数组是以「引用」方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。 
//
// 你可以想象内部操作如下: 
//
// 
//// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
//int len = removeDuplicates(nums);
//
//// 在函数里修改输入数组对于调用者是可见的。
//// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
//for (int i = 0; i < len; i++) {
//    print(nums[i]);
//}
// 
//
// 
//
// 示例 1： 
//
// 
//输入：nums = [1,1,1,2,2,3]
//输出：5, nums = [1,1,2,2,3]
//解释：函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3。 不需要考虑数组中超出新长度后面的元素。
// 
//
// 示例 2： 
//
// 
//输入：nums = [0,0,1,1,1,1,2,3,3]
//输出：7, nums = [0,0,1,1,2,3,3]
//解释：函数应返回新长度 length = 7, 并且原数组的前七个元素被修改为 0, 0, 1, 1, 2, 3, 3。不需要考虑数组中超出新长度后面的元素
//。
// 
//
// 
//
// 提示： 
//
// 
// 1 <= nums.length <= 3 * 10⁴ 
// -10⁴ <= nums[i] <= 10⁴ 
// nums 已按升序排列 
// 
//
// Related Topics 数组 双指针 👍 1313 👎 0


//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 1 || nums.length == 2) return nums.length;
        int fast = 1; //初始的时候还是指向下标1
        int slow = 1;
        int count = 1;
        while (fast <= nums.length - 1) {
            if (nums[fast] != nums[fast - 1]) { // 计算重复的次数会不会超出2
                count = 1;
            } else {
                count++;
            }
            if (count <= 2) {
                nums[slow] = nums[fast]; //只有出现次数<=2才会把当前的元素复制给slow坐标的
                slow++;
            }
            fast++;
        }
        return slow;


    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

### 297 二叉树的序列化与反序列化

序列化：就是通过bfs或者dfs转换为字符串

反序列化：通过字符串构建一棵树

**本质上是二叉树的bfs或者dfs遍历和构造树**

```java
//序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方
//式重构得到原数据。 
//
// 请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串
//反序列化为原始的树结构。 
//
// 提示: 输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 LeetCode 序列化二叉树的格式。你并非必须采取这种方式，你也可以采用其他的
//方法解决这个问题。 
//
// 
//
// 示例 1： 
// 
// 
//输入：root = [1,2,3,null,null,4,5]
//输出：[1,2,3,null,null,4,5]
// 
//
// 示例 2： 
//
// 
//输入：root = []
//输出：[]
// 
//
// 示例 3： 
//
// 
//输入：root = [1]
//输出：[1]
// 
//
// 示例 4： 
//
// 
//输入：root = [1,2]
//输出：[1,2]
// 
//
// 
//
// 提示： 
//
// 
// 树中结点数在范围 [0, 10⁴] 内 
// -1000 <= Node.val <= 1000 
// 
//
// Related Topics 树 深度优先搜索 广度优先搜索 设计 字符串 二叉树 👍 1300 👎 0


//leetcode submit region begin(Prohibit modification and deletion)

import java.util.*;

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 * int val;
 * TreeNode left;
 * TreeNode right;
 * TreeNode(int x) { val = x; }
 * }
 */
public class Codec {
    // 这里面的序列化就是可以用dfs或者BFS遍历树就行
    // 反序列化就是根据序列构造一棵树

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        return dfsSerialize(root, "");
    }

    // 前序遍历的方法
    public String dfsSerialize(TreeNode root, String str) {
        if (root == null) {
            str += "None,";
        } else {
            str += str.valueOf(root.val) + ",";
            str = dfsSerialize(root.left, str);
            str = dfsSerialize(root.right, str);
        }
        return str;

    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] dataArray = data.split(",");
        // Arrays.asList(dataArray) 将数组转换为固定大小的List对象
        List<String> dataList = new LinkedList<String>(Arrays.asList(dataArray));
        return rdeserialize(dataList);

    }

    public TreeNode rdeserialize(List<String> dataList) {
        if (dataList.get(0).equals("None")) {
            dataList.remove(0);
            return null;
        }
        TreeNode root = new TreeNode(Integer.valueOf(dataList.get(0)));
        dataList.remove(0);
        root.left = rdeserialize(dataList);
        root.right = rdeserialize(dataList);

        return root;


    }
}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));
//leetcode submit region end(Prohibit modification and deletion)
```

## day 77 2025-10-16

### 274 H指数

总是想着排序之后正序遍历，为什么就想不到逆序遍历呢

逆序排序，比如排序后`[6, 5, 3, 1, 0]`，如果 `citations[i] > i`，那么前面的数必定大于`i`，所以找到`i`的最大值就是答案，因为 `i`从`0`开始，所以返回结果需要`i+1`

```java
//给你一个整数数组 citations ，其中 citations[i] 表示研究者的第 i 篇论文被引用的次数。计算并返回该研究者的 h 指数。 
//
// 根据维基百科上 h 指数的定义：h 代表“高引用次数” ，一名科研人员的 h 指数 是指他（她）至少发表了 h 篇论文，并且 至少 有 h 篇论文被引用次
//数大于等于 h 。如果 h 有多种可能的值，h 指数 是其中最大的那个。 
//
// 
//
// 示例 1： 
//
// 
//输入：citations = [3,0,6,1,5]
//输出：3 
//解释：给定数组表示研究者总共有 5 篇论文，每篇论文相应的被引用了 3, 0, 6, 1, 5 次。
//     由于研究者有 3 篇论文每篇 至少 被引用了 3 次，其余两篇论文每篇被引用 不多于 3 次，所以她的 h 指数是 3。 
//
// 示例 2： 
//
// 
//输入：citations = [1,3,1]
//输出：1
// 
//
// 
//
// 提示： 
//
// 
// n == citations.length 
// 1 <= n <= 5000 
// 0 <= citations[i] <= 1000 
// 
//
// Related Topics 数组 计数排序 排序 👍 612 👎 0


import java.util.Arrays;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);
        // 逆序遍历
        int h = 0;
        int i = citations.length - 1;
        while (i >= 0 && citations[i] > h) {
            h++;
            i--;
        }
        return h;

    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

## Day 78 2025-10-19

###  380 O(1) 时间插入、删除和获取随机元素

变长数组 = List集合，在O(1)的时间插入和删除元素

哈希表 可以在O1的时间内判断某个元素在不在

```java
//实现RandomizedSet 类： 
//
// 
// 
// 
// RandomizedSet() 初始化 RandomizedSet 对象 
// bool insert(int val) 当元素 val 不存在时，向集合中插入该项，并返回 true ；否则，返回 false 。 
// bool remove(int val) 当元素 val 存在时，从集合中移除该项，并返回 true ；否则，返回 false 。 
// int getRandom() 随机返回现有集合中的一项（测试用例保证调用此方法时集合中至少存在一个元素）。每个元素应该有 相同的概率 被返回。 
// 
// 
// 
//
// 你必须实现类的所有函数，并满足每个函数的 平均 时间复杂度为 O(1) 。 
//
// 
//
// 示例： 
//
// 
//输入
//["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", 
//"insert", "getRandom"]
//[[], [1], [2], [2], [], [1], [2], []]
//输出
//[null, true, false, true, 2, true, false, 2]
//
//解释
//RandomizedSet randomizedSet = new RandomizedSet();
//randomizedSet.insert(1); // 向集合中插入 1 。返回 true 表示 1 被成功地插入。
//randomizedSet.remove(2); // 返回 false ，表示集合中不存在 2 。
//randomizedSet.insert(2); // 向集合中插入 2 。返回 true 。集合现在包含 [1,2] 。
//randomizedSet.getRandom(); // getRandom 应随机返回 1 或 2 。
//randomizedSet.remove(1); // 从集合中移除 1 ，返回 true 。集合现在包含 [2] 。
//randomizedSet.insert(2); // 2 已在集合中，所以返回 false 。
//randomizedSet.getRandom(); // 由于 2 是集合中唯一的数字，getRandom 总是返回 2 。
// 
//
// 
//
// 提示： 
//
// 
// -2³¹ <= val <= 2³¹ - 1 
// 最多调用 insert、remove 和 getRandom 函数 2 * 10⁵ 次 
// 在调用 getRandom 方法时，数据结构中 至少存在一个 元素。 
// 
//
// Related Topics 设计 数组 哈希表 数学 随机化 👍 974 👎 0


import java.util.*;

//leetcode submit region begin(Prohibit modification and deletion)
class RandomizedSet {
    //变长数组+哈希表
    // 变长数组就是List集合
    List<Integer> nums;
    Map<Integer, Integer> indexMap;
    Random random;

    public RandomizedSet() {
        this.nums = new ArrayList<>();
        this.indexMap = new HashMap<>();
        this.random = new Random();
    }

    public boolean insert(int val) {
        // 先从哈希表中判断这个元素在不在
        if (indexMap.containsKey(val)) return false;// 存在就返回false；
        // 不存在的时候
        int index = nums.size();
        nums.add(val);
        indexMap.put(val, index);
        return true;
    }

    public boolean remove(int val) {
        // 删除的时候判断这个元素在不在
        // 如果不存在，返回false
        if (!indexMap.containsKey(val)) return false;
        // 存在的时候
        int last = nums.get(nums.size() - 1);//最后一个元素
        int index = indexMap.get(val);
        nums.set(index, last); //把最后一个元素放到这里
        indexMap.put(last, index);
        nums.remove(nums.size() - 1);//移除最后一个元素
        indexMap.remove(val);
        return true;

    }

    public int getRandom() {
        int index = random.nextInt(nums.size());
        return nums.get(index);

    }
}
```

## day79 2025-10-20

### 13 将罗马数字转换为整数

是一道比较简单的题目，题目理解就行

```java
//罗马数字包含以下七种字符: I， V， X， L，C，D 和 M。 
//
// 
//字符          数值
//I             1
//V             5
//X             10
//L             50
//C             100
//D             500
//M             1000 
//
// 例如， 罗马数字 2 写做 II ，即为两个并列的 1 。12 写做 XII ，即为 X + II 。 27 写做 XXVII, 即为 XX + V + 
//II 。 
//
// 通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5
// 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况： 
//
// 
// I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。 
// X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
// C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。 
// 
//
// 给定一个罗马数字，将其转换成整数。 
//
// 
//
// 示例 1: 
//
// 
//输入: s = "III"
//输出: 3 
//
// 示例 2: 
//
// 
//输入: s = "IV"
//输出: 4 
//
// 示例 3: 
//
// 
//输入: s = "IX"
//输出: 9 
//
// 示例 4: 
//
// 
//输入: s = "LVIII"
//输出: 58
//解释: L = 50, V= 5, III = 3.
// 
//
// 示例 5: 
//
// 
//输入: s = "MCMXCIV"
//输出: 1994
//解释: M = 1000, CM = 900, XC = 90, IV = 4. 
//
// 
//
// 提示： 
//
// 
// 1 <= s.length <= 15 
// s 仅含字符 ('I', 'V', 'X', 'L', 'C', 'D', 'M') 
// 题目数据保证 s 是一个有效的罗马数字，且表示整数在范围 [1, 3999] 内 
// 题目所给测试用例皆符合罗马数字书写规则，不会出现跨位等情况。 
// IL 和 IM 这样的例子并不符合题目要求，49 应该写作 XLIX，999 应该写作 CMXCIX 。 
// 关于罗马数字的详尽书写规则，可以参考 罗马数字 - 百度百科。 
// 
//
// Related Topics 哈希表 数学 字符串 👍 3017 👎 0


import java.util.HashMap;
import java.util.Map;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public int romanToInt(String s) {
        // 定义一个hashmap表
        Map<Character, Integer> map = new HashMap<>();
        map.put('I', 1);
        map.put('V', 5);
        map.put('X', 10);
        map.put('L', 50);
        map.put('C', 100);
        map.put('D', 500);
        map.put('M', 1000);
        // 判断当前字符如果比前一个小，就可以直接累加
        // 如果比前一个字符大，说明要相减
        int sum = 0;
        if (s.length() == 1)
            return map.get(s.charAt(0));

        for (int i = 1; i < s.length(); i++) {
            int cur = map.get(s.charAt(i));
            int pre = map.get(s.charAt(i - 1));

            if (cur <= pre) {
                sum += pre;

            } else {
                sum -= pre;
            }
            if (i == s.length() - 1) {
                sum += cur;
            }

        }
        return sum;
    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

## day80 2025-10-28

### 12 将整数转换成罗马数字

和13题很像

找不超过 num 的最大符号值，将 num 减去该符号值，然后继续寻找不超过 num 的最大符号值，将该符号拼接在上一个找到的符号之后，循环直至 num 为 0。最后得到的字符串即为 num 的罗马数字表示。

```java
//七个不同的符号代表罗马数字，其值如下： 
//
// 
// 
// 
// 符号 
// 值 
// 
// 
// 
// 
// I 
// 1 
// 
// 
// V 
// 5 
// 
// 
// X 
// 10 
// 
// 
// L 
// 50 
// 
// 
// C 
// 100 
// 
// 
// D 
// 500 
// 
// 
// M 
// 1000 
// 
// 
// 
//
// 罗马数字是通过添加从最高到最低的小数位值的转换而形成的。将小数位值转换为罗马数字有以下规则： 
//
// 
// 如果该值不是以 4 或 9 开头，请选择可以从输入中减去的最大值的符号，将该符号附加到结果，减去其值，然后将其余部分转换为罗马数字。 
// 如果该值以 4 或 9 开头，使用 减法形式，表示从以下符号中减去一个符号，例如 4 是 5 (V) 减 1 (I): IV ，9 是 10 (X) 减 
//1 (I)：IX。仅使用以下减法形式：4 (IV)，9 (IX)，40 (XL)，90 (XC)，400 (CD) 和 900 (CM)。 
// 只有 10 的次方（I, X, C, M）最多可以连续附加 3 次以代表 10 的倍数。你不能多次附加 5 (V)，50 (L) 或 500 (D)。如果
//需要将符号附加4次，请使用 减法形式。 
// 
//
// 给定一个整数，将其转换为罗马数字。 
//
// 
//
// 示例 1： 
//
// 
// 输入：num = 3749 
// 
//
// 输出： "MMMDCCXLIX" 
//
// 解释： 
//
// 
//3000 = MMM 由于 1000 (M) + 1000 (M) + 1000 (M)
// 700 = DCC 由于 500 (D) + 100 (C) + 100 (C)
//  40 = XL 由于 50 (L) 减 10 (X)
//   9 = IX 由于 10 (X) 减 1 (I)
//注意：49 不是 50 (L) 减 1 (I) 因为转换是基于小数位
// 
//
//
// 示例 2： 
//
// 
// 输入：num = 58 
// 
//
// 输出："LVIII" 
//
// 解释： 
//
// 
//50 = L
// 8 = VIII
// 
//
//
// 示例 3： 
//
// 
// 输入：num = 1994 
// 
//
// 输出："MCMXCIV" 
//
// 解释： 
//
// 
//1000 = M
// 900 = CM
//  90 = XC
//   4 = IV
// 
//
//
// 
//
// 提示： 
//
// 
// 1 <= num <= 3999 
// 
//
// Related Topics 哈希表 数学 字符串 👍 1435 👎 0


//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
    String[] symbols = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};

    public String intToRoman(int num) {
        StringBuffer sb = new StringBuffer();

        //模拟的方法
        for (int i = 0; i < values.length; i++) {

            int value = values[i];
            String symbol = symbols[i];
            while (num >= value) {
                num -= value;
                sb.append(symbol);
            }
            if (num == 0) {
                break;
            }
        }
        return sb.toString();
    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

### 6 Z字型变换

主要是**巧设flag**，flag控制行数的上下遍历

![image-20251028163006568](/Users/zmjz/Library/Application Support/typora-user-images/image-20251028163006568.png)

```java
//将一个给定字符串 s 根据给定的行数 numRows ，以从上往下、从左到右进行 Z 字形排列。 
//
// 比如输入字符串为 "PAYPALISHIRING" 行数为 3 时，排列如下： 
//
// 
//P   A   H   N
//A P L S I I G
//Y   I   R 
//
// 之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："PAHNAPLSIIGYIR"。 
//
// 请你实现这个将字符串进行指定行数变换的函数： 
//
// 
//string convert(string s, int numRows); 
//
// 
//
// 示例 1： 
//
// 
//输入：s = "PAYPALISHIRING", numRows = 3
//输出："PAHNAPLSIIGYIR"
// 
//
//示例 2：
//
// 
//输入：s = "PAYPALISHIRING", numRows = 4
//输出："PINALSIGYAHRPI"
//解释：
//P     I    N
//A   L S  I G
//Y A   H R
//P     I
// 
//
// 示例 3： 
//
// 
//输入：s = "A", numRows = 1
//输出："A"
// 
//
// 
//
// 提示： 
//
// 
// 1 <= s.length <= 1000 
// s 由英文字母（小写和大写）、',' 和 '.' 组成 
// 1 <= numRows <= 1000 
// 
//
// Related Topics 字符串 👍 2574 👎 0


import java.util.List;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public String convert(String s, int numRows) {
        if (numRows < 2) return s;
        List<StringBuilder> rows = new ArrayList<>();
        for (int i = 0; i < numRows; i++) {
            rows.add(new StringBuilder());
        }
        int i = 0;
        int flag = -1;
        for (char c : s.toCharArray()) {
            rows.get(i).append(c);
            if (i == 0 || i == numRows - 1) flag = -flag;
            i += flag;

        }
        StringBuilder sb = new StringBuilder();
        for (StringBuilder row : rows) {
            sb.append(row);

        }
        return sb.toString();


    }


}
//leetcode submit region end(Prohibit modification and deletion)
```

## day81 2025-10-29

### 125 验证回文串

**思路：双指针**

学会了两个函数

1. 使用 **replaceAll()** 配合正则表达式来去除字符串中非数字字母的字符

- [a-zA-Z0-9]：这是一个否定字符集。

-  在 [] 内部表示“非”（否定）。a-zA-Z 匹配所有小写字母和大写字母。0-9 匹配所有数字。所以 [^a-zA-Z0-9] 匹配任何**不是**字母或数字的字符。那么字符就可以替换成""

  s.replaceAll("[^a-zA-Z0-9]", "")

2. 将字符串中大写字母转换成小写字母，小写字母转换成大写字母，直接使用 **str.toLowerCase()**

   ```java
   //如果在将所有大写字符转换为小写字符、并移除所有非字母数字字符之后，短语正着读和反着读都一样。则可以认为该短语是一个 回文串 。 
   //
   // 字母和数字都属于字母数字字符。 
   //
   // 给你一个字符串 s，如果它是 回文串 ，返回 true ；否则，返回 false 。 
   //
   // 
   //
   // 示例 1： 
   //
   // 
   //输入: s = "A man, a plan, a canal: Panama"
   //输出：true
   //解释："amanaplanacanalpanama" 是回文串。
   // 
   //
   // 示例 2： 
   //
   // 
   //输入：s = "race a car"
   //输出：false
   //解释："raceacar" 不是回文串。
   // 
   //
   // 示例 3： 
   //
   // 
   //输入：s = " "
   //输出：true
   //解释：在移除非字母数字字符之后，s 是一个空字符串 "" 。
   //由于空字符串正着反着读都一样，所以是回文串。
   // 
   //
   // 
   //
   // 提示： 
   //
   // 
   // 1 <= s.length <= 2 * 10⁵ 
   // s 仅由可打印的 ASCII 字符组成 
   // 
   //
   // Related Topics 双指针 字符串 👍 845 👎 0
   
   
   //leetcode submit region begin(Prohibit modification and deletion)
   class Solution {
       public boolean isPalindrome(String s) {
           // 正则表达式推荐
           if (s.length() == 1) return true;
           String str = s.replaceAll("[^a-zA-Z0-9]", "");// 去掉所有非字母数字的字符
           // 把所有的大写字母全部变成小写字母
           str = str.toLowerCase();
           //使用双指针
           int left = 0;
           int right = str.length() - 1;
           while (left <= right) {
               if (str.charAt(left) != str.charAt(right)) {
                   return false;
               }
               left++;
               right--;
           }
           return true;
   
       }
   }
   //leetcode submit region end(Prohibit modification and deletion)
   ```

## day 82 2025-10-30

### 30 串联所有单词的字串

这道题的解题思路就是**滑动窗口**，那么怎么**判断窗口内的词与words完全匹配是关键**！！这道题挺难的，不太会写。。。这个解题过程的解释如下：

即窗口内放入words.length个单词，然后开始滑动, 每次滑动一个词(词的长度都是一样)，并判断窗口内的单词是否由words组成，比如s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]的情况，
第一次滑动流程
初始窗口 ['bar', 'foo','foo'] 未命中
入'bar'出'bar' ['foo','foo','bar'] 未命中
入'the'出'foo' ['foo','bar', 'the'] 命中 index 6
入'foo'出'foo' ['bar','the', 'foo'] 命中 index 9
入'bar'出'bar' ['the','foo','bar'] 命中index 12
入'man'出'the' ['foo','bar','man'] 未命中
结束
第二次滑动流程
初始窗口 ['arf','oof','oob'] 未命中
划动过程略
第三次滑动流程
初始窗口 ['rfo','ofo','oba'] 未命中
划动过程略

无需第四次滑动，因为第四次滑动，初始窗口就是第一次滑动流程划入一个词后的结果
['foo','foo','bar']后续流程与第一次滑动流程一模一样

如何高效判断窗口内的词与words完全匹配是此题的另一个关键
不考虑效率，自然可以复制一份窗口内容，然后遍历一次words，每次命中一个单词则删除掉copy window内该单词，遍历结束查看copy windows内是否有单词剩余，如果没有，则表示全部命中
这里使用hashmap的方式，窗口是一个hashmap，存储每个单词出现的次数，以第一次滑动窗口为例

初始窗口 {'bar':1, 'foo':2} 命中检测 {'bar':0, 'foo':1} 未命中
入'bar'出'bar' {'foo':2,'bar':1} 命中检测 {'foo':0, 'foo':1,'bar':0} 未命中
入'the'出'foo' ['foo':1,'bar':1, 'the':1] 命中检测{'foo':0, 'bar':0,'the':0} 命中
略

为了避免每次滑动完窗口，都要遍历一次words计算，可以初始就将words的值置为-1放入窗口, 这样只要窗口内所有词的出现次数是0 就是命中，而不匹配words的词划入的时候是1 划出之后变成0， 匹配words的词划入是0 划出又变成-1， 以第一次滑动窗口为例

预置 {'bar':-1, 'foo':-1,'the':-1}
初始窗口 {'bar':0,'foo':1, 'the':-1} 未命中
入'bar'出'bar' {'bar':0,'foo':1, 'the':-1} 未命中
入'the'出'foo' {'bar':0,'foo':0, 'the':0} 命中 index 6
入'foo'出'foo' {'bar':0,'foo':0, 'the':0} 命中 index 9
入'bar'出'bar' {'bar':0,'foo':0, 'the':0} 命中index 12
入'man'出'the' {'bar':0,'foo':0, 'the':-1,'man':1} 未命中

每次删除窗口map内计数为0的词，窗口map的大小为0，则命中

```java
//给定一个字符串 s 和一个字符串数组 words。 words 中所有字符串 长度相同。 
//
// s 中的 串联子串 是指一个包含 words 中所有字符串以任意顺序排列连接起来的子串。 
//
// 
// 例如，如果 words = ["ab","cd","ef"]， 那么 "abcdef"， "abefcd"，"cdabef"， "cdefab"，
//"efabcd"， 和 "efcdab" 都是串联子串。 "acdbef" 不是串联子串，因为他不是任何 words 排列的连接。 
// 
//
// 返回所有串联子串在 s 中的开始索引。你可以以 任意顺序 返回答案。 
//
// 
//
// 示例 1： 
//
// 
//输入：s = "barfoothefoobarman", words = ["foo","bar"]
//输出：[0,9]
//解释：因为 words.length == 2 同时 words[i].length == 3，连接的子字符串的长度必须为 6。
//子串 "barfoo" 开始位置是 0。它是 words 中以 ["bar","foo"] 顺序排列的连接。
//子串 "foobar" 开始位置是 9。它是 words 中以 ["foo","bar"] 顺序排列的连接。
//输出顺序无关紧要。返回 [9,0] 也是可以的。
// 
//
// 示例 2： 
//
// 
//输入：s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
//输出：[]
//解释：因为 words.length == 4 并且 words[i].length == 4，所以串联子串的长度必须为 16。
//s 中没有子串长度为 16 并且等于 words 的任何顺序排列的连接。
//所以我们返回一个空数组。
// 
//
// 示例 3： 
//
// 
//输入：s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
//输出：[6,9,12]
//解释：因为 words.length == 3 并且 words[i].length == 3，所以串联子串的长度必须为 9。
//子串 "foobarthe" 开始位置是 6。它是 words 中以 ["foo","bar","the"] 顺序排列的连接。
//子串 "barthefoo" 开始位置是 9。它是 words 中以 ["bar","the","foo"] 顺序排列的连接。
//子串 "thefoobar" 开始位置是 12。它是 words 中以 ["the","foo","bar"] 顺序排列的连接。 
//
// 
//
// 提示： 
//
// 
// 1 <= s.length <= 10⁴ 
// 1 <= words.length <= 5000 
// 1 <= words[i].length <= 30 
// words[i] 和 s 由小写英文字母组成 
// 
//
// Related Topics 哈希表 字符串 滑动窗口 👍 1282 👎 0


import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        // 用滑动窗口来解决
        // 怎么判断窗口里的字符串数组和给的字符串数组是一样的才是关键

        List<Integer> res = new ArrayList<>();
        int m = words.length;
        int n = words[0].length();
        int lens = s.length();
        for (int i = 0; i < n; i++) {
            if (i + m * n > lens) break;
            Map<String, Integer> differ = new HashMap<>();

            for (int j = 0; j < m; j++) {
                String word = s.substring(i + j * n, i + (j + 1) * n);
                differ.put(word, differ.getOrDefault(word, 0) + 1);
            }

            for (String word : words) {
                differ.put(word, differ.getOrDefault(word, 0) - 1);
                if (differ.get(word) == 0) {
                    differ.remove(word);
                }

            }
            for (int start = i; start < lens - m * n + 1; start += n) {
                if (start != i) {
                    String word = s.substring(start + (m - 1) * n, start + m * n);
                    differ.put(word, differ.getOrDefault(word, 0) + 1);
                    if (differ.get(word) == 0) {
                        differ.remove(word);
                    }
                    word = s.substring(start - n, start);
                    differ.put(word, differ.getOrDefault(word, 0) - 1);
                    if (differ.get(word) == 0) {
                        differ.remove(word);
                    }

                }
                if (differ.isEmpty()) {
                    res.add(start);
                }
            }

        }
        return res;

    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

## day83 2025-10-31

### 205 同构字符串

这道题比较简单，利用的是哈希表

hashmap判断key是否存在，也可以判断value是否存在

```java
map.containsKey（） // 判断key是否存在
```

```java
map.containsValue() // 判断value是否存在
```

```java
//给定两个字符串 s 和 t ，判断它们是否是同构的。 
//
// 如果 s 中的字符可以按某种映射关系替换得到 t ，那么这两个字符串是同构的。 
//
// 每个出现的字符都应当映射到另一个字符，同时不改变字符的顺序。不同字符不能映射到同一个字符上，相同字符只能映射到同一个字符上，字符可以映射到自己本身。 
//
// 
//
// 示例 1: 
//
// 
//输入：s = "egg", t = "add"
//输出：true
// 
//
// 示例 2： 
//
// 
//输入：s = "foo", t = "bar"
//输出：false 
//
// 示例 3： 
//
// 
//输入：s = "paper", t = "title"
//输出：true 
//
// 
//
// 提示： 
//
// 
// 
//
// 
// 1 <= s.length <= 5 * 10⁴ 
// t.length == s.length 
// s 和 t 由任意有效的 ASCII 字符组成 
// 
//
// Related Topics 哈希表 字符串 👍 800 👎 0


import java.util.HashMap;
import java.util.Map;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public boolean isIsomorphic(String s, String t) {

        // 1. 长度必须要是一样
        if (s.length() != t.length()) return false;
        // 2. 长度一样之后创建一个哈希表
        Map<Character, Character> map = new HashMap<>();
        int len = s.length();
        for (int i = 0; i < len; i++) {
            if (!map.containsKey(s.charAt(i)) && !map.containsValue(t.charAt(i))) {
                map.put(s.charAt(i), t.charAt(i));
            }
            if (!map.containsKey(s.charAt(i)) && map.containsValue(t.charAt(i))) {
                return false;
            }
            if (map.containsKey(s.charAt(i)) && map.get(s.charAt(i)) != t.charAt(i)) {
                return false;
            }

        }
        return true;

    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

## day84 2025-11-3

### 290 单词规律

和上述205一样的方法，都是哈希表，比较简单，不过这道题是字符到字符串之间的映射，字符串之间的比较要用**equals()**！！

注意点：**字符串之间用equals()比较，不是==或者!=**

```java
//给定一种规律 pattern 和一个字符串 s ，判断 s 是否遵循相同的规律。 
//
// 这里的 遵循 指完全匹配，例如， pattern 里的每个字母和字符串 s 中的每个非空单词之间存在着双向连接的对应规律。具体来说： 
//
// 
// pattern 中的每个字母都 恰好 映射到 s 中的一个唯一单词。 
// s 中的每个唯一单词都 恰好 映射到 pattern 中的一个字母。 
// 没有两个字母映射到同一个单词，也没有两个单词映射到同一个字母。 
// 
//
// 
//
// 示例1: 
//
// 
//输入: pattern = "abba", s = "dog cat cat dog"
//输出: true 
//
// 示例 2: 
//
// 
//输入:pattern = "abba", s = "dog cat cat fish"
//输出: false 
//
// 示例 3: 
//
// 
//输入: pattern = "aaaa", s = "dog cat cat dog"
//输出: false 
//
// 
//
// 提示: 
//
// 
// 1 <= pattern.length <= 300 
// pattern 只包含小写英文字母 
// 1 <= s.length <= 3000 
// s 只包含小写英文字母和 ' ' 
// s 不包含 任何前导或尾随对空格 
// s 中每个单词都被 单个空格 分隔 
// 
//
// Related Topics 哈希表 字符串 👍 723 👎 0


import java.util.HashMap;
import java.util.Map;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public boolean wordPattern(String pattern, String s) {


        String[] str = s.split(" ");

        if (pattern.length() != str.length)
            return false;

        // 创建哈希表
        Map<Character, String> map = new HashMap<>();
        for (int i = 0; i < str.length; i++) {
            if (!map.containsKey(pattern.charAt(i)) && !map.containsValue(str[i])) {
                map.put(pattern.charAt(i), str[i]);
            }
            if (map.containsValue(str[i]) && !map.containsKey(pattern.charAt(i))) {
                return false;
            }
            //字符串之间的比较用equals()
            if (map.containsKey(pattern.charAt(i)) && !map.get(pattern.charAt(i)).equals(str[i])) {
                return false;
            }


        }
        return true;

    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

### 219 存在重复元素II

很简单的哈希表判断重复元素之间的索引间隔

```java
//给你一个整数数组 nums 和一个整数 k ，判断数组中是否存在两个 不同的索引 i 和 j ，满足 nums[i] == nums[j] 且 abs(i 
//- j) <= k 。如果存在，返回 true ；否则，返回 false 。 
//
// 
//
// 示例 1： 
//
// 
//输入：nums = [1,2,3,1], k = 3
//输出：true 
//
// 示例 2： 
//
// 
//输入：nums = [1,0,1,1], k = 1
//输出：true 
//
// 示例 3： 
//
// 
//输入：nums = [1,2,3,1,2,3], k = 2
//输出：false 
//
// 
//
// 
//
// 提示： 
//
// 
// 1 <= nums.length <= 10⁵ 
// -10⁹ <= nums[i] <= 10⁹ 
// 0 <= k <= 10⁵ 
// 
//
// Related Topics 数组 哈希表 滑动窗口 👍 826 👎 0


import java.util.HashMap;
import java.util.Map;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {

        // 哈希表
        int lens = nums.length;
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (!map.containsKey(nums[i])) {
                map.put(nums[i], i);
            } else {
                int value = map.get(nums[i]);
                map.put(nums[i], i);
                if (i - value <= k) {
                    return true;
                }

            }


        }
        return false;


    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

## Day85 2025-11-4

### 228 汇总区间

就是找个所有连续的区间，比较简单的一道题

把int整型变成string用的是 **String.valueOf()**、**Integer.toString()**、或者**直接用"+"号**

可以直接用+号，通过java的自动类型转换，在底层，Java 编译器会创建一个 StringBuilder (或 StringBuffer) 对象，然后进行 append 操作，最后再调用 toString()。但是，大量循环中，性能比较差。推荐前两种。

```java
//给定一个 无重复元素 的 有序 整数数组 nums 。 
//
// 区间 [a,b] 是从 a 到 b（包含）的所有整数的集合。 
//
// 返回 恰好覆盖数组中所有数字 的 最小有序 区间范围列表 。也就是说，nums 的每个元素都恰好被某个区间范围所覆盖，并且不存在属于某个区间但不属于 
//nums 的数字 x 。 
//
// 列表中的每个区间范围 [a,b] 应该按如下格式输出： 
//
// 
// "a->b" ，如果 a != b 
// "a" ，如果 a == b 
// 
//
// 
//
// 示例 1： 
//
// 
//输入：nums = [0,1,2,4,5,7]
//输出：["0->2","4->5","7"]
//解释：区间范围是：
//[0,2] --> "0->2"
//[4,5] --> "4->5"
//[7,7] --> "7"
// 
//
// 示例 2： 
//
// 
//输入：nums = [0,2,3,4,6,8,9]
//输出：["0","2->4","6","8->9"]
//解释：区间范围是：
//[0,0] --> "0"
//[2,4] --> "2->4"
//[6,6] --> "6"
//[8,9] --> "8->9"
// 
//
// 
//
// 提示： 
//
// 
// 0 <= nums.length <= 20 
// -2³¹ <= nums[i] <= 2³¹ - 1 
// nums 中的所有值都 互不相同 
// nums 按升序排列 
// 
//
// Related Topics 数组 👍 463 👎 0


import java.util.ArrayList;
import java.util.List;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> res = new ArrayList<>();
        if (nums.length == 0) return res;
        int begin = 0;
        int end = 0;
        int lens = nums.length;
        for (int i = 0; i < lens - 1; i++) {
            if (nums[i + 1] - nums[i] == 1) {
                end++;
                if (i + 1 == lens - 1) {
                    String str = String.valueOf(nums[begin]) + "->" + String.valueOf(nums[end]);
                    res.add(str);
                }
            } else {
                if (begin != end) {
                    String str = String.valueOf(nums[begin]) + "->" + String.valueOf(nums[end]);
                    res.add(str);
                } else {
                    String str = String.valueOf(nums[begin]);
                    res.add(str);
                }
                end++;
                begin = end;
            }

        }
        if (begin == end) {
            String str = String.valueOf(nums[begin]);
            res.add(str);
        }
        return res;


    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

## day 86 2025-11-5

### 57 插入区间

返回是一个二维数组，先把结果存到List集合中，再把结果从集合转变到二维数组中

分为三种情况考虑：

1. 区间在要插入区间的左边
2. 区间在要插入区间的右边
3. 两个区间有重叠，要进行区间的合并

```java
//给你一个 无重叠的 ，按照区间起始端点排序的区间列表 intervals，其中 intervals[i] = [starti, endi] 表示第 i 个区
//间的开始和结束，并且 intervals 按照 starti 升序排列。同样给定一个区间 newInterval = [start, end] 表示另一个区间的
//开始和结束。 
//
// 在 intervals 中插入区间 newInterval，使得 intervals 依然按照 starti 升序排列，且区间之间不重叠（如果有必要的话，
//可以合并区间）。 
//
// 返回插入之后的 intervals。 
//
// 注意 你不需要原地修改 intervals。你可以创建一个新数组然后返回它。 
//
// 
//
// 示例 1： 
//
// 
//输入：intervals = [[1,3],[6,9]], newInterval = [2,5]
//输出：[[1,5],[6,9]]
// 
//
// 示例 2： 
//
// 
//输入：intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
//输出：[[1,2],[3,10],[12,16]]
//解释：这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。
// 
//
// 
//
// 提示： 
//
// 
// 0 <= intervals.length <= 10⁴ 
// intervals[i].length == 2 
// 0 <= starti <= endi <= 10⁵ 
// intervals 根据 starti 按 升序 排列 
// newInterval.length == 2 
// 0 <= start <= end <= 10⁵ 
// 
//
// Related Topics 数组 👍 1018 👎 0


import java.util.ArrayList;
import java.util.List;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> res = new ArrayList<>();
        boolean flag = false;
        int left = newInterval[0];
        int right = newInterval[1];
        for (int[] interval : intervals) {
            //如果当前区间在new区间的右边
            if (interval[0] > newInterval[1]) {
                if (!flag) {
                    res.add(new int[]{left, right});
                    flag = true;
                }
                res.add(new int[]{interval[0], interval[1]});
            } else if (interval[1] < newInterval[0]) { // 如果当前区间在new的左边
                res.add(new int[]{interval[0], interval[1]});
            } else {
                // 如果都不是，说明重叠的
                left = Math.min(left, interval[0]);
                right = Math.max(right, interval[1]);
            }
        }

        if (!flag) {
            res.add(new int[]{left, right});
        }
        int[][] result = new int[res.size()][2];
        for (int i = 0; i < res.size(); i++) {
            result[i] = res.get(i);
        }

        return result;

    }

}
//leetcode submit region end(Prohibit modification and deletion)
```

## DAY87 2025-11-6

### 71 简化区间

这种目录结构的就是会用栈来解决，栈的实现一般选择的是双端队列

`Deque<String> stack = new ArrayDeque<>();`//双端队列实现栈

只需要想明白什么哪些是需要入栈的就可以！！出栈的情况就一种，就是遇到上级目录的时候才会出栈。

```java
//给你一个字符串 path ，表示指向某一文件或目录的 Unix 风格 绝对路径 （以 '/' 开头），请你将其转化为 更加简洁的规范路径。 
//
// 在 Unix 风格的文件系统中规则如下： 
//
// 
// 一个点 '.' 表示当前目录本身。 
// 此外，两个点 '..' 表示将目录切换到上一级（指向父目录）。 
// 任意多个连续的斜杠（即，'//' 或 '///'）都被视为单个斜杠 '/'。 
// 任何其他格式的点（例如，'...' 或 '....'）均被视为有效的文件/目录名称。 
// 
//
// 返回的 简化路径 必须遵循下述格式： 
//
// 
// 始终以斜杠 '/' 开头。 
// 两个目录名之间必须只有一个斜杠 '/' 。 
// 最后一个目录名（如果存在）不能 以 '/' 结尾。 
// 此外，路径仅包含从根目录到目标文件或目录的路径上的目录（即，不含 '.' 或 '..'）。 
// 
//
// 返回简化后得到的 规范路径 。 
//
// 
//
// 示例 1： 
//
// 
// 输入：path = "/home/" 
// 
//
// 输出："/home" 
//
// 解释： 
//
// 应删除尾随斜杠。 
//
// 示例 2： 
//
// 
// 输入：path = "/home//foo/" 
// 
//
// 输出："/home/foo" 
//
// 解释： 
//
// 多个连续的斜杠被单个斜杠替换。 
//
// 示例 3： 
//
// 
// 输入：path = "/home/user/Documents/../Pictures" 
// 
//
// 输出："/home/user/Pictures" 
//
// 解释： 
//
// 两个点 ".." 表示上一级目录（父目录）。 
//
// 示例 4： 
//
// 
// 输入：path = "/../" 
// 
//
// 输出："/" 
//
// 解释： 
//
// 不可能从根目录上升一级目录。 
//
// 示例 5： 
//
// 
// 输入：path = "/.../a/../b/c/../d/./" 
// 
//
// 输出："/.../b/d" 
//
// 解释： 
//
// "..." 在这个问题中是一个合法的目录名。 
//
// 
//
// 提示： 
//
// 
// 1 <= path.length <= 3000 
// path 由英文字母，数字，'.'，'/' 或 '_' 组成。 
// path 是一个有效的 Unix 风格绝对路径。 
// 
//
// Related Topics 栈 字符串 👍 840 👎 0


import java.util.ArrayDeque;
import java.util.Deque;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public String simplifyPath(String path) {
        // 用栈
        // 这个栈是用双端队列实现的
        String[] names = path.split("/");
        Deque<String> stack = new ArrayDeque<>();//双端队列实现栈

        for (String name : names) {
            if ("..".equals(name)) {
                // 说明要弹出当前栈顶元素
                if (!stack.isEmpty()) {
                    stack.pollLast();
                }
            } else if (name.length() > 0 && !".".equals(name)) {
                stack.offerLast(name);
            }
        }
        StringBuilder sb = new StringBuilder();

        if (stack.isEmpty()) {
            sb.append("/");
        } else {

            while (!stack.isEmpty()) {
                sb.append("/");
                sb.append(stack.pollFirst());
            }
        }
        return sb.toString();


    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

## Day 88 2025-11-7

### 92 反转链表II

有多种解法，今天自己使用的是用栈的方法

这种反转的解法：**头插法、虚拟头结点、还有这种用栈仅仅增加了一点空间，但是逻辑会清晰很多，可读性也会很高。**

```java
//给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链
//表节点，返回 反转后的链表 。
//
// 
//
// 示例 1： 
// 
// 
//输入：head = [1,2,3,4,5], left = 2, right = 4
//输出：[1,4,3,2,5]
// 
//
// 示例 2： 
//
// 
//输入：head = [5], left = 1, right = 1
//输出：[5]
// 
//
// 
//
// 提示： 
//
// 
// 链表中节点数目为 n 
// 1 <= n <= 500 
// -500 <= Node.val <= 500 
// 1 <= left <= right <= n 
// 
//
// 
//
// 进阶： 你可以使用一趟扫描完成反转吗？ 
//
// Related Topics 链表 👍 2023 👎 0


//leetcode submit region begin(Prohibit modification and deletion)


import java.util.ArrayDeque;
import java.util.Deque;
import java.util.List;
/*

public class ListNode {
    int val;
    ListNode next;

    ListNode() {
    }

    ListNode(int val) {
        this.val = val;
    }

    ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}
*/

class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        // 虚拟头结点也可以实现
        // 借助一个栈来实现
        Deque<Integer> stack = new ArrayDeque<>();
        int index = 1;
        ListNode pre = null;
        ListNode end = null;
        ListNode node = head;
        while (node != null) {
            if (index == left - 1) {
                // 标记前一个pre结点
                pre = node;
            }
            // 标记后面一个结点
            if (index == right + 1) {
                end = node;
            }
            if (index >= left && index <= right) {
                // 入栈
                stack.offerLast(node.val);
            }
            node = node.next;
            index++;
        }
        // pre可能为null而且end也可可能为null
        // 要解决这个问题就是用虚拟头结点来解决
        ListNode vhead = new ListNode(-600);
        vhead.next = head;

        ListNode cur = new ListNode(stack.pollLast());
        if (pre != null) {
            pre.next = cur;
        } else {
            vhead.next = cur;
        }
        while (!stack.isEmpty()) {
            ListNode newNode = new ListNode(stack.pollLast());
            cur.next = newNode;
            cur = cur.next;
        }
        cur.next = end;
        return vhead.next;
    }

}
//leetcode submit region end(Prohibit modification and deletion)
```

## Day 89 2025-11-10

### 200 岛屿数量

**再次重刷了一遍岛屿数量，用dfs深度优先搜索解决**

```java
//给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。 
//
// 岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。 
//
// 此外，你可以假设该网格的四条边均被水包围。 
//
// 
//
// 示例 1： 
//
// 
//输入：grid = [
//  ['1','1','1','1','0'],
//  ['1','1','0','1','0'],
//  ['1','1','0','0','0'],
//  ['0','0','0','0','0']
//]
//输出：1
// 
//
// 示例 2： 
//
// 
//输入：grid = [
//  ['1','1','0','0','0'],
//  ['1','1','0','0','0'],
//  ['0','0','1','0','0'],
//  ['0','0','0','1','1']
//]
//输出：3
// 
//
// 
//
// 提示： 
//
// 
// m == grid.length 
// n == grid[i].length 
// 1 <= m, n <= 300 
// grid[i][j] 的值为 '0' 或 '1' 
// 
//
// Related Topics 深度优先搜索 广度优先搜索 并查集 数组 矩阵 👍 2867 👎 0


//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public int numIslands(char[][] grid) {
        // dfs深度优先搜索
        // 这种解法可以理解为搜索过的岛屿全都为0
        if (grid == null || grid.length == 0) {
            return 0;
        }
        int row = grid.length;
        int col = grid[0].length;
        int lands = 0;

        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (grid[i][j] == '1') {
                    lands++;
                    dfs(grid, i, j);
                }

            }

        }
        return lands;

    }

    private void dfs(char[][] grid, int row, int col) {
        int lenrow = grid.length;
        int lencol = grid[0].length;
        if (row < 0 || row > lenrow - 1 || col < 0 || col > lencol - 1 || grid[row][col] == '0') {
            return;
        }
        grid[row][col] = '0';
        dfs(grid, row - 1, col);// 上
        dfs(grid, row + 1, col); //下
        dfs(grid, row, col - 1);// 左
        dfs(grid, row, col + 1); // 右

    }
}
//leetcode submit region end(Prohibit modification and deletion)
```

## day90 2025-11-11

### 994 腐烂的橘子

**bfs广度优先搜索**，bfs解决最短路径、最少时间

**正确的逻辑应该是：**

- **第0分钟**：grid[0][0] 是腐烂的。
- **第1分钟**：grid[0][0] 腐烂了 (0,1) 和 (1,0)。现在 (0,1) 和 (1,0) 也变成了腐烂源。
- **第2分钟**：(0,1) 腐烂了 (0,2) 和 (1,1)。(1,0) 腐烂了 (1,1)（重复）和 (2,1)。
- **第3分钟**：(0,2) 和 (1,1) 开始腐烂 (1,2)。(2,1) 开始腐烂 (2,2)。
- **第4分钟**：(1,2) 和 (2,2) 腐烂了 (2,1) 的最后一个新鲜邻居（如果之前没被腐烂的话）。最终所有橘子都腐烂了。

这是一个**层层向外扩散**的过程，这正是**广度优先搜索（BFS）**的定义。**每一层搜索就代表一分钟**。

```java
//在给定的 m x n 网格
// grid 中，每个单元格可以有以下三个值之一： 
//
// 
// 值 0 代表空单元格； 
// 值 1 代表新鲜橘子； 
// 值 2 代表腐烂的橘子。 
// 
//
// 每分钟，腐烂的橘子 周围 4 个方向上相邻 的新鲜橘子都会腐烂。 
//
// 返回 直到单元格中没有新鲜橘子为止所必须经过的最小分钟数。如果不可能，返回 -1 。 
//
// 
//
// 示例 1： 
//
// 
//
// 
//输入：grid = [[2,1,1],[1,1,0],[0,1,1]]
//输出：4
// 
//
// 示例 2： 
//
// 
//输入：grid = [[2,1,1],[0,1,1],[1,0,1]]
//输出：-1
//解释：左下角的橘子（第 2 行， 第 0 列）永远不会腐烂，因为腐烂只会发生在 4 个方向上。
// 
//
// 示例 3： 
//
// 
//输入：grid = [[0,2]]
//输出：0
//解释：因为 0 分钟时已经没有新鲜橘子了，所以答案就是 0 。
// 
//
// 
//
// 提示： 
//
// 
// m == grid.length 
// n == grid[i].length 
// 1 <= m, n <= 10 
// grid[i][j] 仅为 0、1 或 2 
// 
//
// Related Topics 广度优先搜索 数组 矩阵 👍 1084 👎 0


import java.util.LinkedList;
import java.util.Queue;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public int orangesRotting(int[][] grid) {
        // 要用bfs广度优先搜索
        // 构造一个队列，把所有腐烂的橘子装进去
        // 计数新鲜的橘子
        int row = grid.length;
        int col = grid[0].length;
        int count = 0;
        int minute = 0;
        Queue<int[]> queue = new LinkedList<>();
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (grid[i][j] == 1) {
                    count++;
                }
                if (grid[i][j] == 2) {
                    queue.offer(new int[]{i, j});
                }
            }
        }
        while (count > 0 && !queue.isEmpty()) {
            minute++; //对应着第几层
            int n = queue.size();
            for (int i = 0; i < n; i++) {
                int[] arr = queue.poll();
                int r = arr[0];
                int c = arr[1];
                if (r - 1 >= 0 && grid[r - 1][c] == 1) {
                    grid[r - 1][c] = 2;
                    count--;
                    queue.offer(new int[]{r - 1, c});
                }
                if (r + 1 <= row - 1 && grid[r + 1][c] == 1) {
                    grid[r + 1][c] = 2;
                    count--;
                    queue.offer(new int[]{r + 1, c});
                }
                if (c - 1 >= 0 && grid[r][c - 1] == 1) {
                    grid[r][c - 1] =2;
                    count--;
                    queue.offer(new int[]{r, c - 1});
                }
                if (c + 1 <= col - 1 && grid[r][c + 1] == 1) {
                    grid[r][c + 1] = 2;
                    count--;
                    queue.offer(new int[]{r, c + 1});
                }
            }
        }
        if (count > 0) {
            return -1;
        }
        return minute;


    }


}
//leetcode submit region end(Prohibit modification and deletion)
```
