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