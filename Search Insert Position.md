# Search Insert Position

## Intuition

Since the array is sorted in ascending order, binary search can efficiently locate the target. If the target exists, return its index. Otherwise, the position where the search ends represents the correct insertion index while maintaining the sorted order.

---

## Approach

* Initialize two pointers representing the beginning and end of the array.
* Repeatedly calculate the middle index.
* Compare the middle element with the target:

  * If equal, return the middle index.
  * If smaller, search the right half.
  * If larger, search the left half.
* When the search space becomes empty, the left pointer indicates the correct insertion position.

---

## Algorithm

1. Set two pointers:

   * `left` at the beginning of the array.
   * `right` at the last index of the array.
2. While `left` is less than or equal to `right`:

   * Compute the middle index.
   * If the middle element equals the target, return its index.
   * If the middle element is smaller than the target, move `left` to `middle + 1`.
   * Otherwise, move `right` to `middle - 1`.
3. Return `left` as the insertion position.

---

## Code (C++)

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    int searchInsert(vector<int>& numbers, int target) {
        int left = 0;
        int right = numbers.size() - 1;

        while (left <= right) {
            int middle = left + (right - left) / 2;

            if (numbers[middle] == target) {
                return middle;
            } else if (numbers[middle] < target) {
                left = middle + 1;
            } else {
                right = middle - 1;
            }
        }

        return left;
    }
};
```

---

## Time Complexity

**O(log n)**

Binary search halves the search space in every iteration.

---

## Space Complexity

**O(1)**

Only a constant amount of extra space is used.
