### Name: Vivian Richard Demello
### Section: A1
### Roll No: 2


## Q.2: Program to find majority element from an array using Moore Voting Algorithm  

#### Map does not allow Duplicate Keys  

### Complexity:
1. Insertion: O(1)
In average case insertion of element happens in constant time in map
2. Deletion: O(1)
In average case deletion of element happens in constant time in map
3. Lookup: O(1)
In average case looking up an element in map takes constant time 

## Implementation in C++:  

C++ allows Unordered or Ordered Maps:  

### 1. Unordered Map  
In Unordered Map the order in which Key-Value pairs are inserted is not maintained.   

```cpp
#include<iostream>
#include<unordered_map>
using namespace std;

int main(void) {
	unordered_map<string, int>scores_map = {
		{"Vivian", 90},
		{"Shardul", 93},
		{"Adarsh", 95}
	};
	
	for (auto i : scores_map) {
		cout << "Name: " << i.first << " ";
		cout << "Score: " << i.second << endl;
	}
	
	cout << "Name: " << scores_map["Vivian"] << endl;
}
```

Output:   

Order of insertion is not followed  
```
Name: Shardul Score: 93  
Name: Adarsh Score: 95  
Name: Vivian Scores: 90  
```

### 1. Ordered Map 
In Ordered Map the order in which Key-Value pairs are inserted is maintained.  

```cpp
#include<iostream>
#include<map>
using namespace std;

int main(void) {
	map<string, int>scores_map;
	
	scores_map.insert({"Vivian", 19});
	scores_map.insert({"Shardul", 19});

	for (auto i : scores_map) {
		cout << "Name: " << i.first << endl;
		cout << "Score: " << i.second << endl;
	}
}
```

Output:  

Order of insertion is followed  
```
Name: Vivian Score: 90  
Name: Shardul Scores: 93  
Name: Adarsh Score: 95  
```