# Leetcode day3  141. Linked List Cycle 
## Description

> Given a linked list, determine if it has a cycle in it.
> To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.


	Input: head = [3,2,0,-4], pos = 1
	Output: true
	Explanation: There is a cycle in the linked list, where tail connects to the second node.
![](%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-04-02%2018.21.51.png)
### Python3:
using Hash table
class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        dic = {}
        while head:
            if head in dic:
                return True
        
            dic[head] = 0
            head = head.next
        return False

### C++:
using TWO POINTERS
class Solution {
public:
    bool hasCycle(ListNode *head) {        
        auto fast = head;
        auto slow = head;
        
        while (fast && fast->next) {
            fast = fast->next->next;
            slow = slow->next;
            
            if (fast == slow)
                return true;
        }
        
        return false;
    }
};
