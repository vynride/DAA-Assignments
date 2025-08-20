### Name: Vivian Richard Demello
### Section: A1
### Roll No: 2


## Q.3: Program to detect a loop in linked list  

A loop in a linked list means one node in the list is connected back to another node in the list.

To detect this loop we can use a slow pointer and fast pointer approach

### Complexity:
Time Complexity: O(N)   
In worst case we need to iterate over array completely and no loop is found  
Space Complexity: O(1)  
No extra space is needed apart from 2 pointers for list  

### Algorithm:

Algorithm: Finding Loop in Linked List (Linked List Head):

1. Loop over linked list using two pointers one fast and one slow
2. Move slow pointer by one step and fast pointer by two steps
3. If these pointers meet at the same node then there is a loop in the list
4. If pointers do not meet then the linked list doesn't have a loop

Example: 1=>2=>3=>4=>5  
			   |	 |   
			   <=7 <=6  
  
1. First we set slow pointer and fast pointer to 1
2. In next iteration slow pointer => 2 & fast pointer => 3
3. Then, slow pointer => 3 & fast pointer => 5
4. Then, slow pointer => 4 & fast pointer => 7
5. Then, slow pointer => 5 & fast pointer => 4
6. Then, slow pointer => 6 & fast pointer => 6
7. As both slow and fast pointer point at same node there is a loop in the linked list


### C++ Code:

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

class ListNode {
public:
    int value;
    ListNode* next;

    ListNode(int val) {
        value = val;
        next = nullptr;
    }
};

bool hasCycle(ListNode* head) {
    unordered_set<ListNode*> visitedNodes;

    while (head != nullptr) {
        if (visitedNodes.count(head))
            return true;

        visitedNodes.insert(head);
        head = head->next;
    }

    return false;
}

int main() {
    ListNode* node1 = new ListNode(1);
    ListNode* node2 = new ListNode(2);
    ListNode* node3 = new ListNode(3);
    ListNode* node4 = new ListNode(4);
    ListNode* node5 = new ListNode(5);
    ListNode* node6 = new ListNode(6);
    ListNode* node7 = new ListNode(7);

    node1->next = node2;
    node2->next = node3;
    node3->next = node4;
    node4->next = node5;
    node5->next = node6;
    node6->next = node7;
    node7->next = node3; 
    
    cout << (hasCycle(node1) ? "true" : "false") << endl;
}
```