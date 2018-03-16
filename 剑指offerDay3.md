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



#2
题目描述
输入一个链表，输出该链表中倒数第k个结点。
    
    public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
    }
    public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        if(head == null || k <= 0){
            return null;
        }
        ListNode pre = head;
        ListNode last = head;
        for(int i =0;i<k-1;i++){
            if(last.next!=null){
                last= last.next;
            }else {
                return null;
            }
        }
        while(last.next!=null){
            last=last.next;
            pre=pre.next;
        };
        return pre;
    }
    }
    
```
Java代码，通过校验。代码思路如下：两个指针，先让第一个指针和第二个指针都指向头结点，然后再让第一个指正走(k-1)步，到达第k个节点。然后两个指针同时往后移动，当第一个结点到达末尾的时候，第二个结点所在位置就是倒数第k个节点了。。
```