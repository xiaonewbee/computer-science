#### [剑指 Offer 31. 栈的压入、弹出序列](https://leetcode.cn/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)

难度中等356

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

```java

class Solution {
    // 网友神qi的法子，修改pushed数组，使得pop过的后面元素一个一个向前替换，覆盖前面的值，可能用到别的题解，这算一个算法吧
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        int i=0,j=0;
        for(int num:pushed){
            pushed[i]=num;
            while(i>=0&&pushed[i]==popped[j]){
                j++;
                i--;
            }
            i++;
        }
        return i==0;
    }
}
// 
// 1234567
//   i
// 4532176
//  j
class Solution {
    // 网友神qi的法子，修改pushed数组，使得pop过的后面元素一个一个向前替换，覆盖前面的值，可能用到别的题解，这算一个算法吧
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        int i=0,j=0;
        for(int num:pushed){
            pushed[i]=num;
            while(i>=0&&pushed[i]==popped[j]){
                j++;
                i--;
            }
            i++;
        }
        return i==0;
    }
}
// 
// 1234567
//   i
// 4532176
//  j

```

