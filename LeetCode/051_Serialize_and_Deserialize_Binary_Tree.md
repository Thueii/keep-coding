# 二叉树的序列化与反序列化

Link => [二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

## 题目
序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

提示: 输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 LeetCode 序列化二叉树的格式。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。


**示例1**
>输入：root = [1,2,3,null,null,4,5]<br />
>输出：[1,2,3,null,null,4,5]<br />

**示例2**
>输入：root = []<br />
>输出：[]<br />

**执行结果：通过 显示详情**
第一想法：要一个每一层的list，然后遍历这个list，再赋值这个list！
虽然写的很烂，意思还是到了= =，结果也还可以。
看了题解，其他人也是每次要做两次，一个left 一个right，ok

- 执行用时：88 ms, 在所有 Python3 提交中击败了99.06% 的用户
内存消耗：19.8 MB, 在所有 Python3 提交中击败了17.05% 的用户
通过测试用例：52 / 52
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return "null"
        tmp = [root]
        res = [str(root.val)]
        layer = []
        while True:
            while tmp:
                cur = tmp.pop()
                if cur.left:
                    layer.append(cur.left)
                    res.append(str(cur.left.val))
                else:
                    res.append("null")
                if cur.right:
                    layer.append(cur.right)
                    res.append(str(cur.right.val))
                else:
                    res.append("null")
            if layer:
                tmp = layer[::-1]
                layer = []
            else:
                break

        my_res  = "+".join(res)
        print(my_res)
        return my_res
    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if data == "null":
            return None
        res = data.split("+")
        res = res[::-1]
        root = TreeNode(res.pop())
        layer = [root]
        while True:
            temp = []
            while layer:
                cur = layer.pop()
                if res:
                    left = res.pop()
                    cur.left = TreeNode(left) if left != "null" else None
                else:
                    break
                if res:
                    right = res.pop()
                    cur.right = TreeNode(right) if right != "null" else None
                else:
                    break

                if cur.left:
                    temp.append(cur.left)
                if cur.right:
                    temp.append(cur.right)
            if temp:
                layer = temp[::-1]
                temp = []
            else:
                break
        return root

# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))

```
**Tag: 数、深度优先搜索、广度优先搜索、设计、字符串、二叉树**
