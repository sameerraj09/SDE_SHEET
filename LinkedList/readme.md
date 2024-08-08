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
        if (carry > 0) {l
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
**160. Intersection of Two Linked Lists**
Approach:- We will find the count of both linked list and we will taverse till both come on same length after that the moment they have same value we will return it

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode(int x) {
 * val = x;
 * next = null;
 * }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode curr1 = headA;
        ListNode curr2 = headB;
        int count1 = 0;
        int count2 = 0;
        // pehle linked list 1 ke number of elements rkhliye
        while (curr1 != null) {
            curr1 = curr1.next;
            count1++;
        }
        // fir linked list 2 ke number of elements rkhliye
        while (curr2 != null) {
            curr2 = curr2.next;
            count2++;
        }
        // dono me same number of elements bache ho, wahan tk traverse krwado

        // agr linkedlist1 me zyada elements hai to aage bdhao tbtk, jbtk remaining
        // elements, linkedlist2 ke total elements ke count ke barabar ho
        while (count1 > count2) {
            headA = headA.next;
            count1--;
        }
        // agr linkedlist2 me zyada elements hai to aage bdhao tbtk, jbtk remaining
        // elements, linkedlist1 ke total elements ke count ke barabar ho
        while (count1 < count2) {
            headB = headB.next;
            count2--;
        }
        // ab dono list me same number of remaining elements hai, to headA aur headB
        // dono ko aage bdhaate rho, jbtk same na aaye.
        while (headA != headB) {
            headA = headA.next;
            headB = headB.next;
        }
        // jese hi same aaye, return krdo
        return headB;

    }
}
another approach
// ListNode A = headA;
// ListNode B = headB;
// while(A!=B){

// if(A==null) A=headB;
// else A = A.next;
// if(B==null) B=headA;
// else B = B.next;

// }
// return A;

```

**141. Linked List Cycle**
Approach:- slow fast pointer if slow == fast return true else return false
```
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = fast;
        while(fast!=null &&fast.next!=null){
            slow =  slow.next;
            fast = fast.next.next;
            if(slow==fast) return true;
        }
        return false;
        
    }
}
```
**Hard**
**25. Reverse Nodes in k-Group**
```
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        // Edge cases: if the list is empty or k is less than or equal to 1, return the head as-is.
        if (head == null || k <= 1) return head;

        // Step 1: Calculate the length of the list
        int length = 0;
        ListNode current = head;
        // Traverse the list to determine its length.
        while (current != null) {
            length++;
            current = current.next;
        }

        // Step 2: Reverse in groups of k
        // Create a dummy node to make it easier to manipulate the head of the list.
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        
        // This pointer keeps track of the end of the previous group of reversed nodes.
        ListNode prevGroupEnd = dummy;
        
        // This pointer marks the start of the current group to be reversed.
        ListNode groupStart = head;

        // Continue reversing groups as long as there are at least k nodes left.
        while (length >= k) {
            // Initialize pointers for reversing the current group.
            ListNode prev = null;
            ListNode curr = groupStart;
            
            // Reverse the next k nodes.
            for (int i = 0; i < k; i++) {
                ListNode nextNode = curr.next;
                curr.next = prev;
                prev = curr;
                curr = nextNode;
            }
            
            // After reversing, connect the end of the previous group to the start of the newly reversed group.
            prevGroupEnd.next = prev;
            
            // Connect the end of the newly reversed group to the next part of the list.
            groupStart.next = curr;
            
            // Move the prevGroupEnd pointer to the end of the newly reversed group.
            prevGroupEnd = groupStart;
            
            // Move to the next group.
            groupStart = curr;
            
            // Decrease the length by k, since we have processed k nodes.
            length -= k;
        }

        // The dummy node's next pointer now points to the head of the modified list.
        return dummy.next;
    }
}
```
**234. Palindrome Linked List**
Approach:-
Sabse pehle LL ke middle tak jayenge for usko ulta kar ke ek nayi linkes list me daal denge aur fir compare kar lenge jaise unequal mile false return kar denge

```
Approach thoda lendi hai but achha hai

class Solution {
    public boolean isPalindrome(ListNode head) {
        int count = size(head);
        int target = count/2;
        int i = 0;
        ListNode curr = head;
        while(i<target){
         curr=curr.next;
         i++;
        }
        //now my current is on target where we have to reverse the element
        ListNode dummy = new ListNode(-1);
      dummy.next = rev(curr);

        ListNode curr1 = head;
        ListNode curr2 = dummy.next;
        while(curr1!=null && curr2!=null){
            if(curr1.val!=curr2.val) return false;
            curr1 = curr1.next;
            curr2 = curr2.next;
        }
        return true;

        
    }
    public int size(ListNode head){
        ListNode curr = head;
        int count = 0;
        while(curr!=null){
            count++;
            curr = curr.next;
        }
        return count;
    }
    public ListNode rev(ListNode head){
        ListNode curr = head;
        ListNode prev = null;
        ListNode next;
        while(curr!=null){
               next = curr.next;
               curr.next = prev;
               prev = curr;
               curr = next;
        }
        return prev;
    }
}
```

**LinkedList Cycle 2**
Approach:-  slow fast
we will try to find the point where both meet 
after that we will reset any one and put it on head and run both by one unit the place where both meet after that is the loop node

```
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if(head==null ||head.next==null) return null;
        ListNode slow = head;
        ListNode fast = head;
        while(fast!=null &&fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow==fast){
                fast = head;
                while(slow!=fast){
                    slow = slow.next;
                    fast = fast.next;
                }
                return slow;
            }
        }
       
       return null;
        
        
    }
}
```


