# Min Stack

**Level:** Easy

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

## Example

```text
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

## Solution

```python3
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.values = []
        self.min = None

    def push(self, x: int) -> None:
        self.values.append(x)
        if self.min is None or x < self.min:
            self.min = x

    def pop(self) -> None:
        if self.min is None:
            raise ValueError("Pop from empty stack")
  
        value = self.values.pop()
        if value == self.min:
            if len(self.values) == 0:
                self.min = None
            else:
                self.min = sorted(self.values)[0]
        return value

    def top(self) -> int:
        if self.min is None:
            raise ValueError("Top of empty stack")

        return self.values[-1]

    def getMin(self) -> int:
        return self.min


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```

**Note:**

Runtime: 56 ms, faster than 95.30% of Python3 online submissions for Min Stack.\
Memory Usage: 16.2 MB, less than 100.00% of Python3 online submissions for Min Stack.
