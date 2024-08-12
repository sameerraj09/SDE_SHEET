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

**Left View:-**
Approach:-Just do the lever order and during adding the curr data to the ans array just add only first element of the level i.e i = 0;
And for right view last element for the level i = size;
```
class Tree
{
    //Function to return list containing elements of left view of binary tree.
    ArrayList<Integer> leftView(Node root)
    {
      // Your code here
      ArrayList<Integer> ans = new ArrayList<>();
      Queue<Node> q = new LinkedList<>();
      q.add(root);
      while(!q.isEmpty()){
       int size = q.size();
          for(int i = 0;i<size;i++){
           Node curr = q.remove();
           if(i==0)    ans.add(curr.data);
           if(curr.left !=null) q.add(curr.left);
             if(curr.right !=null) q.add(curr.right);
          }
      }
         return ans;
    }
 
}
```
**Botoom View**
In this we have to create a pair class of Node and col col means left and right distance from the root 
root = 0
root.left =-1
toot.right = 1

in this also we have to do the level order traversal
but in this we have to create a tree map for storing the col val and corre



