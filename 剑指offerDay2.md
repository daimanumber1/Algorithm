# 剑指offerDay2
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