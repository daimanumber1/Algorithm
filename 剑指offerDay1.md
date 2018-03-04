# 剑指offerDay1
#1
##题目描述
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
