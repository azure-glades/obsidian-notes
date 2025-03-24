Message queue system that is realized using a circular queue

```c
#include <stdio.h>
#include <stdlib.h>
#define SIZE 4

struct queue
{
	int front, rear;
	char data[SIZE][32];
};

typedef struct queue QU;

void send (QU *q, char item[32])
{
	if(q->front == (q->rear+1)%SIZE)
		printf("]n message queue full");
	else
	{
		q->rear = (q->rear+1)%SIZE;
		strcpy(q->data[q->rear], item);
		if(q->front == -1)
			q->front = 0;
	}
}

char *receive(QU *q)
{
	char *del ;
	if(q->front == -1)
	{
		printf("\nmessage queue full");
		return -1;
	}
	else
	{
		del = q->data[q->front];
		if(q->front == q->rear)
		{
			q->front = -1;
			q->rear = -1;
		}
		else
			q->front  = (q->front+1)%SIZE;
		return del;
	}
}

void display(QU q)
{
	int i;
	if(q.front == -1)
		printf("\nmessage queue empty");
	else
	{
		printf("\nmessages:\n");
		for(i = q.front; i != q.rear; i = (i+1)%SIZE)
			printf("Message %d: %s\n", i+1, q.data[i]);
		printf("%s\n", q.data[i]);
	}
}

void main()
{
	int ch; char *del; char item[32];
	QU q;
	q.front = -1; q.rear = -1;
	while(1)
	{
		printf("\nsend / receive / display / exit\n");
		printf("> ");
		scanf("%d", &ch);
		getchar();
		switch(ch)
		{
			case 1:
				printf("to send: ");
				scanf("%s", &item);
				send(&q, item);
				break;
			case 2:
				del = receive(&q);
				if(del != NULL)
					printf("deleted element: %s\n", del);
				break;
			case 3:
				display(q);
				break;
			default:
				return;
		}
	}
}
```