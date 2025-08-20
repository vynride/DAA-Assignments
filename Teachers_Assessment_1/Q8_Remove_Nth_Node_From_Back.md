### Name: Vivian Richard Demello
### Section: A1
### Roll No: 2

## Q.8: Program to remove the Nth Node from the End of a Linked List

We are given the head of a linked list, we have to remove the nth node from the end of the list and return the head of the list.

### Complexity:
**Time Complexity: O(N)**  
We only iterate the list once to find the node

**Space Complexity: O(1)**  
We only use two pointers, so the memory used is constant

### Algorithm:

Algorithm: Remove Lth Node from End (head, l):  

1. We'll use two pointer method, a fast one and a slow one
2. We first let the fast pointer get a head start by moving it l steps into the list
3. Now we move both the fast and slow pointers forward one step at a time. But the fast pointer will always stay l steps ahead of the slow one
4. When the fast pointer reaches the very end of the list, the slow pointer will be exactly at the node right before the one we want to delete
5. We then remove the node from the list

**Example:** `head = [1,2,3,4,5]`, `n = 2`

**Output:** `[1,2,3,5]`  
The 2nd node from the end is `4`. The algorithm finds node `3` and makes it point directly to `5`, skipping `4`  

### C++ Code:

```cpp
#include <iostream>
#include <vector>

using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    
	ListNode(int x) {
	    val = x;
	    next = nullptr;
	}
};

ListNode *removeNthFromEnd(ListNode* head, int n) {
    ListNode *fast = head;
    ListNode *slow = head;

    for (int i = 0; i < n; ++i) {
        fast = fast->next;
    }

    if (fast == nullptr) {
        return head->next;
    }

    while (fast->next != nullptr) {
        fast = fast->next;
        slow = slow->next;
    }

    slow->next = slow->next->next;
    
    return head;
}

void printList(ListNode* head) {
    while (head != nullptr) {
        cout << head->val << " -> ";
        head = head->next;
    }
    cout << "NULL" << endl;
}

int main() {
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);
    
    int n = 2;
    
    head = removeNthFromEnd(head, n);
    
    printList(head);
}
```