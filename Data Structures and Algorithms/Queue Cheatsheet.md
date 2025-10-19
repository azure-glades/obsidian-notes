### `Queue` Cheatsheet 📦

A `Queue` is a data structure that follows the **First-In, First-Out (FIFO)** principle. The recommended way to implement a queue in Java is by using a **`Deque`** (Double-Ended Queue), specifically the **`ArrayDeque`** class, as it's efficient for this purpose.

---

### Key Methods

|Method|Purpose|Throws Exception?|Returns on Failure|
|---|---|---|---|
|`offer(E e)`|**Adds** an element to the end of the queue.|No|`false`|
|`poll()`|**Removes** and returns the element at the front.|No|`null`|
|`peek()`|**Returns** (but doesn't remove) the element at the front.|No|`null`|
|`isEmpty()`|Checks if the queue has no elements.|No|`true` or `false`|
|`size()`|Returns the number of elements.|No|An integer|

---

### Common Usage Pattern

Java

``` java
import java.util.ArrayDeque;
import java.util.Queue;

public class QueueExample {
    public static void main(String[] args) {
        // 1. Define and initialize a Queue
        Queue<String> tasks = new ArrayDeque<>();

        // 2. Add elements to the queue
        tasks.offer("Task A");
        tasks.offer("Task B");

        // 3. Check the next element without removing it
        String nextTask = tasks.peek();
        System.out.println("Next task: " + nextTask); // Output: Task A

        // 4. Process all elements in the queue
        while (!tasks.isEmpty()) {
            String currentTask = tasks.poll();
            System.out.println("Processing: " + currentTask);
        }

        System.out.println("Is the queue empty? " + tasks.isEmpty()); // Output: true
    }
}
```