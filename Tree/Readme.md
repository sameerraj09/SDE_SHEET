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
**All traversal in one code**
Approach:-Making seperate function for all the traversal passing the arraylist to it 
and then add that value to the ArraList<ArrayList<Integer>> 
```
import java.util.ArrayList;
import java.util.List;
public class Solution {
    public static List<List<Integer>> getTreeTraversal(TreeNode root) {
        // Write your code here.
          List<List<Integer>> result = new ArrayList<>();
        if(root==null){
            return result ;
        }
    //    List<List<Integer>> result = new ArrayList<>();
        List<Integer> in = new ArrayList<>();
        inorder(root,in);
        result.add(in);
         List<Integer> pre = new ArrayList<>();
        preorder(root,pre);
        result.add(pre);
         List<Integer> post = new ArrayList<>();
        postorder(root,post);
        result.add(post);
        return result;
        
    }
    public static void inorder(TreeNode root,List<Integer> l1){
        if(root==null)  return;
        inorder(root.left, l1); 
         l1.add(root.data);     
          inorder(root.right, l1);

    }
     public static void preorder(TreeNode root,List<Integer> l1){
        if(root==null)  return;
          l1.add(root.data);   
        preorder(root.left, l1);   
          preorder(root.right, l1);

    }
     public static void postorder(TreeNode root,List<Integer> l1){
        if(root==null)  return;
        postorder(root.left, l1);     
          postorder(root.right, l1);
            l1.add(root.data); 

    }
}
```
**102. Binary Tree Level Order Traversal**
Approach:-
We have to do bfs type traversal for this we have to always use a queue
And by default always add the root the queue to it
Now run a loop when the queue is not empty it will ensure that all node is visite
Now inside the while find the size the queue 
after that run a for loop till the size
And do the following step 
First remove the node from the queue 
add the node val to ans
now check whether the left child is null or not if not add the left to the queue and do same for the child

always check the edge whether the root is null or not
```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        // List to store the final result, where each sublist represents a level in the tree
        List<List<Integer>> ans = new ArrayList<>();
        
        // If the root is null, return an empty list
        if (root == null) {
            return ans;
        }
        
        // Queue to facilitate level-order traversal (BFS)
        Queue<TreeNode> q = new LinkedList<>();
        
        // Start with the root node
        q.add(root);
        
        // While there are nodes to process in the queue
        while (!q.isEmpty()) {
            int size = q.size(); // Number of nodes at the current level
            ArrayList<Integer> currLevel = new ArrayList<>(); // List to store nodes at the current level
            
            // Process all nodes at the current level
            for (int i = 0; i < size; i++) {
                TreeNode curr = q.remove(); // Remove the front node from the queue
                currLevel.add(curr.val);    // Add the current node's value to the current level list
                
                // Enqueue left child if it exists
                if (curr.left != null) {
                    q.add(curr.left);
                }
                
                // Enqueue right child if it exists
                if (curr.right != null) {
                    q.add(curr.right);
                }
            }
            
            // Add the current level list to the final result list
            ans.add(currLevel);
        }
        
        // Return the list of levels
        return ans;
    }
}

```

**Left View:-**
Approach:-Just do the lever order and during adding the curr data to the ans array just add only first element of the level i.e i = 0; 
we just need the first element for every order

And for right view last element for the level i = size;
we just need the last element of each level
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
Approach:-

Data structure used:- Queue<Pair> , ArrayList<Integer>(for storing the ans) ,TreeMap<Integer,Intger>(we can also use integer and Node) for storing unique col and node data.

We have to return all the last element of column 
In this we have to create a pair class of Node and col
col means left and right distance from the root 
val of col changes
root = 0
root.left =-1
toot.right = 1

now in this problem we will do the level order but we have to deal with user defined data type i.e pair
so we add root  and 0 as col val to queue
after that we will do the same thing which we do with level order
now inplace of adding the answer to the arraylist we will add it to tree map

we no need to check anything because we need to take last col val so cal get replaced with the recent val
after that check the as usal things if node.left!=null add it to queue same for the right also

