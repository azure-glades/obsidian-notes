 Open hashing, also known as separate chaining, allows multiple values to be stored in the same index of the hash table by adding each colliding index to the end of linked list. Each index stores a linked list

Implementation:
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 16
#define EMPTY -9999

struct node {
	int info;
	struct node *next;
};
typedef struct node *NODE;

NODE getNode(int key){
	NODE tmp = (NODE)malloc(sizeof(struct node));
	tmp->info = key;
	tmp->next = NULL;
	return tmp;
}

struct table{
	NODE entry[MAX];
};
typedef struct table *HASH;

HASH initTable(){
	HASH ht = (HASH)malloc(sizeof(struct table));
	for(int i = 0; i<MAX; i++){
		NODE tmp = getNode(EMPTY);
		ht->entry[i] = tmp;
	}
	return ht;
}

int hashfn(int key){
	return (key % MAX);
}

void insert(HASH table, int key){
	int i = hashfn(key);
	NODE tmp = getNode(key);
	if((table->entry[i])->info == EMPTY)
		table->entry[i] = tmp;
	else {
		NODE cur = table->entry[i];
		while(cur->next != NULL)
			cur = cur->next;
		cur->next = tmp;
	}
}

void display(HASH table){
	printf("INDEX\tINFO\n");
	for(int i = 0; i<MAX; i++){
		if((table->entry[i])->info == EMPTY)
			printf("%d)\t[x]\n", i);
		else{
			printf("%d)\t", i);
			NODE cur = table->entry[i];
			while(cur != NULL) {
				printf("%d->",cur->info);
				cur = cur->next;
			}
			printf("[x]\n");
		}
	}
	printf("-----\t----\n");
}

int search(HASH table, int key){
	int i = hashfn(key);
	NODE cur = table->entry[i];
	int cnt = 1;
	while(cur != NULL && cur->info != key){
		cur = cur->next;
		cnt++;
	}
	if(cur == NULL) {
		printf("Error: Not found\n");
		return -1;
	} else { 
		printf("Found at INDEX: %d, POS: %d", i, cnt);
		return i;
	}
}

void delete(HASH table, int key){
	int i = hashfn(key);
	NODE cur = table->entry[i];
	NODE prev = cur;
	while(cur != NULL && cur->info != key){
		cur = cur->next;
	}
	while(prev->next != cur)
		prev = prev->next;

	if(cur == NULL) {
		printf("Error: Not found\n");
		return;
	} else { 
		prev->next = cur->next;
		cur->info = EMPTY;
		free(cur);
		cur = NULL;
	}
}
```