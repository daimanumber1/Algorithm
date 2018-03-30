# day3
 
#1
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.




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



