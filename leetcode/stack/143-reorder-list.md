# 143. Reorder List
You are given the head of a singly linked-list. The list can be represented as:
L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

Example 1:
Input: head = [1,2,3,4]
Output: [1,4,2,3]

Example 2:
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]

Constraints:
The number of nodes in the list is in the range [1, 5 * 104].
1 <= Node.val <= 1000


## Solution

1. Create a deque and add each node into the deque. Poll out each node from the deque and reoder the sequence.

* Time Complexity: O(2n)
* Space Complexity: O(n)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public void reorderList(ListNode head) {
        Deque<ListNode> deque = new ArrayDeque<>();
        ListNode curr = head;
        // add original list into the deque list
        while(curr != null){
            deque.add(curr);
            curr = curr.next;
        }
    
        int i = 0;
        // poll out each node from deque and add the first and last node in deque in sequence
        while(!deque.isEmpty()){
            if(i % 2 == 0){
                head.next = deque.pollFirst();
            } else {
                head.next = deque.pollLast();
            }
            head = head.next;
            i++;
        }
        head.next = null;
    }
}
```