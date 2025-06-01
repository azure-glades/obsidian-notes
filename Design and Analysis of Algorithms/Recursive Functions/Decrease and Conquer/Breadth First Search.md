#graph-traversal-algorithm 
BFS is level-order on binary tree
The running time of BFS is $\text{O}(V + E)$ 
BFS produces the bredth-first forest

```al
FUNC BFS(G, r)
//INPUT: Graph G = {E, V}, r is the starting node
	static count = 1
	visited[r] = count
	count++
	queue.enqueue(r)
	WHILE (queue != EMPTY)
		v = queue.dequeue()
		FOR (w, w is a neighbour of v)
			IF(visited[w] == 0)
				visited[w] == count
				count++
				queue.enqueue(w)
			END IF
		END FOR
	END WHILE
RETURN visited
```

Here is BFS in Java using a queue
```java
package DAA;  
import java.util.Arrays;  
import java.util.LinkedList;  
  
public class BFS {  
    int[][] adj_m = {{0,1,0,0,1,1},{...},{1,0,0,0,0,0}};  
    LinkedList<Integer> qu = new LinkedList<>();  
    int[] visited = {0,0,0,0,0,0};  
    int count = 0;  
  
    void bfs_recurse(int n){  
        for(int i = n; i<6; i++){  
            for(int j = 0; j<6; j++){  
                if(adj_m[i][j] == 1 && visited[j] == 0){  
                    qu.add(j);  
                }  
            }  
            if(visited[i] == 0){  
                count++;  
                visited[i] = count;  
                System.out.printf("%d, ",i);  
                while(qu.peek() != null){  
                    bfs_recurse(qu.poll());  
                }  
            }  
        }  
    }  
  
    public static void main(String[] args){  
        BFS nn = new BFS();  
        nn.bfs_recurse(0);  
        System.out.printf("\n"+ Arrays.toString(nn.visited)+"\n");  
    }  
}
```