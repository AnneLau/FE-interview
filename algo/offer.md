# 剑指offer算法总结

## offer

### 二维数组的查找

思路：从右上角或者左下角开始遍历

边界条件：二维数组的行或者列长度为0


### 替换空格

题目：请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。


思路：使用正则表达式：将空字符特换成‘%20’

### 从尾巴到头部打印链表的每个节点的值

思路：使用array的unshift方法，从左边将值塞进去
边界条件：链表长度为0的时候

### 重建二叉树

> 题目：输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

思路：先确定左右子树，然后递归求解

易错点是在这个地方
```js
node.left = reConstructBinaryTree(pre.slice(1,index+1),left);
    node.right = reConstructBinaryTree(pre.slice(index+1),right);
```
因为左右子树的数量是固定的，所以通过中序的index可以判定左右子树的位置


### 用两个栈实现队列

 主要是实现push和pop的方法
 
思路： 所有的push都往stack1中push
当stack2非空的时候，直接从stack2 pop出去
当stack2为空的时候，将stack1中所有的元素pop到stack2中去

### 旋转数组最小数字

如果可以使用
```js
return Math.min(...rotateArray)
```
如果不能就使用一个指针来判断

### Fibonacci
1. 常规解法：

思路：找一个中间变量记录下上一次的部分和

2. 使用尾递归

```
function Fibonacci2(n , ac1=0,ac2=1){
    if(n==0) return ac1;
    return Fibonacci2(n-1,ac2,ac1+ac2);
}
```

### 二进制1的个数

负数使用补码表示，这是最难的：

```js

function NumberOf1(n){
    if(n < 0){
        n = n >>> 0;
    }
    var arr = n.toString(2).split('');
    return arr.reduce(function(a,b){
        return b === "1" ? a + 1 : a;
    },0);
}
```

toString(2)表示转换为二进制  split拆分字符串变成数组



### 调整数组顺序使奇数位于偶数前面

用两个数组存下来

问题是：注意判断奇数偶数的方法是

```
(item&1)===1 奇数
```

### 输入一个链表：输出倒数第k个节点

快慢链表法：先让一个链表走k步

### 反转链表

使用递归

newHead只是一个虚有的概念

关键还是每一步的操作


### 合并两个排序的链表

注意最后将不用的链表指针消除掉，避免内存泄露

### 输入两颗二叉树A，B，判断B是不是A的子结构

借助一个辅助函数 isSubTree

### 镜像二叉树

递归

### 顺时针打印矩阵//还没看

### 栈的压入弹出序列 
这个很简单
第一层循环用来遍历pushV压入栈
第二层循环用来遍历popV弹出栈

### 从上到下打印二叉树--二叉树先序遍历

### 二叉搜索树后序遍历序列

从左到右扫描，找到左右子树分界线
然后判断右子树是否符合规定

然后递归判断左右子树

### 二叉树寻路


### 二叉搜索树转换双向链表

递归遍历

```javascript
function Convert(pRootOfTree)
{
    // write code here
    if(pRootOfTree==null) return pRootOfTree;
    
    if( pRootOfTree.left ==null&& pRootOfTree.right==null){
        return pRootOfTree;
    }
    if(pRootOfTree.left!=null){
    var left = Convert(pRootOfTree.left);
    
    var p = left;
    
    while(p!=null&&p.right!=null){
        p = p.right;
    }
    p.right = pRootOfTree;
    pRootOfTree.left = p;
    }
    if(pRootOfTree.right!=null){
    var right = Convert(pRootOfTree.right);
    pRootOfTree.right = right;
    right.left = pRootOfTree;
        }
    
    return left!=null?left:pRootOfTree;
}
```



### 连续子数组最大和

记录部分和
如果部分和小于0 部分和就是下一个数字
然后对部分和来一次冒泡，求出最大值

### 1到n中1出现的次数
正则

###



