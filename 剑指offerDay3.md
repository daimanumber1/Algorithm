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


#3
题目描述
输入一个链表，反转链表后，输出链表的所有元素。

    /*
    public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
    }*/
    public class Solution {
    public ListNode ReverseList(ListNode head) {
        if(head ==null)return null;
        ListNode pre = null;
        ListNode curr = head;
        ListNode nex = head.next;
        while(curr != null){
            curr.next = pre;
             pre = curr;
            curr = nex;
            if(curr == null){
                nex =null;
            }else{
               nex = curr.next; 
            }
           
        };
        return pre;
    }
    }
    
```
根据题目描述可知为：单链表，因此 用指针来代表下标；
其实这题用2个指针就可以了；

```


#4
题目描述
输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

    /*
    public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
    }*/
    public class Solution {
    public ListNode Merge(ListNode list1,ListNode list2) {
       if(list1 == null){
           return list2;
       }
       if(list2 == null){
           return list1;
        }
        if(list1.val <= list2.val){
            list1.next = Merge(list1.next, list2);
            return list1;
        }else{
            list2.next = Merge(list1, list2.next);
            return list2;
            }
    }
    }
    
```
解题思路:  用递归的最简单的方法就是用极限思维；
即 list1==null 或者 list1 = 1； list2 = 2  时 递归
```

#5

题目描述
输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）


    /**
    public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

    }
    */
    public class Solution {
    public boolean HasSubtree(TreeNode root1,TreeNode root2) {
        boolean result = false;
        if(root1 != null && root2 !=null){
            if(root1.val == root2.val){
                result = check(root1,root2);
            }
            if(!result){
                result = check(root1.left,root2);
            }
            if(!result){
                result = check(root1.right,root2);
            }
        }
          return result; 
    }
    public static boolean check(TreeNode startNode,TreeNode checkNode){
        if(checkNode == null){
            return true;
        }
        if(startNode == null ){
            return false; 
        }
        if(startNode.val!=checkNode.val){
            return false;
        }
        return check(startNode.left,checkNode.left) && check(startNode.right,checkNode.right);
    }
    }
    
    
```
    这题难题挺大无法理解；
    if(checkNode == null){
            return true;
        }
        if(startNode == null ){
            return false; 
        }
        这2行的位置不能互换，换了就出错
    
```


#6
题目描述
操作给定的二叉树，将其变换为源二叉树的镜像。
输入描述:
二叉树的镜像定义：源二叉树 
    	    8
    	   /  \
    	  6   10
    	 / \  / \
    	5  7 9 11
    	镜像二叉树
    	    8
    	   /  \
    	  10   6
    	 / \  / \
    	11 9 7  5
    
    /**
    public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

    }
    */
    public class Solution {
    public void Mirror(TreeNode root) {
        if(root == null){
            return;
        }
        if(root.left == null && root.right == null){
            return ;
        }
        TreeNode temp  = root.left;
        root.left = root.right;
        root.right = temp;
        Mirror(root.left);
        Mirror(root.right);
        
    }
    }    	
    
```
 递归调用；
```