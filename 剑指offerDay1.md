# 剑指offerDay1
#1
##题目描述 103ms
在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数


----------
java代码

    public class Solution {
    public boolean Find(int target, int [][] array) {
     int n = array.length;
     int m = array[0].length;
     int y = n-1;
     int x = 0;
        while(y>=0&&x < m){
            if(array[x][y]==target){
                return true;
            }else if(array[x][y] > target){
                y--;
            }else{
                x++;
            }
        }
        return false;
        
    }
}


----------
注意点：
 可以从左下角开始寻找，或者右上角；
 当array[0][n-1]大于target时则向上移动，
 小于时则向又移动；
 **记得返回值（return）以及跨域的判断**
 


----------

#2
 
 题目描述
请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

java代码
### 方法1，正面插入：运行速度24ms 

    public class Solution {
    public String replaceSpace(StringBuffer str) {
    	int length = str.length();
        int spaceNum = 0;
        StringBuffer newStr = new StringBuffer();
        for(int i=0; i<length;i++){
            char a = str.charAt(i);
            if(a==' '){
                spaceNum ++ ;
                newStr.append("%20");
            }else {
                newStr.append(a);                               
            }
        };
        return newStr.toString();
                                         
    }
}

```
此问题好像在java中的运行时间为O（n）
此题的思路是从后往前插入；
第一次遍历记录空格的数量，从而求得newStr = spaceNumber*2 + length（每替换一个空格则增加2个长度则乘以2）；
```

### 方法2，牛客的答案
    
   	public class Solution {
		public String replaceSpace(StringBuffer str) {
			int spacenum = 0;// spacenum为计算空格数
			for (int i = 0; i < str.length(); i++) {
				if (str.charAt(i) == ' ')
					spacenum++;
			}
			int indexold = str.length() - 1; 
			// indexold为为替换前的str下标
			int newlength = str.length() + spacenum * 2;
			// 计算空格转换成%20之后的str长度
			int indexnew = newlength - 1;
			// indexold为为把空格替换为%20后的str下标
			str.setLength(newlength);
			// 使str的长度扩大到转换成%20之后的长度,防止下标越界
			for (; indexold >= 0 && indexold < newlength; --indexold) {
				if (str.charAt(indexold) == ' ') { 
					str.setCharAt(indexnew--, '0');
					str.setCharAt(indexnew--, '2');
					str.setCharAt(indexnew--, '%');
				} else {
					str.setCharAt(indexnew--,
					str.charAt(indexold));
				}
			}
			return str.toString();
		}
	}
	
#3
题目描述
输入一个链表，从尾到头打印链表每个节点的值。

    public class Solution {
		ArrayList<Integer> arrayList = new ArrayList<Integer>();
		public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
			if (listNode != null) {
				this.printListFromTailToHead(listNode.next);
				arrayList.add(listNode.val);
			}
			return arrayList;
		}
	}

	public class ListNode {
		int val;
		ListNode next = null;

		ListNode(int val) {
			this.val = val;
		}
	}

```
 此方法主要是通过java的jvm中的java虚拟机栈来实现递归调用，而不必重新创建java.util.stack类的对象；
 在虚拟机栈中 每个方法被执行时都会创建一个栈帧，
 因此递归到最后导致：最后一个链表结点是第一个入栈的；
 而小细节  ArrayList必须是全局变量，不这么做的话每次递归调用会重新创建ArrayList，而我们的目的是为了返回一个ArrayList；
 
```
###方法2

    import java.util.ArrayList;
    import java.util.Stack;
    public class Solution2 {
	public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
		Stack<Integer> stack = new Stack<Integer>();
		while (listNode != null) {
			stack.push(listNode.val);
			listNode = listNode.next;
		}

		ArrayList<Integer> list = new ArrayList<Integer>();
		while (!stack.isEmpty()) {
			list.add(stack.pop());
		}
		return list;
	}
	}
	
```
 此方法是创建了一个util中的stack类来实现的
```


#4

题目描述
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。


```
先序遍历二叉树： 
1.先访问根节点；
2.先序遍历左子树；
3.先序遍历右子树；
中序遍历：
1.中序遍历左子树；
2.访问根节点；
3.中序遍历右子树；

```

    class Solution {
	public TreeNode reConstructBinaryTree(int[] pre, int[] in) {
		TreeNode root = reConstructBinaryTree(pre, 0, pre.length - 1, in, 0, in.length - 1);
		return root;
	}

	// 前序遍历{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}
	private TreeNode reConstructBinaryTree(int[] pre, int startPre, int endPre, int[] in, int startIn, int endIn) {

		if (startPre > endPre || startIn > endIn)
			return null;
		TreeNode root = new TreeNode(pre[startPre]);

		for (int i = startIn; i <= endIn; i++)
			if (in[i] == pre[startPre]) {
				root.left = reConstructBinaryTree(pre, startPre + 1, startPre + i - startIn, in, startIn, i - 1);
				root.right = reConstructBinaryTree(pre, i - startIn + startPre + 1, endPre, in, i + 1, endIn);
				break;
			}
		return root;
	}
	}

    class TreeNode {
	int val;
	TreeNode left;
	TreeNode right;

	TreeNode(int x) {
		val = x;
	}
	}

```
 这题好难。。。。。前序中序的索引 总是不对；
 
```

#5
题目描述
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

    class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    
    public void push(int node) {
       stack1.push(node);
    }
    
    public int pop() {
        int a;
        if(stack2.empty()){
            while(!stack1.empty()){
               a = stack1.pop();
                stack2.push(a);
            } ;
            
        };
        a = stack2.pop();
        
        return a ;
    }
}
```
 这题的话。。比较简单  主要是要判断 pop时栈2为空  和不为空的情况；
 为空时：必须要把栈1的全部元素压入到栈2中
```

#6

题目描述
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0


    import java.util.ArrayList;
    public class Solution {
    public int minNumberInRotateArray(int [] array) {
       int left = 0 ; int right = array.length-1;
        while(left < right){
           int mid = left+ (right-left)/2;
            if(array[right] < array[mid]){
                left = mid + 1 ;
            }else if(array[right] == array[mid]){
                 right = right - 1 ;
            }else{
                right = mid;
            };
        };
        return array[right];
    }
    }



```
 这题 若是从头到尾遍历的话则复杂度为O（n）但是明显没有利用到旋转数组的性质；
 小细节：int a = 7/2 = 3  而不是3.5  向下取整;
```
##重点！！！！！！
```
int middle=(low + high)/2 ; 存在整数溢出的风险，应改为
int middle=low + (high-low)/2 ;
这个人家回复是正确的。因为int是4字节，有一定范围。如果两个其中一个很大，相加容易超出这个范围，改成相减的形式可以一定程度避免。这种写法值得推崇！
---------------
还有二分查找指的是第一次二分后面都是递加1！！！！！
```