- **Front**: The end from which elements are removed (dequeued).
- **Rear**: The end where elements are added (enqueued).
Operations: The primary operations include:
- **Enqueue**: Adding an element at the rear.
- **Dequeue**: Removing an element from the front.
- **Peek**: Viewing the front element without removing it.

## Array representation

```c
#include <stdio.h>
#define MAX 64

struct queue
{
	int a[MAX];
	int rear;
	int front;
};


void enqueue(struct queue *q1, int ele)
{
	if(q1->rear == MAX-1)
	{
		printf("\nMEMORY OVERFLOW");
		return;
	}
	
	q1->a[++(q1->rear)] = ele;
}

int dequeue(struct queue  *q1)
{
	if(q1->front > q1->rear)
	{
		printf("\nMEMORY UNDERFLOW");
		return 404;
	}
	return q1->a[(q1->front)++];
}

void display(struct queue *q1)
{
	if(q1->front > q1->rear)
	{
		printf("\n--- end of queue ---");
		return;
	}
	
	printf("Queue contents: ");
	for(int i = q1->front; i<=q1->rear; i++)
	{
		printf("%d ", q1->a[i]);
	}
	printf("\n");
}
```