at last iterate over hash map and add all key val to the arrayList
```
class Solution {
    
    // Helper class to store a node and its corresponding column index
    class pair {
        Node n;   // The node itself
        int col;  // The column index of the node
        
        // Constructor to initialize the pair object
        public pair(Node n, int col) {
            this.n = n;
            this.col = col;
        }
    }
    
    // Function to return a list containing the bottom view of the given tree
    public ArrayList<Integer> bottomView(Node root) {
        // List to store the final bottom view nodes
        ArrayList<Integer> arr = new ArrayList<>();
        
        // Queue to facilitate level-order traversal (BFS)
        Queue<pair> q = new LinkedList<>();
        
        // TreeMap to store the node's data for each column index
        // TreeMap keeps keys in sorted order, so the bottom view will be from left to right
        TreeMap<Integer, Integer> tm = new TreeMap<>();
        
        // Start with the root node at column index 0
        q.add(new pair(root, 0));
        
        // While there are nodes to process in the queue
        while (!q.isEmpty()) {
            int size = q.size();
            
            // Process all nodes at the current level
            for (int i = 0; i < size; i++) {
                pair curr = q.remove();  // Remove the front node from the queue
                int col = curr.col;      // Get the column index of the current node
                Node node = curr.n;      // Get the current node
                
                // Update the TreeMap with the current node's data
                // This will replace any previous node's data at the same column index,
                // ensuring that the last node's data at each column is stored (bottom view)
                tm.put(col, node.data); //in this place we can just add the node also if we have intger node 
                
                // If the left child exists, enqueue it with the column index decreased by 1
                if (node.left != null) {
                    q.add(new pair(node.left, col - 1));
                }
                
                // If the right child exists, enqueue it with the column index increased by 1
                if (node.right != null) {
                    q.add(new pair(node.right, col + 1));
                }
            }
        }
        
        // Collect all the values from the TreeMap in order of their keys (column indices)
        for (int k : tm.keySet()) {
            arr.add(tm.get(k));  //if we have integer node then we have to use .data at the last i.e(arr.add(tm.get(k).data)
        }
        
        // Return the list containing the bottom view of the binary tree
        return arr;
    }
}
```

**Top view:-**
Same approach like buttom view but in this we have to just check whether the val for the col is exist or not if exist then don't add bcs we have to get the first val for each col
```
class Solution {
    // Function to return a list of nodes visible from the top view
    // from left to right in a Binary Tree.
    static ArrayList<Integer> topView(Node root) {
        // TreeMap to store the first node's data at each horizontal distance (column index)
        TreeMap<Integer, Integer> tm = new TreeMap<>();
        
        // ArrayList to store the final result which will contain the top view nodes
        ArrayList<Integer> ans = new ArrayList<>();
        
        // Queue to facilitate level-order traversal (BFS)
        // It will store pairs of nodes and their respective column index
        Queue<Pair> q = new LinkedList<>();
        
        // Start with the root node at column index 0
        q.add(new Pair(root, 0));
        
        // While there are nodes to process in the queue
        while (!q.isEmpty()) {
            // Remove the node from the front of the queue
            Pair curr = q.remove();
            int col = curr.col;   // Get the column index of the current node
            Node node = curr.n;   // Get the current node
            
            // If the column index is not already in the TreeMap, add it
            // This ensures that only the first (topmost) node at each column is stored
            if (!tm.containsKey(col)) {
                tm.put(col, node.data);
            }
            
            // If the left child exists, enqueue it with the column index decreased by 1
            if (node.left != null) {
                q.add(new Pair(node.left, col - 1));
            }
            
            // If the right child exists, enqueue it with the column index increased by 1
            if (node.right != null) {
                q.add(new Pair(node.right, col + 1));
            }
        }
        
        // Collect all the values from the TreeMap in order of their keys (column indices)
        for (int k : tm.keySet()) {
            ans.add(tm.get(k));
        }
        
        // Return the list containing the top view of the binary tree
        return ans;
    }

    // Helper class to store a node and its corresponding column index
    static class Pair {
        Node n;   // The node itself
        int col;  // The column index of the node
        
        // Constructor to initialize the Pair object
        public Pair(Node n, int col) {
            this.n = n;
            this.col = col;
        }
    }
}
```
**987. Vertical Order Traversal of a Binary Tree**
Approach:-
So this is very similar to the top view but with a small difference we have not return only the first column value for the particular horizontal distance
instead we have to return all value for the particular distance
So to handle this we will create a treemap with integer and ArrayList
integer is for horizontal distance and arrayList is for string all the value for the particular distance
now the catch is for horizontal distance we have to return value based on level like the first level val will come first 
so for that we will add a level of type int in Pair class and during returnnig the answer we have to sort it and based on that we have to return the ans

