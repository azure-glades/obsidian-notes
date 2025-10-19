### `Stack` Cheatsheet 📚

A `Stack` is a data structure that follows the **Last-In, First-Out (LIFO)** principle. The recommended way to implement a stack in modern Java is by using a **`Deque`** (Double-Ended Queue), specifically the **`ArrayDeque`** class.

---

### Key Methods

|Method|Purpose|Returns|
|---|---|---|
|`push(E e)`|**Adds** an element to the top of the stack.|`void`|
|`pop()`|**Removes** and returns the element at the top.|The element, or throws `NoSuchElementException` if empty|
|`peek()`|**Returns** (but doesn't remove) the element at the top.|The element, or `null` if empty|
|`isEmpty()`|Checks if the stack has no elements.|`boolean` (`true` or `false`)|
|`size()`|Returns the number of elements.|`int`|

---

### Common Usage Pattern
``` java
import java.util.ArrayDeque;
import java.util.Deque;

public class StackExample {
    public static void main(String[] args) {
        // 1. Define and initialize a Stack
        Deque<String> stack = new ArrayDeque<>();

        // 2. Add elements to the stack
        stack.push("Task A");
        stack.push("Task B");
        stack.push("Task C");

        System.out.println("Current stack: " + stack); // [Task C, Task B, Task A] (order depends on implementation toString())

        // 3. Check the top element without removing it
        String nextTask = stack.peek();
        System.out.println("Top element (peek): " + nextTask); // Task C

        // 4. Process all elements in the stack
        while (!stack.isEmpty()) {
            String currentTask = stack.pop();
            System.out.println("Popping: " + currentTask);
        }

        System.out.println("Is the stack empty? " + stack.isEmpty()); // true
    }
}
```
