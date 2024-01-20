## AVL树的旋转
1. 左旋转
2. 左右旋转
3. 右旋转
4. 右左旋转

## 构建过程
`懂了左旋，右旋是和左旋相反的过程，而左右旋和右左旋转是左旋和右旋组合的结果`
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    # 用于获取某个节点的高度
    def getHeight(self,root:Optional[TreeNode])->int:
        if not root:
            return 0
        return max(self.getHeight(root.left),self.getHeight(root.right))+1
    def buildAVL(self,root:Optional[TreeNode],val:int)->Optional[TreeNode]:
        if not root:
            return TreeNode(val)
        if root.val==val:
            return root
        if root.val>val:
            root.left=buildAVL(root.left)
            # 左右子树高度差大于一，不平衡了
            if self.getHeight(root.left)-self.getHeight(root.right)>1:
                # 如果节点被插入到了左子树的左子树上，则进行左旋转
                # 如果节点被插入到了左子树的右子树上，则进行左右旋转
                if val<root.left.val:
                    root=self.leftRotate(root)
                else:
                    root=self.rightLeftRotate(root)
        else:
            root.right=self.buildAVL(root.right,val)
            # 如果节点被插入到了右子树的右子树上，则进行右旋转
            # 如果节点被插入到了右子树的左子树上，则进行右左旋转
            if self.getHeight(root.right)-self.getHeight(root.left)>1:
                # 如果节点被插入到了右子树的右子树上，则进行右旋转
                if root.right.val<val:
                    root=self.rightRotate(root)
                else:
                    root=self.leftRightRotate(root)
        return root
    # 左旋操作
    def leftRotate(self,root:Optional[TreeNode])->Optional[TreeNode]:
        p=root.left
        root.left=p.right
        p.right=root
        return p
    # 右旋操作
    def rightRotate(self,root:Optional[TreeNode])->Optional[TreeNode]:
        p=root.right
        root.right=p.left
        p.left=root
        return p
    ## 左右旋操作：对root的左子树进行左旋转，然后对root进行右旋转
    def leftRightRotate(self,root:TreeNode)->Optional[TreeNode]:
        root.left=self.leftRotate(root.left)
        return self.rightRotate(root)
    ## 右左旋操作:对root的右子树进行右旋转，然后对root进行左旋转
    def rightLeftRotate(self,root:Optional[TreeNode])->Optional[TreeNode]:
        root.right=self.rightRotate(root.right)
        return self.leftRotate(root)
    def sortedListToBST(self, head: Optional[ListNode]) -> Optional[TreeNode]:
        p=head
        root=None
        while p is not None:
            val=p.val
            node=TreeNode(val)
            root=self.buildAVL(root,val)
            p=p.next
        return root
```
