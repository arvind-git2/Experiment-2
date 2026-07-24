# Largest Rectangle in Histogram

## Intuition

A rectangle in the histogram can extend left and right until a bar shorter than its height is encountered. Instead of checking every possible rectangle, a stack can be used to efficiently determine the maximum width for each bar where it acts as the smallest height.

---

## Approach

* Maintain a stack to store the indices of histogram bars in increasing order of their heights.
* Traverse the histogram from left to right.
* If the current bar is shorter than the bar at the top of the stack, repeatedly pop indices from the stack.
* For each popped bar:

  * Calculate its height.
  * Determine the width of the rectangle it can form.
  * Compute the area and update the maximum area.
* After processing all bars, use a virtual bar of height `0` to ensure all remaining bars in the stack are processed.

---

## Algorithm

1. Create an empty stack to store indices of histogram bars.
2. Initialize the maximum area as `0`.
3. Traverse the histogram from left to right, including one additional iteration with height `0`.
4. While the current bar is shorter than the bar represented by the top index in the stack:

   * Pop the top index.
   * Use the corresponding bar height.
   * Calculate the rectangle width:

     * If the stack becomes empty, the width is the current index.
     * Otherwise, the width is the distance between the current index and the new top of the stack minus one.
   * Compute the area and update the maximum area.
5. Push the current index onto the stack.
6. Return the maximum area obtained.

---

## Code (C++)

```cpp
#include <vector>
#include <stack>
#include <algorithm>
using namespace std;

class Solution {
public:
    int largestRectangleArea(vector<int>& histogram) {
        stack<int> indexStack;
        int maximumArea = 0;
        int numberOfBars = histogram.size();

        for (int currentIndex = 0; currentIndex <= numberOfBars; currentIndex++) {

            int currentHeight = (currentIndex == numberOfBars) ? 0 : histogram[currentIndex];

            while (!indexStack.empty() &&
                   histogram[indexStack.top()] > currentHeight) {

                int height = histogram[indexStack.top()];
                indexStack.pop();

                int width;
                if (indexStack.empty()) {
                    width = currentIndex;
                } else {
                    width = currentIndex - indexStack.top() - 1;
                }

                int area = height * width;
                maximumArea = max(maximumArea, area);
            }

            indexStack.push(currentIndex);
        }

        return maximumArea;
    }
};
```

---

## Time Complexity

**O(n)**

Each histogram bar is pushed onto and popped from the stack at most once.

---

## Space Complexity

**O(n)**

The auxiliary stack may store up to `n` indices in the worst case.
