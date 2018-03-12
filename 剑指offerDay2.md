# 剑指offerDay2

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
```



