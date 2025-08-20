### Name: Vivian Richard Demello
### Section: A1
### Roll No: 2

## Q.7: Program to solve the Lemonade Stand Change Challenge

We are given a list of notes `[5, 10, 20]` of money paid by customers, find if it's possible to provide the correct change for all customers when each lemonade costs $5.

### Complexity:
**Time Complexity: O(N)**  
Iteration through list of notes once takes O(N) complexity  

**Space Complexity: O(1)**  
Counters for 5 and 10 dollar notes

### Algorithm:

Algorithm: Lemonade Stand Change(notes[]):

1.  Initialize counters for $5 and $10 notes to zero
2.  Iterate through each note from the customers
3.  If the note is $5, accept it and increment the count of $5 notes
4.  If the note is $10 we give $5 change. If we have at least one $5 note we use it and increment the count of $10 notes. If not, return false.
5.  If the note is $20 we must give $15 change. Prioritize using a $10 and a $5 note to save smaller notes
    *   If we have a $10 and a $5 we use them
    *   Otherwise, if you have at least three $5 note we use them
    *   If neither option is possible, you cannot make change, so return false
6.  If you successfully pass all customers then return true.

**Example:** `notes = {5, 5, 10, 10, 20}`

**Output:** false  
After serving the first four customers, we will have two $10 notes but no $5 notes. You cannot provide the required $15 change for the $20 note.

### C++ Code:

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool lemonadeChange(vector<int>& notes) {
    int five_count = 0;
    int ten_count = 0;

    for (int note : notes) {
        if (note == 5) {
            five_count++;
        } 
        
        else if (note == 10) {
            if (five_count > 0) {
                five_count--;
                ten_count++;
            } 
            
            else {
                return false;
            }
        } 
        
        else {
            if (ten_count > 0 && five_count > 0) {
                ten_count--;
                five_count--;
            } 
            
            else if (five_count >= 3) {
                five_count -= 3;
            } 
            
            else {
                return false;
            }
        }
    }
    return true;
}

int main() {
    vector<int> notes = {5, 5, 10, 10, 20};
    
    cout << (lemonadeChange(notes) ? "true" : "false") << endl;
}
```