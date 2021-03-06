﻿# 剑指offerDay2
#1
题目描述
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项。
n<=39

    public class Solution {
    public int Fibonacci(int n) {
           if(n == 0){
               return 0;
           }else if(n==1){
               return 1;
           }else{
               return Fibonacci(n-1)+Fibonacci(n-2);
           }
       }
    } 


----------


    public class Solution {
    public int Fibonacci(int n) {
           if(n == 0){
               return 0;
           }else if(n==1){
               return 1;
           }else{
               return Fibonacci(n-1)+Fibonacci(n-2);
           }
       }

}


```
斐波那契数列（Fibonacci sequence），又称 黄金分割数列、因数学家列昂纳多·斐波那契（Leonardoda Fibonacci）以兔子繁殖为例子而引入，故又称为“ 兔子数列”，指的是这样一个数列：1、1、2、3、5、8、13、21、34、……在数学上，斐波纳契数列以如下被以 递归的方法定义：F(0)=0，F(1)=1, F(n)=F(n-1)+F(n-2)（n>=2，n∈N*）
```

#2

题目描述
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

288ms
    
    class Solution {
    public int JumpFloor(int target) {
        if(target == 1){
            return 1;
        }else if(target == 2){
            return 2;
        }else {
            target = JumpFloor(target-1)+JumpFloor(target-2);
            return target;
        }
    }
}

##方法2    28ms  快了10倍
    public class Solution {
    public int JumpFloor(int target) {
          if(target<3){
              return target;
          }
        int f1 = 1,f2=2,f3=0;
        for(int i=1;i<=target-2;i++){
            f3=f1+f2;
            f1 = f2;
            f2 = f3;
            
        };
        return f3;
    }
}



```
对于本题,前提只有 一次 1阶或者2阶的跳法。
a.如果两种跳法，1阶或者2阶，那么假定第一次跳的是一阶，那么剩下的是n-1个台阶，跳法是f(n-1);
b.假定第一次跳的是2阶，那么剩下的是n-2个台阶，跳法是f(n-2)
c.由a\b假设可以得出总跳法为: f(n) = f(n-1) + f(n-2) 
d.然后通过实际的情况可以得出：只有一阶的时候 f(1) = 1 ,只有两阶的时候可以有 f(2) = 2
e.可以发现最终得出的是一个斐波那契数列：
        
           | 1, (n=1)
f(n) =     | 2, (n=2)
           | f(n-1)+f(n-2) ,(n>2,n为整数)

方法2   主要是为了避免重复计算；加快速度

```

#3
题目描述
一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

    public class Solution {
    public int JumpFloorII(int target) {
        if(target <=2 ){
            return target;
        }else {
            int s = 2*JumpFloorII(target-1);
            return s;
        }
    }
    }
    
```
分析： 无论怎样分析第一次就行了：
跳1阶，跳法为 f（n-1）；
跳2阶，跳法为 f（n-2）；
跳3阶，跳法为 f（n-3）；
跳n阶，跳法为 f（0）；
  所以 f（n）=f（0）+f（1）+.....f（n-2）+f(n-1)；
  而f(n-1) = f(0)+f(1)+....f(n-2);
  
  因此：f(n)=2*f(n-1);

```

#4
题目描述
我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

    public class Solution {
    public int RectCover(int target) {
        if(target <=2 ){
            return target;
        }
        int f1= 1,f2=2,f3=0;
        for(int i=1;i<=target-2;i++){
            f3=f1+f2;
            f1=f2;
            f2=f3;
        }
        return f3;
        
    }
    }
    
```
 还是斐波那契数列；
 分析：
 还是看第一层，
 若竖着放，则 f（n-2）；
 横着放，则 f（n-1）；
 因此 f(n)=f(n-1)+f(n-2);
 
```

#5
题目描述
输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

    public class Solution {
    public int NumberOf1(int n) {
        int count = 0;
        while( n!=0 ){
            count++;
            n = n & (n-1);
        }
        return count;
    }
    }
    
```
如果一个整数不为0，那么这个整数至少有一位是1。如果我们把这个整数减1，那么原来处在整数最右边的1就会变为0，原来在1后面的所有的0都会变成1(如果最右边的1后面还有0的话)。其余所有位将不会受到影响。
举个例子：一个二进制数1100，从右边数起第三位是处于最右边的一个1。减去1后，第三位变成0，它后面的两位0变成了1，而前面的1保持不变，因此得到的结果是1011.我们发现减1的结果是把最右边的一个1开始的所有位都取反了。这个时候如果我们再把原来的整数和减去1之后的结果做与运算，从原来整数最右边一个1那一位开始所有位都会变成0。如1100&1011=1000.也就是说，把一个整数减去1，再和原整数做与运算，会把该整数最右边一个1变成0.那么一个整数的二进制有多少个1，就可以进行多少次这样的操作。
```

#6
题目描述
给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

    public class Solution {
    public double Power(double base, int exponent) {
        double  result = 1.0;
        if(exponent==0){
            return 1;
        }
        for(int i=0;i<Math.abs(exponent);i++){
            result *= base;
        }
        if(exponent<0){
            result = 1/result;
        }
        return result;
    }
    }


```
 方法1 很平庸不够完美，
 方法2 利用递归；
 递归：n为偶数，a^n=a^n/2*a^n/2;n为奇数，a^n=（a^（n-1）/2）*（a^（n-1/2））*a
时间复杂度O（logn）
```