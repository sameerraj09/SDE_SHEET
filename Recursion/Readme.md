**Reverse a Stack:-**
Approach:- 
first we will make the stack empty using recursion so that we have each pop item store in the call stack 
After that we start pushing each item in the buttom of stack by a function pushButtom()
so pop all item till the stack get empty so the item which will pop first(topitem) will push first at buttom bcs of call stack 
in that manner we can reverse our stack
```
class Solution { 
    // This method reverses the stack
    static void reverse(Stack<Integer> s) { 
        // Base case: if the stack is empty, return
        if(s.isEmpty()){
            return;
        }

        // Pop the top element from the stack and store it in temp
        int temp = s.pop();

        // Recursively reverse the remaining stack
        reverse(s);

        // Add the popped element (temp) to the bottom of the reversed stack
        addButtom(s, temp);
    }

    // This method adds an element to the bottom of the stack
    public static void addButtom(Stack<Integer> s, int data) {
        // Base case: if the stack is empty, push the data and return
        if(s.isEmpty()){
            s.push(data);
            return;
        }

        // Pop the top element from the stack
        int top = s.pop();

        // Recursively call addButtom to reach the bottom of the stack
        addButtom(s, data);

        // After adding the data to the bottom, push the popped elements back onto the stack
        s.push(top);
    }
}
```
**Sort an array using recursion::-**

**Approach:**
Remove All Elements Using Recursion (func1):

Use a recursive function (func1) to pop all elements from the stack until it becomes empty.
This process will effectively empty the stack, preparing it for the next phase where elements will be inserted back in sorted order.
Insert Elements Back in Sorted Order (func2):

Use another recursive function (func2) to insert elements back into the stack in the correct order:
If the stack is empty, simply push the element.
If the top element of the stack is less than the current element to be added, push the current element onto the stack.
If the top element is greater than the current element,
pop the top element and recursively call func2 to find the correct position for the current element.
Once the correct position is found, push the previously popped elements back onto the stack in order.
```
class GfG {
    // Method to sort the stack
    public Stack<Integer> sort(Stack<Integer> s) {
        func1(s); // Initiate the sorting process
        return s; // Return the sorted stack
    }

    // Recursive function to sort the stack
    public void func1(Stack<Integer> s) {
        // Base case: If the stack is empty, return
        if(s.isEmpty()) {
           return; 
        }

        // Pop the top element and store it in variable a
        int a = s.pop();

        // Recursively sort the remaining stack
        func1(s);

        // Insert the popped element in its correct position in the sorted stack
        func2(s, a);
    }

    // Helper function to insert an element in a sorted stack
    public void func2(Stack<Integer> s, int add) {
        // Base case: If the stack is empty, push the element and return
        if(s.isEmpty()) {
            s.push(add);
            return;
        }

        // If the top element of the stack is smaller than the element to be added
        else if(s.peek() < add) {
            s.push(add); // Push the element directly onto the stack
        } 
        // If the top element is larger, remove it and recurse to find the correct position
        else {
            int top = s.pop(); // Pop the top element
            func2(s, add); // Recursively call func2 to insert the element in its correct position
            s.push(top); // Push the previously popped elements back onto the stack
        }
    }
}
```
**50: pow(x,n)**
```
class Solution {
    // Method to calculate x raised to the power n (x^n)
    public double myPow(double x, int n) {
        // Base case: If exponent n is 0, return 1 (since any number to the power of 0 is 1)
        if(n == 0) return 1;

        // Special case: Handle the edge case where x = 2 and n is the minimum integer value (overflow case)
        if(x == 2 && n == -2147483648) return 0;

        // If n is negative, make it positive and invert x (1/x)
        if(n < 0) {
            n = -n;
            x = 1 / x;
        }

        // If n is even, use the property (x^n = (x*x)^(n/2)) to reduce the problem size
        if(n % 2 == 0) {
            return myPow(x * x, n / 2);   // Example: 7^4 => (7*7)^2
        }
        // If n is odd, multiply x by the result of myPow with n-1
        else {
            return x * myPow(x, n - 1);   // Example: 7^3 => 7 * 7^2
        }
    }
}
```

