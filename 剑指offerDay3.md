#剑指offerDay3

#1
题目描述
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

    public class Solution {
    public void reOrderArray(int [] array) {
        int a=0;
        int length  = array.length;
        int[] b = new int[length] ;
        for(int i=0;i<length;i++){
            if(array[i]%2 != 0){
            	b[a] = array[i];
                a++;
            }
        };
        for(int i=0;i<length;i++){
            if(array[i]%2 == 0){
                b[a] = array[i];
                a++;
            }
        };
        for(int c=0;c<length;c++){
            array[c]= b[c];
        }
    }
    }

```
有点low的方法。。。。。
方法传递的是引用传递的复制  而不是引用传递本身，因此必须改变每个数组的值   而不是用 array=b赋值  ，因为如果这样做无法实现真正的改变 
```




