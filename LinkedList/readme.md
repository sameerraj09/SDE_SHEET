**206:-Reverse A linked List**
Three variable and four step

```
  public ListNode reverseList(ListNode head) {

  // we need three variable and 4 step
    ListNode prev = null;
    ListNode curr = head;
    ListNode next;
    while(curr!=null){
     next = curr.next;
     curr.next = prev; //reverse the prder
     prev = curr;
     curr = next;
    }
    return prev;

 } 
```
** 876:- Find middle element of linked list **
 slow fast approach 
 ```
   public ListNode middleNode(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while(fast!=null && fast.next!=null){
            slow=slow.next;
            fast = fast.next.next;
        }
        return slow;  
    }
```

**    21. Merge Two Sorted Lists**
we have to create a dummy linked list then we have to compare the value of given two linked based upon that
we have to assing the next of dummy to that node and at last which ever is left just point the next of dummy to it
```
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(-1);
        ListNode temp1 = list1;
        ListNode temp2 = list2;
        ListNode temp3 = dummy;
        while(temp1!=null && temp2!=null){
            if(temp1.val<=temp2.val){
               temp3.next  = temp1;
               temp1 = temp1.next;
            }
            else if(temp1.val>temp2.val){
                temp3.next = temp2;
                temp2 = temp2.next;
            }
              temp3 = temp3.next;
        } 
            while(temp1!=null){
                temp3.next = temp1;
                temp1=temp1.next;
                temp3= temp3.next;
            }
            while(temp2!=null){
                temp3.next =temp2;
                temp2 = temp2.next;
                temp3= temp3.next;
            }
        return dummy.next;
}
}
```
**19. Remove Nth Node From End of List**
Approach:-
first find the size of the linked list
then run a loop till the size-n-1
after that make the curr.next = curr.next.next
Code:- 

```
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
     //first find the size of the linked list
     ListNode temp = head;
     int count = 0;
     while(temp!=null){
        count++;
        temp = temp.next;
     }
     if(count==n) return head.next; //if we have to remove the nth element from last and that is equal to the size means remove head
     ListNode curr = head;
     for(int i = 0;i<count-n-1;i++){
        curr = curr.next;
     }
     //now we are on one prev node which we have to delete 
     //just make curr.next = curr.next.next
     curr.next = curr.next.next;
        
        return head;
    }
}
```

**2 Add two No**
Approach:-
first make a dummy node where we will store the sum
now make three node pointing on head of each linked list
initialize carry  = 0;
find the sum i.e sum = temp1.val+temp2.val+temp3.vall
before finding val just make sure the Linked list are not empty
fint the carry after adding and digit also which we have to add my modulo 
then make a new node and point next of dummy to it

```
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // Dummy node to form the result list
        ListNode dummy = new ListNode(-1);
        // Pointer to the current node in the result list
        ListNode current = dummy;
        // Pointers to traverse l1 and l2
        ListNode temp1 = l1;
        ListNode temp2 = l2;
        // Carry to handle sums greater than 10
        int carry = 0;   
        // Loop until both lists are fully traversed
        while (temp1 != null || temp2 != null) {
            // Get the values from temp1 and temp2, or 0 if the node is null
            int val1 = (temp1 != null) ? temp1.val : 0;
            int val2 = (temp2 != null) ? temp2.val : 0;
            // Calculate the sum of the values and the carry
            int sum = val1 + val2 + carry;
            // Update carry for the next iteration
            carry = sum / 10;
            // Calculate the current digit to store in the node
            int digit = sum % 10;      
           // Create a new node with the current digit and append it to the result list
            current.next = new ListNode(digit);
            // Move the current pointer to the next node
            current = current.next;
            // Move temp1 and temp2 pointers to their next nodes if they exist
            if (temp1 != null) temp1 = temp1.next;
            if (temp2 != null) temp2 = temp2.next;
        }
        // If there's a carry left after the final addition, add a new node with the carry
        if (carry > 0) {
            current.next = new ListNode(carry);
        }
        // Return the head of the resultant list (next node of the dummy)
        return dummy.next;
    }
}
```

**237: Delete node in LinkedList**

for deleting any value we have to make the prev.next = prev.next.next but in our case only node is given we will store the value of next node to node and delete the next
```
class Solution {
    public void deleteNode(ListNode node) {
        node.val = node.next.val;  //store the value of next node in the node and delete next node    
        node.next = node.next.next;
    }
}
```



