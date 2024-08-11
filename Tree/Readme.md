**94 **Inorder Traversal:-**
   ```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
       ArrayList<Integer> ans = new ArrayList<>();
       helper(root,ans);
       return ans;
        
    }
    public static void helper(TreeNode root,ArrayList<Integer> ans){
        if(root ==null){
            return ;
        }
        helper(root.left,ans);
        ans.add(root.val);
    helper( root.right,ans);        
    }
}
```
**144. Binary Tree Preorder Traversal**
```

class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        preorder(root,result);
        return result;
    }
    public void preorder(TreeNode root,List<Integer> result){
      if(root==null){
        return;
      }
      result.add(root.val);
      preorder(root.left,result);
      preorder(root.right,result);
    }
}
```
**145. Binary Tree Postorder Traversal**
```
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        postorder(root,result);
        return result;
    }
    public void postorder(TreeNode root,List<Integer> result){
        if(root==null){
            return ;
        }
        postorder(root.left,result);
        postorder(root.right,result);
        result.add(root.val);
    }
}
```


