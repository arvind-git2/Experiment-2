# 232. Implement Queue using Stacks

---

## Intuition

A queue follows the **FIFO (First In, First Out)** principle, whereas a stack follows **LIFO (Last In, First Out)**. To simulate a queue using stacks, we use two stacks:

- **Input Stack:** Stores newly inserted elements.
- **Output Stack:** Provides elements in queue order.

When removing or peeking an element, if the output stack is empty, transfer all elements from the input stack to the output stack. This reverses the order and makes the oldest element available on top.

---

## Approach

- Maintain two stacks:
  - `in` for insertion.
  - `out` for deletion and front access.
- Push every new element into `in`.
- Before performing `pop()` or `peek()`, check whether `out` is empty.
- If it is empty, move all elements from `in` to `out`.
- The top of `out` represents the front of the queue.

---

## Algorithm

1. Create two stacks: `in` and `out`.
2. For `push(x)`, insert `x` into `in`.
3. For `pop()`:
   - If `out` is empty, move all elements from `in` to `out`.
   - Remove and return the top element of `out`.
4. For `peek()`:
   - If `out` is empty, transfer elements.
   - Return the top element of `out`.
5. For `empty()`:
   - Return true if both stacks are empty.

---

## Code (C++)

#include <stack>
using namespace std;

class MyQueue {
private:
    stack<int> input;
    stack<int> output;

    void transfer() {
        if (output.empty()) {
            while (!input.empty()) {
                output.push(input.top());
                input.pop();
            }
        }
    }

public:
    MyQueue() {}

    void push(int x) {
        input.push(x);
    }

    int pop() {
        transfer();
        int frontElement = output.top();
        output.pop();
        return frontElement;
    }

    int peek() {
        transfer();
        return output.top();
    }

    bool empty() {
        return input.empty() && output.empty();
    }
};
---

---

## Time Complexity

| Operation | Complexity |
|-----------|------------|
| push() | O(1) |
| pop() | O(1) Amortized |
| peek() | O(1) Amortized |
| empty() | O(1) |

---

## Space Complexity

**O(n)**

where `n` is the number of elements stored in the queue.
