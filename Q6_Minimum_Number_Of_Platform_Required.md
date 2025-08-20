### Name: Vivian Richard Demello
### Section: A1
### Roll No: 2

## Q.6: Program to find out Minimum number of platforms required for running trains

When we are given arrival and departure timings of trains we need to find the minimum number of platforms so that trains don't have to wait for space anytime

### Complexity:
Time Complexity: O(N log N)  
Sorting the arrival and departure arrays takes O(N log N) time, which is the dominant operation.

Space Complexity: O(1)  
No extra space proportional to the input size is used; only a few variables are needed for pointers and counters.

### Algorithm:

Algorithm: Minimum number of platforms required for running trains(ArrivalTime[], DepartureTime[]):

1.  Sort the ArrivalTime and DepartureTime lists
2.  Use two pointers, i for arrivals and j for departures, to iterate through the sorted lists
3.  If the next arrival time is earlier than or equal to the next departure time increment the platform count and increment the arrival pointer `i`
4.  If the next departure time is earlier decrement the platform count and increment the departure pointer `j`
5.  Maximum platform count will be the final answer

Example: ArrivalTime = {900, 940, 950, 1100, 1500, 1800}  
         DepartureTime = {910, 1200, 1120, 1130, 1900, 2000}

Output: 3  

At the peak time (11:00), three trains are at the station at same time, so 3 platforms are required

### C++ Code:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int findMinPlatforms(vector<int>& ArrivalTime, vector<int>& DepartureTime) {
    int n = ArrivalTime.size();
    if (n == 0) {
        return 0;
    }

    sort(ArrivalTime.begin(), ArrivalTime.end());
    sort(DepartureTime.begin(), DepartureTime.end());

    int platforms_needed = 1;
    int max_platforms = 1;
    int i = 1;
    int j = 0;

    while (i < n && j < n) {
        if (ArrivalTime[i] <= DepartureTime[j]) {
            platforms_needed++;
            i++;
        } 
        
        else {
            platforms_needed--;
            j++;
        }
        max_platforms = max(max_platforms, platforms_needed);
    }

    return max_platforms;
}

int main() {
    vector<int> arrivals = {900, 940, 950, 1100, 1500, 1800};
    vector<int> departures = {910, 1200, 1120, 1130, 1900, 2000};
    
    cout << "Minimum platforms required: " << findMinPlatforms(arrivals, departures) << endl; 
    return 0;
}
```