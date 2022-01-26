# Swap Nodes in Pairs Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/swap-nodes-in-pairs/

## Problem Description

*The description of the "Swap Nodes in Pairs" problem is as follows:*

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

**Example 1:**

*Note: This example in Leetcode also includes a visual representation of the input and expected output. Please use the link referenced above to view the problem in Leetcode and find the accompanying image for this example.*

```
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```

**Example 2:**

```
Input: head = []
Output: []
```

**Example 3:**

```
Input: head = [1]
Output: [1]
```

**Constraints**

- The number of nodes in the list is in the range `[0, 100]`.
- `0 <= Node.val <= 100`

## Solution

Below is my working solution for the problem in Leetcode:

```
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
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        ListNode headSwapped = head.next;
        ListNode first = head;
        ListNode second = head.next;
        ListNode prevConnector = new ListNode(0, head);
        while(first != null && second != null){
            prevConnector.next = second;
            ListNode temp = second.next;
            first.next = temp;
            second.next = first;
            prevConnector = first;
            if(temp == null){
                return headSwapped;
            }
            first = temp;
            second = first.next;
        }
        return headSwapped;
        
    }
}
```
This solution has a runtime of approximately less than 1 ms and a memory usage of approximately 36-39MB. 
