2 methods: reverse pop order of DFS and Vertex deletion method (which is [[Kahn's Algorithm]])

```al
FUNC topologicalSort(G)
	call DFS(G) -> as each vertex gets finished, insert it to linked-list
RETURN linked-list
```


## DFS in C
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 64

typedef struct Graph{
	int vertices;
	int adj[MAX][MAX];
	int visited[MAX];
} Graph;

typedef struct Stack{
	int data[MAX];
	int top;
} stk;

void initGraph(Graph *g, int vertices){
	g->vertices = vertices;
	for(int i = 0; i<vertices; i++){
		g->visited[i] = 0;
		for(int j = 0; j<vertices; j++){
			g->adj[i][j] = 0;
		}
	}
}

void addEdge(Graph *g, int u, int v) {
    g->adj[u][v] = 1; 
}

void initStack(stk *s) {
    s->top = -1;
}

void push(stk *s, int value) {
    s->data[++(s->top)] = value;
}

int pop(stk *s) {
    return s->data[(s->top)--];
}

void dfs(Graph *g, stk *s, int vertex){
	g->visited[vertex] = 1;
	for(int i = 0; i<g->vertices; i++){
		if(g->adj[vertex][i] && !g->visited[i]){
			dfs(g,s,i);
		}
	}
	push(s, vertex);
}

void topologicalSort(Graph *g){
	stk s;
	initStack(&s);

	for(int i = 0; i<g->vertices; i++){
		if(!g->visited[i]){
			dfs(g, &s, i);
		}
	}

	printf("Topological Sort: ");
	while(s.top != -1){
		printf("%d->", pop(&s));
	}
	printf("\n");
}

int main() {
    Graph g;
	
	g.vertices = 6;
	initGraph(&g, g.vertices);
    
	addEdge(&g, 5, 2);
    addEdge(&g, 5, 0);
    addEdge(&g, 4, 0);
    addEdge(&g, 4, 1);
    addEdge(&g, 2, 3);
    addEdge(&g, 3, 1);

	topologicalSort(&g);
	return 0;
}
```