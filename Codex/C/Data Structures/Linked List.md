[[Nexus ~ C]]

* Made up of a long chain of **Nodes**
* Each node has 2 parts: **Data to be stored**; **Pointer to the next node in link**
	* Final node has no pointer (null), called Tail
	* Starting node is called Head
* Addition and Deletion is easy
* Searching can only be done linearly
* Binary searching done with sorted doubly linked list
```c
struct node{
    int data;
    struct list *next;
};
```

### **Basic linked list functions**
* Starting/Head-pointer to point to the first element of list
```c
//head pointer
node *hp = NULL;
```
* Creating a function to allocate memory from heap. Optional
```c
node* getNode()
{
    node *x;
    x = (node*)malloc(sizeof(struct lls*));
    if(x == NULL)
    {
        printf("memory overloading! !\n");
        return NULL;
    }
    return x;
}
```
* Following loop is used to traverse the list
```c
node* p = hp;
    while(p != NULL)
    {
	    //operation/modification
        p = p->next;
    }
```

1. Creating a list by repeatedly calling the attach to front function
```c
void create(int n)
{
    int hal;
    for(int i = 0; i<n; i++)
    {
        printf("%d: ", i+1);
        scanf("%d", &hal);
        insert_head(hal); //calls insert_head
        printf("\n");
    }
}
```
2. Attaching a new node to beginning
```c
void attach(node head, int val)
{
    head = getNode();
    if(head == NULL)
        printf("Node creation error: Memory not allocated\n");
        return;
    head->data = val;
    head->link = hp;
    hp = head;
}
```
2. Appending a new node to the end
```c
void insert_tail(int val)
{
    node* p = hp;
    while(p->next != NULL)
    {
        p = p->next;
    }
    node *new = getNode();
    new->data = val;
    new->next = NULL;
    p->next = new;
}
```
3. Inserting a new node inside the list
```c
void insert_rand(int val, int pos)
{
    node *p = hp;
    while(p->data != pos)
    {
        p = p->next;
        if(p == NULL)
        {
            printf("Item absent\n");
            return;
        }
    }
    node *new = getNode();
    new->data = val;
    new->next = p->next;
    p->next = new;
}
```
4. Deleting first node (head)\
```c
void del_head()
{
    node *p = hp;
    hp = p->next;
    p->data = 0;
    free(p);
}
```
5. Deleting last node (tail)
```c
void del_tail()
{
    node* p = hp;
    node *pp = hp;
    while(p->next != NULL)
    {
        p = p->next;
    }
    while(pp->next != p)
    {
        pp = pp->next;
    }
    free(p);
    pp->next = NULL;

}
```
6. Deleting a node inside the list
```c
void del_rand(int pos)
{
    node *p = hp;
    node *ptr = hp;
    while(p->data != pos && p != NULL)
    {
        p = p->next;
    }
    while(ptr->next != p)
    {
        ptr = ptr->next;
    }
    ptr->next = p->next;
    p->data = 0;
    free(p);
}

```

 Manipulating the list:
 1. Searching for item
```c
void locate(int val)
{
    int counter = 0;
    int flag = 0;
    node *p = hp;
    while(p != NULL)
    {
        counter++;
        if(p->data == val)
        {
            flag = 1;
            printf("Found at #%d\nAddress: %x\n", counter, (int*)p);
        }
        p = p->next;
    }
    if(flag == 0)
        printf("Data not present\n");
}
```

2. Displaying the list:
```c
void disp()
{
    node* p = hp;
    while(p != NULL)
    {
        printf("%d ->", p->data);
        p = p->next;
    }
    printf("END\n");
}
```
3. Memory dumps all addresses
```c
void memdump()
{
    node *p = hp;
    printf("Addresses:\n");
    while(p != NULL)
    {
        printf("| %x\n", (int*)p);
        p = p->next;
    }
    printf("//end of list//\n");
}
```