Simple Explanation:
Purpose of the Code: This code performs a vertical order traversal of a binary tree, where nodes are grouped by their horizontal distance from the root. Nodes that are on the same vertical line are then sorted by their level (depth), and if they share the same level, they are sorted by their value.

Pair Class:

Stores three things: the node, its horizontal distance from the root (hd), and its level in the tree (level).
TreeMap:

Used to group nodes by their horizontal distance (hd). Keys in TreeMap are naturally sorted, so the traversal order will be maintained.
Queue and Level Order Traversal:

The tree is traversed level by level using a queue. For each node, its horizontal distance and level are updated and stored in the TreeMap.
Sorting Nodes:

Within each horizontal distance, nodes are sorted first by their level, and then by their value if levels are the same.
Result Construction:

After sorting, the node values are extracted and added to the final result list, which is then returned as the output.
This approach ensures that the nodes are correctly ordered both horizontally and vertically in the final output.



```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    // A helper class to store the node, its horizontal distance, and its level
    static class Pair {
        int hd; // Horizontal distance from the root
        int level; // Level (depth) of the node
        TreeNode node; // The actual tree node
        
        public Pair(int hd, int level, TreeNode node) {
            this.hd = hd;
            this.level = level;
            this.node = node;
        }
    }
    
    public List<List<Integer>> verticalTraversal(TreeNode root) {
        // TreeMap to store nodes according to their horizontal distance (hd)
        TreeMap<Integer, List<Pair>> tm = new TreeMap<>();
        // Queue for level order traversal of the tree
        Queue<Pair> q = new LinkedList<>();
        // Start with the root node at horizontal distance 0 and level 0
        q.add(new Pair(0, 0, root));
        
        // Level order traversal of the tree
        while (!q.isEmpty()) {
            Pair curr = q.remove(); // Get the current node and its position
            int hd = curr.hd;
            int level = curr.level;
            TreeNode node = curr.node;
            
            // If the horizontal distance is encountered for the first time, create a list
            tm.putIfAbsent(hd, new ArrayList<>());
            // Add the current node to the list corresponding to its horizontal distance
            tm.get(hd).add(new Pair(hd, level, node));
            
            // If there is a left child, add it to the queue with hd-1 (left shift) and level+1
            if (node.left != null) {
                q.add(new Pair(hd - 1, level + 1, node.left));
            }
            // If there is a right child, add it to the queue with hd+1 (right shift) and level+1
            if (node.right != null) {
                q.add(new Pair(hd + 1, level + 1, node.right));
            }
        }
        
        // Prepare the final result list
        List<List<Integer>> ans = new LinkedList<>();
        
        // Process each horizontal distance (key) in the TreeMap
        for (List<Pair> entry : tm.values()) {
            // Sort the list of nodes first by their level, then by their value if levels are the same
            entry.sort((a, b) -> {
                if (a.level == b.level) {
                    return a.node.val - b.node.val; // If levels are the same, sort by value
                } else {
                    return a.level - b.level; // Otherwise, sort by level
                }
            });
            
            // Collect the sorted node values into a list
            List<Integer> sortedValues = new ArrayList<>();
            for (Pair p : entry) {
                sortedValues.add(p.node.val);
            }
            // Add this list to the final result
            ans.add(sortedValues);
        }
        
        // Return the final vertical order traversal result
        return ans;
    }
}
```
**Root to leaf Path:-**
Approach:-
Just make a ans array of arrayList and a current array whenever we encounter it is a leaf node add curr to answer and do normal traversal and when root node case hit just remove a element from the curr

```
class Solution {
    public static ArrayList<ArrayList<Integer>> Paths(Node root) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
        path(ans, new ArrayList<>(), root);
        return ans;
    }

    public static void path(ArrayList<ArrayList<Integer>> ans, ArrayList<Integer> curr, Node root) {
        // Base case: if the current node is null, return
        if (root == null) {
            return;
        }

        // Add the current node's data to the path
        curr.add(root.data);

        // If it's a leaf node, add the current path to the answer
        if (root.left == null && root.right == null) {
            ans.add(new ArrayList<>(curr));  // Add a copy of the current path
        } else {
            // Recur for the left and right subtrees
            path(ans, curr, root.left);
            path(ans, curr, root.right);
        }

        // Backtrack: remove the current node's data from the path
        curr.remove(curr.size() - 1);
    }
}
```



