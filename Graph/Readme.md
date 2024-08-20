Notes:-
The maximum number of edges in an undirected graph is n(n-1)/2 and obviously in a directed graph there are twice as many. 
If the graph is not a multi graph then it is clearly n * (n - 1), as each node can at most have edges to every other node

**Important Note:-**
For n nodes we have  n(n-1)/2 edges now the total no of possible undirectd graph will be sum of combination of each edge i.e no edge connected ec0 +ec1(1 edge connected) + ec2 (two edge connecte....ecn 
There are a total of 2^(n*(n-1)/2) possible graphs that can be constructed using the n vertices.(sum of all combination)

Q Given an integer n representing number of vertices. Find out how many undirected graphs (not necessarily connected) can be constructed out of a given n number of vertices.
```
class Solution {
    static long count(int n) {
    // code here
    return (long)Math.pow(2,n+1);

  }
}
```
Given an undirected graph with V nodes and E edges, create and return an adjacency list of the graph. 0-based indexing is followed everywhere.
Approach:-
Aceess each elemnt of matrix and put the dest val in src place in ans arraylist(iski biwi uske sath)
```
class Solution {
    public List<List<Integer>> printGraph(int V, int edges[][]) {
        
        List<List<Integer>> ans = new ArrayList<>(); // Create a list of lists to store the adjacency list
        for(int i = 0; i < V; i++){
            ans.add(new ArrayList<>());  // Add an empty list for each vertex
        }
        for(int[] arr : edges){
            int a = arr[0];  // Get the start vertex of the edge
            int b = arr[1];  // Get the end vertex of the edge
            ans.get(a).add(b); // Add the end vertex to the start vertex's adjacency list
            ans.get(b).add(a); // Add the start vertex to the end vertex's adjacency list (since it's an undirected graph)
        }
        return ans; // Return the adjacency list
    }
}
```
**BFS:-**
Approach:-
Queue me src ko add karo aur loop chala do jab tak loop khali nahi ho jata 
ek boolean arr banao jo vis ho gaya usko true kardo
aur harek ke dest ko add karte jao q me
```
class Solution {
    // Function to return Breadth First Traversal of the given graph.
    public ArrayList<Integer> bfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        // List to store the BFS result
        ArrayList<Integer> ans = new ArrayList<>();
        
        // Queue to manage the BFS process
        Queue<Integer> q = new LinkedList<>();
        
        // Array to keep track of visited nodes
        boolean vis[] = new boolean[V];
        
        // Start BFS from node 0
        q.add(0);
        vis[0] = true; // Mark node 0 as visited
        
        // While there are nodes to process in the queue
        while (!q.isEmpty()) {
            int curr = q.remove(); // Get the current node from the queue
            ans.add(curr); // Add the current node to the BFS result
            
            // Check all the neighbors of the current node
            for (int i = 0; i < adj.get(curr).size(); i++) {
                int dest = adj.get(curr).get(i); // Get the neighbor node
                
                // If the neighbor hasn't been visited yet
                if (!vis[dest]) {
                    vis[dest] = true; // Mark it as visited
                    q.add(dest); // Add it to the queue for processing
                }
            }
        }
        
        // Return the final BFS result
        return ans;  
    }
}
```
**DFS:-**
Approach:-
Sure, here’s the approach explained in English:

1. **Setting Up DFS**:
   - First, we create a boolean array `vis[]` to keep track of which nodes have been visited.
   - We then create an ArrayList called `ans` to store the result of our DFS traversal.
   - We start the traversal from node `0`, mark it as visited, and add it to the `ans` list.

2. **Traversing Using Recursion**:
   - We define a `helper` function that will handle the DFS traversal using recursion.
   - For the current node, we check all its neighbors. If a neighbor hasn’t been visited yet, we visit it, add it to `ans`, and then recursively call the `helper` function for that neighbor.

3. **Base Logic**:
   - The recursion continues until all neighbors are visited. Once no more nodes are left to visit, the recursion ends, and we have our complete DFS result in `ans`.

4. **Final Output**:
   - Finally, the `ans` list, which contains the full DFS sequence, is returned.
```
class Solution {
    // Function to return a list containing the DFS traversal of the graph.
    public ArrayList<Integer> dfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        // Array to keep track of visited nodes
        boolean vis[] = new boolean[V];
        
        // List to store the DFS result
        ArrayList<Integer> ans = new ArrayList<>();
        
        // Start DFS from node 0
        ans.add(0);
        vis[0] = true; // Mark node 0 as visited
        
        // Call the helper function to perform DFS
        return helper(adj, 0, vis, ans);
    }
    
    // Helper function to perform DFS recursively
    public ArrayList<Integer> helper(ArrayList<ArrayList<Integer>> adj, int curr, boolean vis[], ArrayList<Integer> ans) {
        
        // Traverse all the neighbors of the current node
        for (int i = 0; i < adj.get(curr).size(); i++) {
            int dest = adj.get(curr).get(i); // Get the neighbor node
            
            // If the neighbor hasn't been visited yet
            if (!vis[dest]) {
                vis[dest] = true; // Mark it as visited
                ans.add(dest); // Add it to the DFS result
                
                // Recursively perform DFS on the neighbor
                helper(adj, dest, vis, ans);
            }
        }
        
        // Return the final DFS result
        return ans;
    }
}
```
