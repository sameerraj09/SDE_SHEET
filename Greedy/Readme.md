**N meetings in one room**
Approach:-
we will create a arraylist of array and store start and end value of each meeting slot.
After that we have to sort the Arraylist of Array on the basis of end time of meeting
Now we will check the start time of each meeting with the previous end time it it is greater then meeting can be held not and overlapping meeting
and do count++ ,and update the lasttime
and then return
```
import java.util.*;

class Solution {
    // Function to find the maximum number of meetings that can
    // be performed in a meeting room.
    public int maxMeetings(int n, int start[], int end[]) {
        // Create an ArrayList of arrays to store the start and end times of each meeting
        ArrayList<int[]> slots = new ArrayList<>();
        
        // Add start and end times as pairs (arrays) to the slots list
        for (int i = 0; i < n; i++) {
            slots.add(new int[]{start[i], end[i]});
        }
        
        // Sort the meetings based on their end times
        Collections.sort(slots, (a, b) -> a[1] - b[1]);
        
        // Initialize the count of meetings that can be attended
        int count = 1; // The first meeting is always selected
        int lastEndTime = slots.get(0)[1]; // End time of the first meeting
        
        // Iterate through the remaining meetings
        for (int i = 1; i < n; i++) {
            // If the start time of the current meeting is greater than the end time
            // of the last selected meeting, select this meeting
            if (slots.get(i)[0] > lastEndTime) {
                count++;
                lastEndTime = slots.get(i)[1]; // Update the end time
            }
        }
        
        return count; // Return the maximum number of meetings that can be attended
    }
}

```

**Minimum Platforms**
Approach:-
Sort the arrival and departure 
check the condition whether the arrival is greater than the previous train departure or not
if no increase the platform and update the i for seeing next train coming time
if yes decreae the patform and update the departure and increase the j 
```
class Solution {
    // Function to find the minimum number of platforms required at the
    // railway station such that no train waits.
    static int findPlatform(int arr[], int dep[]) {
        // Sort the arrival and departure times
        Arrays.sort(arr);
        Arrays.sort(dep);
        
        // Initialize platform count and maximum platforms needed
        int i = 1, j = 0;
        int platformNeeded = 1;
        int maxPlatform = 1;
        
        // Iterate through the arrival and departure times
        while (i < arr.length && j < dep.length) {
            // If the next train is arriving before the previous one departs,
            // increase platform count
            if (arr[i] <= dep[j]) {
                platformNeeded++;
                i++;
            }
            // Else, decrease platform count as a train has departed
            else {
                platformNeeded--;
                j++;
            }
            // Update the maximum platforms required
            maxPlatform = Math.max(maxPlatform, platformNeeded);
        }
        
        // Return the maximum number of platforms required
        return maxPlatform;
    }
}
```


