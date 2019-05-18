# 剑指Offer
解题方法总结

## 斐波那契数列  （尾递归）
- 使用伪递归  F(n) = F(n-1)+b
- 当编译器检测到一个函数调用是尾递归的时候，它就覆盖当前的活动记录而不是在栈中去创建一个新的。编译器可以做到这点，因为递归调用是当前活跃期内最后一条待执行的语句，于是当这个调用返回时栈帧中并没有其他事情可做，因此也就没有保存栈帧的必要了。通过覆盖当前的栈帧而不是在其之上重新添加一个，这样所使用的栈空间就大大缩减了，这使得实际的运行效率会变得更高。
```
// 0 1 1 2 3 5 8 13.......
public class Solution {
    public int Fibonacci(int n) {
        return Fibonacci(n,0,1); //n == 2 返回 s1+s2==0+1
    }
     
     
    private static int Fibonacci(int n,int s1,int s2){
        if(n==0) return 0;
        if(n==1) return s2;
        else     return Fibonacci(n - 1, s2, s1 + s2);
    }
}
```
## 跳台阶    （尾递归）
- 一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。
## 矩形覆盖
- 我们可以用2X1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2X1的小矩形无重叠地覆盖一个2Xn的大矩形，总共有多少种方法？
```
// 0 1 2 3 5 8
public class Solution {
    public int JumpFloor(int target) {
        return Jump(target,1,2);//n == 2 返回 s1+s2==1+2
    }
    
    public int Jump(int n, int s1, int s2){
        if(n == 0){
            return 0;
        }else if(n == 1){
            return 1;
        }else if(n == 2){
            return s2;
        }else{
            return Jump(n-1,s2,s1+s2);
        }
        
    }
}

```
- 只需要满足 F(n) = F(n-1)+b这种动态规划的问题都适合用尾递归解决。
- F（n）= F(n-1)+F(n-2)+...+F(1)这种也可以。如变态跳台阶：
- Q:一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。
- A:2的n次方
```
import java.lang.Math; //可以直接else返回Math.pow(2,taget-1)
// 0 1 2 4 8 16 .....
public class Solution {
    public int JumpFloorII(int target) {
        if(target == 0){
            return 0;
        }else if(target == 1){
            return 1;
        }else{
            return 2*JumpFloorII(target-1);
        }
    }
}
```

## 二进制中1的个数  (位操作)
- Q:输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。
- A:刚开始想着把int转为以二进制表示方法转为String，然后数1的个数，后来看了讨论区，orz：  位操作
```
public class Solution {
    public int NumberOf1(int n) {
        int result=0;
        int test=n;
        while (test!=0){
            test&=(test-1);
            result++;
        }
        return result;
    }
}
```
## 链表中倒数第k个结点  （快慢指针）
- Q:输入一个链表，输出该链表中倒数第k个结点
- A:快慢指针解决，先让快指针走k-1步，走完以后，慢指针开始和快指针一起走，当快指针到达链表尾部时候，慢指针就指向倒数第k个结点。
- 注意：在快指针走k-1步时要判断快指针是否为null，即有没有第k个结点的存在。如果是，返回null。
```
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        ListNode slow = head;
        ListNode fast = head;
        for(int i=0; i<k; i++){//快指针走k-1步
            if(fast == null){
                return null;
            }
            fast = fast.next;
        }
        while(fast != null){
            fast = fast.next;
            slow = slow.next;
        }
        return slow;
    }
}
```
未完待续...


