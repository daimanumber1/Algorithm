# day3
 
#1
题目描述
定义栈的数据结构，请在该类型中实现一个能够得到栈最小元素的min函数。




    import java.util.Stack;
    public class Solution {
    Stack<Integer> stack1 =new Stack<Integer>();;
    Stack<Integer> stack2 =new Stack<Integer>();;
    public void push(int node) {
        stack1.push(node);
        if(stack2.empty() || stack2.peek() >=node){
            stack2.push(node);
        }else {
             stack2.push(stack2.peek());
        }
    }
    public void pop() {
        stack1.pop();
        stack2.pop();
    }
    public int top() {
        return stack1.peek();
    }
    public int min() {
        return stack2.peek();
    }
    }

```
添加一个辅助栈；
如果push的值大于辅助栈的栈顶时则辅助栈push之前的值；不然push node 
核心： 用辅助栈的栈顶来看最小值
```

#2
题目描述
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4，5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

    import java.util.ArrayList;
    import java.util.Stack;
    public class Solution {
        public boolean IsPopOrder(int [] pushA,int [] popA) {
            Stack<Integer> s = new Stack<Integer>();
            int index = 0;
            for(int i=0;i<pushA.length;i++){
                s.push(pushA[i]);
                while( !s.empty()&& s.peek() == popA[index]){
                    s.pop();
                    index++;
                }
            };
            return s.empty();
        }
    }


```
 感觉智商被压制；
 利用辅助栈。。。。
```
