# leet-day65

# Merge Intervals

## Problem Description

Given an array of intervals where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

### Example 1:

**Input:**

```cpp
intervals = [[1,3],[2,6],[8,10],[15,18]]
```

**Output:**

```cpp
[[1,6],[8,10],[15,18]]
```

**Explanation:**

Since intervals `[1,3]` and `[2,6]` overlap, merge them into `[1,6]`.

### Example 2:

**Input:**

```cpp
intervals = [[1,4],[4,5]]
```

**Output:**

```cpp
[[1,5]]
```

**Explanation:**

Intervals `[1,4]` and `[4,5]` are considered overlapping.

## Approach

To solve this problem efficiently, we can follow these steps:

1. Sort the intervals based on their start times in ascending order. This step ensures that overlapping intervals will be adjacent to each other.

2. Initialize an empty vector `mergedIntervals` to store the merged intervals.

3. Initialize a `currentInterval` variable with the first interval from the sorted list.

4. Iterate through the sorted intervals, starting from the second interval.

5. For each interval, check if it overlaps with the `currentInterval` by comparing the end time of `currentInterval` with the start time of the current interval.

6. If there is an overlap, merge the intervals by updating the end time of `currentInterval` to the maximum of the two end times.

7. If there is no overlap, add the `currentInterval` to `mergedIntervals` and update `currentInterval` to the current interval being processed.

8. After the loop, add the last remaining `currentInterval` to `mergedIntervals`.

9. Return `mergedIntervals` as the result.

## Complexity Analysis

- Time Complexity: O(n * log(n)), where n is the number of intervals. Sorting the intervals takes O(n * log(n)) time.

- Space Complexity: O(n), where n is the number of intervals. We use additional space to store the merged intervals.

## Implementation

```cpp
#include <vector>
#include <algorithm>

class Solution {
public:
    std::vector<std::vector<int>> merge(std::vector<std::vector<int>>& intervals) {
        // Sort the intervals based on their start times
        std::sort(intervals.begin(), intervals.end(), [](const std::vector<int>& a, const std::vector<int>& b) {
            return a[0] < b[0];
        });

        std::vector<std::vector<int>> mergedIntervals;
        std::vector<int> currentInterval = intervals[0];

        for (int i = 1; i < intervals.size(); ++i) {
            // Check if the current interval overlaps with the next interval
            if (currentInterval[1] >= intervals[i][0]) {
                // Merge the intervals by updating the end time
                currentInterval[1] = std::max(currentInterval[1], intervals[i][1]);
            } else {
                // If no overlap, add the current interval to the result and update the current interval
                mergedIntervals.push_back(currentInterval);
                currentInterval = intervals[i];
            }
        }

        // Add the last remaining interval to the result
        mergedIntervals.push_back(currentInterval);

        return mergedIntervals;
    }
};
```

You can use this implementation to merge overlapping intervals efficiently.

## Summary

This solution provides an efficient way to merge overlapping intervals in a given array. By sorting the intervals based on their start times and merging adjacent overlapping intervals, we can obtain a list of non-overlapping merged intervals as the result. The time complexity of this solution is O(n * log(n)), where n is the number of intervals, making it suitable for large datasets.
