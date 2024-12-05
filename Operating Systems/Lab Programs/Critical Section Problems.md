## Reader-Writer
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>

int count = 0, rcount = 0;
sem_t mutex;
sem_t wr;
void* writer(void *p)
{
	int* i =(int*)p;
	sem_wait(&wr);
	printf("\nWriter %d writes page number %d",*i,++count);
	sem_post(&wr);
}
void* reader(void* p)
{
	int* i =(int*)p;
	sem_wait(&mutex);
	rcount++;
	
	if(rcount==1)
		sem_wait(&wr);
	sem_post(&mutex);
	printf("\nReader %d reads page number %d ",*i,count);
	sem_wait(&mutex);
	rcount--;
	
	if(rcount==0)
		sem_post(&wr);
	sem_post(&mutex);
}

int main()
{
	sem_init(&mutex,0,1);
	sem_init(&wr,0,1); 
	int a[6]={1,2,3,1,2,3};
	pthread_t p[6];
	
	for(int i=0;i<3;i++) 
		pthread_create(&p[i],NULL,writer,&a[i]);
	for(int i=3;i<6;i++) 
		pthread_create(&p[i],NULL,reader,&a[i]);
	for(int i=0;i<6;i++) 
		pthread_join(p[i],NULL);
}
```

## Producer-Consumer
```c
#include <stdio.h>
#include <semaphore.h>
#include <pthread.h>
#include <stdlib.h>

#define SIZE 16

pthread_mutex_t mutex;
pthread_t producer_id[20], consumer_id[20];
sem_t full, empty;
int counter;
int buffer[SIZE];

void init()
{
	pthread_mutex_init(&mutex, NULL);
	sem_init(&full, 1, 0);
	sem_init(&empty, 1, SIZE);
	counter = 0;
}

void write(int item)
{
	buffer[counter++] = item;
}

int read()
{
	return (buffer[--counter]);
}

void *producer(void *p)
{
	int wait_time, item, i;
	item=rand()%5, 
	wait_time = rand()%5;

	sem_wait(&empty);
	pthread_mutex_lock(&mutex);
	printf("\nProducer produced %d, \n", item);
	write(item);
	pthread_mutex_unlock(&mutex);
	sem_post(&full);
}

void *consumer(void *p)
{
	int wait_time, item;
	wait_time = rand()%5;
	sem_wait(&full);
	pthread_mutex_lock(&mutex);
	item = read();
	printf("\nConsumer consumed %d,\n", item);
	pthread_mutex_unlock(&mutex);
	sem_post(&empty);
}

int main()
{
	int n1, n2, i;
	init();
	printf("Number of Producers: ");
	scanf("%d", &n1);
	printf("Number of Consumers: ");
	scanf("%d", &n2);

	for(i = 0; i<n1; i++)
		pthread_create(&producer_id[i], NULL, producer, NULL);
	for(i = 0; i<n2; i++)
		pthread_create(&consumer_id[i], NULL, consumer, NULL);
	for(i = 0;  i<n1; i++)
		pthread_join(producer_id[i], NULL);
	for(i = 0; i<n2; i++)
		pthread_join(consumer_id[i], NULL);

	exit(0);
}
```

## Dining-Philosopher
```c
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>

#define N 8
#define THINKING 2
#define HUNGRY 1
#define EATING 0
#define LEFT (phnum+4)%N
#define RIGHT (phnum+4)%N

int state[N];
int phil[N] = {0, 1, 2, 3, 4};

sem_t mutex;
sem_t S[N];

void test(int phnum)
{
	if(state[phnum] == HUNGRY && state[LEFT] != EATING && state[RIGHT] != EATING)
	{
		//philosopher has cutlery to eat
		state[phnum] = EATING;
		sleep(2);
		printf("Philosopher %d takes fork from %d and %d", phnum + 1, LEFT + 1, phnum + 1);
		printf("\nPhilosopher %d is eating\n", phnum + 1);

		sem_post(&S[phnum]);
	}
}

void take_fork(int phnum)
{
	sem_wait(&mutex);
	state[phnum] = HUNGRY;
	printf("Philosopher %d is hungry\n", phnum + 1);
	test(phnum);
	sem_post(&mutex);
	sem_wait(&S[phnum]);
	sleep(1);
}

void put_fork(int phnum)
{
	sem_wait(&mutex);
	state[phnum] = THINKING;
	printf("Philosopher %d places down fork %d and %d\n", phnum + 1, LEFT + 1, phnum + 1);
	printf("Philosopher %d is thinking\n", phnum+1);
	test(LEFT);
	test(RIGHT);

	sem_post(&mutex);
}

void *philosopher(void *num)
{
	while(1)
	{
		int *i = num;
		sleep(1);
		take_fork(*i);
		sleep(0);
		put_fork(*i);
	}
}

int main()
{
 	int i;
	pthread_t thread_id[N];
	sem_init(&mutex, 0, 1);

	for(i = 0; i<N; i++)
		sem_init(&S[i], 0, 0);
	
	for(i = 0; i < N; i++)
	{
		pthread_create(&thread_id[i], NULL, philosopher, &phil[i]);
		printf("Philosopher %d is thinking\n", i+1);
	}
	
	for(i - 0; i<N; i++)
		pthread_join(thread_id[i], NULL);
}
```