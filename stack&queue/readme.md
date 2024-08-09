

**Stack using Array:-**
Approach:- add element at the last of array and increment the top after addding during pop remove get element from the top poisition and -- the top
```
class MyStack {
    private int[] arr;
    private int top;

    public MyStack() {
        arr = new int[1000];
        top = -1;
    }


    public void push(int x) {
        
        // Your Code
      arr[++top] = x;
   //   top++;
        
        
    }

    public int pop() {
        // Your Code
        if(top==-1) return top;
                int get  = arr[top--];
       // top--;
        return get;
        
    }
}

```

**Queue using array:-**
Approach:- During adding increase the rear and add that place
           during removal remove from rear and ++;
```
  class MyQueue {

    int front, rear;
	int arr[] = new int[100005];

    MyQueue()
	{
		front=0;
		rear=0;
	}
	
	//Function to push an element x in a queue.
	void push(int x)
	{
	    arr[rear] = x;
	    rear++;
	    
	    // Your code here
	} 

    //Function to pop an element from queue and return that element.
	int pop()
	{
	    if(front==rear) return -1;
	    int get = arr[front];
	    front++;
	    return get;
		// Your code here
	} 
}
```
**
225. Implement Stack using Queues**
Approach:- We will use two queue for this and then when we have to add the element we will remove all the element from q1 and put in the another queue q2 
and once we will add that element in the q1 this will maintaion order
```
class MyStack {
Queue <Integer> q1 = new LinkedList<>();
        Queue <Integer> q2 = new LinkedList<>();
    public MyStack() {
        this.q1 = q1;
        this.q2 = q2;
    }
    
    public void push(int x) {
        if(q1.isEmpty()){
            q1.add(x);
        }
        else{
            while(!q1.isEmpty()){
                q2.add(q1.remove());
            }
            q1.add(x);
            while(!q2.isEmpty()){
                q1.add(q2.remove());
            }
        }

        
    }
    
    public int pop() {
    return q1.remove();
    }
    
    public int top() {
        return q1.peek();
    }
    
    public boolean empty() {
        return q1.isEmpty();
    }
}
```
225:-Queue using Stack
Same approach just use stack in place of queue(previous code)
```
class MyQueue {
    Stack<Integer> s1 = new Stack<>();
    Stack<Integer> s2 = new Stack<>();
    public MyQueue() {
        this.s1 = s1;
        this.s2 = s2;
    }
    
    public void push(int x) {
      if(s1.isEmpty()){
        s1.push(x);
      }
      else{
        while(!s1.isEmpty()){
            s2.push(s1.pop());
        }
        s1.push(x);
        while(!s2.isEmpty()){
            s1.push(s2.pop());
        }
      }
        
    }
    
    public int pop() {
        return s1.pop();
    }
    
    public int peek() {
        return s1.peek();
    }
    
    public boolean empty() {
        return s1.isEmpty();
    }
}

```


**Approach 1 **
check the top of stack for all closing paranthesis
if we got the opening for that continue and keek doing if not return false
else if it a copening paranthesis just push it 
at last chack whether stack is empty or not

**Approach 2**

```
class Solution {
    public boolean isValid(String s) {
        Stack<Character> s1 = new Stack<>();
        for (char c : s.toCharArray()) {
            // now if we will get open brackets we will push the close else we will check
            // the char with the top and return
            // the result effectively
            if (c == '(') s1.push(')');
                
            else if (c == '{')  s1.push('}');
               
            else if (c == '[')  s1.push(']');
               
            else {
                if(s1.isEmpty()) return false;
                char top = s1.pop();
                if (top != c) {
                    return false;
                }
            }

        }
        return s1.isEmpty();
    }
}
```
