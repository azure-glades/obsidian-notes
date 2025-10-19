*Definition*:
A circular queue is an advanced version of a linear queue that connects the last element back to the first element, forming a circular structure. This design allows for efficient use of space and overcomes limitations associated with traditional linear queues.
- **Efficient Memory Utilization**: By reusing vacated spaces, circular queues minimize wasted memory that can occur in linear queues.
- **Continuous Operation**: The circular nature allows for continuous insertion and deletion without needing to reset or shift elements.

-> Used to implement a [[Message Queuing]] system
## Array Implementation
```c
#include <stdio.h>
#define MAX 8

struct queue
{
	int a[MAX];
	int f, r;
};

void nq(struct queue *q, int n)
{
	if(q->r == -1)
	{
		printf("Creating queue...\n");
		q->r = 0; q->f = 0;
		q->a[q->r] = n;
		return;
	}
	if(q->r == (q->f-1) || (q->r == MAX-1 && q->f == 0))
	{
		printf("QUEUE FULL\n");
	}
	else
	{
		q->r = (q->r+1)%MAX;
		q->a[q->r]= n;
	}
}

int dq(struct queue *q)
{
	if(q->f == -1)
	{
		printf("EMPTY QUEUE\n");
		return 404;
	}
	else
	{
		int t = q->a[q->f];
		printf("Deleted %d\n", t);
		if(q->f == q->r)
		{
			q->f = q->r = -1;
		}
		else
		{
		//Big brain technigue. if f > MAX, index is put from 0 to MAX automatically
			q->f = (q->f+1)%MAX;
		}
		return t;
	}
}

void display(struct queue *q)
{
	for(int i = q->f; i < q->r; i++)
	{
		printf("%d > ", q->a[i]);
	}
	printf("[]\n");
}
```

## Linked List Implementation
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    int info;
    struct node *next;
} *NODE;

NODE getNode(int info) {
    NODE t;
    t = (NODE)malloc(sizeof(struct node));
    t->info = info;
    t->next = NULL;
    return t;
}

NODE attachNode(NODE start, int info) {
    NODE nw = getNode(info);
    if (start == NULL) {
        nw->next = nw;
        return nw;
    }

    nw->next = start->next;
    start->next = nw;
    return start;
}

NODE removeNode(NODE start) {
    if (start == NULL) {
        printf("No Queue\n");
        return start;
    }

    NODE cur = start->next;
    if (start->next == start) { // Use == for comparison
        printf("Info: %d\n", start->info);
        free(start);
        return NULL;
    }

    while (cur->next != start)
        cur = cur->next;
    printf("Info: %d\n", start->info);
    cur->next = start->next;
    free(start);
    return cur;
	}
```