| 看着视频的 |          |          |
| ---------- | -------- | -------- |
| 1589       |          |          |
| 340        |          |          |
| 713        | 双指针   | 连续子集 |
| 1004       | 动态规划 |          |

# 做题经验



1. 我推荐的刷题顺序的规则是：

   按分类刷；每个分类从 Easy 到 Medium 顺序刷；
   优先刷 树、链表、二分查找、DFS、BFS 等面试常考类型；
   优先刷题号靠前的题目；
   优先刷点赞较多的题目；
   如果基本上能做到 Easy 题 100% 能做对，Medium 题经过思考或与面试官交流后能做对，基本就能拿到 Offer。在实际面试过程中，很少出 Hard 题，视能力刷。
   ————————————————
   版权声明：本文为CSDN博主「负雪明烛」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
   原文链接：https://blog.csdn.net/fuxuemingzhu/article/details/105183554

   

2. #### [剑指 Offer 05. 替换空格](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

   有同学问了，为什么要从后向前填充，从前向后填充不行么？

   从前向后填充就是O(n^2)的算法了，因为每次添加元素都要将添加元素之后的所有元素向后移动。

   **其实很多数组填充类的问题，都可以先预先给数组扩容带填充后的大小，然后在从后向前进行操作。**

   这么做有两个好处：

   1. 不用申请新数组。
   2. 从后向前填充元素，避免了从前先后填充元素要来的 每次添加元素都要将添加元素之后的所有元素向后移动。

```cpp
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if(!preorder.size()){   //判断是否为空
            return nullptr;
        }
        TreeNode* root = new TreeNode(preorder[0]); //先序的首为根节点
        stack<TreeNode*> stk;   //建立栈
        stk.push(root); //根节点入栈
        int inorderIndex = 0;   //扫描中序的指针
        for(int i = 1; i < preorder.size(); i++){   //从先序遍历开始逐个遍历
            TreeNode *node = stk.top();
            if(node->val != inorder[inorderIndex]){ //栈顶元素的值与中序遍历当前所指的元素值不等
                node->left = new TreeNode(preorder[i]); //前序遍历中处在栈顶元素位置后一位的元素是栈顶元素的左子树
                stk.push(node->left);   //栈顶元素左子树节点入栈
            }else{  //栈顶元素的值与中序遍历当前所指的元素值相等,栈顶即为最左下角的树节点
                while(!stk.empty() && stk.top()->val == inorder[inorderIndex]){ //while循环向上返回，寻找位置进行右子树的重建
                    node = stk.top();   //指针向右扫描中序遍历
                    stk.pop();  //栈中所有与当前指针所指元素值相等的节点出栈
                    inorderIndex++;
                }
                node->right = new TreeNode(preorder[i]);    // 循环结束后，node所指栈顶元素即是需要重建右子树的节点
                stk.push(node->right);
            }
        }
        return root;    
    }
};
```

