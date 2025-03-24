Implementation:
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 16
#define CONST 5
#define EMPTY -9999

struct table{
	int entry[MAX];
};
typedef struct table *HASH;

HASH initTable(){
	HASH ht = (HASH)malloc(sizeof(struct table));
	for(int i = 0; i<MAX; i++){
		ht->entry[i] = tmp;
	}
	return ht;
}

int hashfn(int key){
	return (key % MAX);
}

int secondhashfn(int key){
	return (key % CONST)+1;
}

void insert(HASH table, int key){
	int i = hashfn(key);
	if	
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