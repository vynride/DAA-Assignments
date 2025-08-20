### Name: Vivian Richard Demello
### Section: A1
### Roll No: 2

## Q.5: Program for Flattening a Linked List

We are given a linked list where each node has a `next` pointer (to the right) and a `bottom` pointer (downwards), and "bottom" list is sorted. We have to flatten the entire list into a single sorted list

### Complexity:
**Time Complexity: O(N * K)**  
Where N is the average number of nodes in a vertical list and K is the number of vertical lists. We merge each list one by one

**Space Complexity: O(K)**  
This is due to the recursion which will go as deep as the number of lists

### Algorithm:

Algorithm: Flatten a Linked List (head):

1.  The problem is just merging the first vertical list with the flattened version of all the other lists
2.  If we have only one list left (or none), it's already "flat," so we're done so we return it
3.  If not we ask our function to first go and flatten the rest of the list
4.  Now we have two perfectly sorted lists: the first list (`head`) and the flattened result of the rest (`head->next`). We just need to merge these two together.
5.  We compare the top nodes of both lists, pick the smaller one, and attach it to our final list. We keep repeating until all nodes are used

**Example:**

```
5 -> 10 -> 19 -> 28
|    |     |     |
7    20    22    35
|          |     |
8          50    40
|                |
30               45
```

**Output:** `5 -> 7 -> 8 -> 10 -> 19 -> 20 -> 22 -> 28 -> 30 -> 35 -> 40 -> 45 -> 50`

### C++ Code:

```cpp
#include <iostream>

using namespace std;

struct Node {
    int data;
    Node *next;
    Node *bottom;

    Node(int x) {
        data = x;
        next = nullptr;
        bottom = nullptr;
    }
};

Node* mergeTwoLists(Node* a, Node* b) {
    if (a == nullptr) 
    	return b;
    	
    if (b == nullptr) 
    	return a;

    Node* result;

    if (a->data < b->data) {
        result = a;
        result->bottom = mergeTwoLists(a->bottom, b);
    } 
    
    else {
        result = b;
        result->bottom = mergeTwoLists(a, b->bottom);
    }
    
    result->next = nullptr;
    return result;
}

Node* flatten(Node* root) {
    if (root == nullptr || root->next == nullptr) {
        return root;
    }

    root->next = flatten(root->next);

    root = mergeTwoLists(root, root->next);

    return root;
}

void printList(Node* node) {
    while (node != nullptr) {
        cout << node->data << " -> ";
        node = node->bottom;
    }
    cout << "NULL" << endl;
}

int main() {
    Node* head = new Node(5);
    head->next = new Node(10);
    head->next->next = new Node(19);
    head->next->next->next = new Node(28);

    head->bottom = new Node(7);
    head->bottom->bottom = new Node(8);
    head->bottom->bottom->bottom = new Node(30);

    head->next->bottom = new Node(20);

    head->next->next->bottom = new Node(22);
    head->next->next->bottom->bottom = new Node(50);

    head->next->next->next->bottom = new Node(35);
    head->next->next->next->bottom->bottom = new Node(40);
    head->next->next->next->bottom->bottom->bottom = new Node(45);
    
    Node* flattenedList = flatten(head);
    
    printList(flattenedList);
}
```