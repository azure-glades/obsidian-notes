[[Infix-Prefix-Postfix]]

A **stack** is a linear data structure that operates on a **Last In, First Out (LIFO)** principle.
Stacks have 2 variables `top` and `MAX` and 3 primitive operations; `pop`, `push`, `peek`

## 1. Implementing a stack in C
- Stacks are represented using a structure, either via an array, or via a linked list
```c
struct stack {
	int array[MAX];
	int top;
}
```
### 1.1. `pop()`
- Implement in array
```algorithm
if(top == NULL)
	print("STACK UNDERFLOW")
	exit
else
	return stack[top]
	top--
exit
```
- Implement in linked list
``` algorithm
if(head->next == NULL)
	print("STACK UNDERFLOW)
	exit
else
	ptr = head
	head = head->next
	free(ptr)
exit
```

### 1.2. `push()`
- Implement in array
```
if(top == MAX - 1)
	print("STACK OVERFLOW")
	end
else
	top++
	stack[top] = value
exit
```
- Implement in linked list
```algorithm
struct linked_list new_node

new_node->data = value
new_node->next = head
head = new_node

exit
```

### 1.3. `peek()`
- Implement in array
```algorithm
if(top == NULL)
	print("empty stack")
else
	print(stack[top])
exit
```

- Implement in linked_list
```
if(head == NULL)
	print("empty stack")
else
	print(head->data)
exit
```

## 2. Application of stacks
All applications of stacks utillize the LIFO to their advantage
1. [[Reversing a list]]
2. [[Parenthesis checker]]
3. [[Infix-Prefix-Postfix]]
4. . **Function Call Management**:
    - Stacks manage function calls and execution contexts, enabling recursion and nested calls by pushing and popping contexts.
5. **Undo/Redo Functionality**:
    - Used in applications like text editors to track user actions; actions are pushed onto an undo stack, allowing users to revert or reapply changes.
6. **Expression Evaluation**:
    - Essential for evaluating arithmetic expressions in postfix notation by pushing operands onto the stack and applying operators as needed.
7. **Syntax Parsing and Delimiter Checking**:
    - Employed in compilers to check matching delimiters (parentheses, brackets) by pushing opening delimiters onto the stack and popping them for closing matches.
8. **Backtracking Algorithms**:
    - Utilized in solving puzzles (e.g., mazes, Sudoku) to track choices and states, allowing the algorithm to backtrack by popping states off the stack when dead ends are encountered.