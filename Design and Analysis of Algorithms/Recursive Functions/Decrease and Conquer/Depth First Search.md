#graph-traversal-algorithm
DFS is pre-order traversal on binary tree. DFS uses a stack, and when done with recursion, the stack is the call stack.
The pop-order in DFS is a way of getting the [[Topological Ordering]] of a graph
```al
FUNCTION DFS(G)
//INPUT: G is a graph, G = {V,E}
//OUTPUT: G is marked with consequtive integers in which they have been encountered
	count = 0
	FOR (vertex in V)
		IF (v is unvisited)
			dfs_driver(v)
		END IF
	END FOR
RETURN

FUNCTION dfs_driver(v)
//INPUT: v is a vertex in graph G
	count++
	set v = count //order of encounter
	FOR (vertex w in V AND w is adjacent to v)
		IF (w is unvisited)
			dfs_driver(w)
		END IF
	END FOR
RETURN
```

DFS in Java
```java
package DAA;  
  
import java.util.Arrays;  
  
public class DFS {  
    int[][] adj_m = {{0,1,0,0,1,1},{...},{1,0,0,0,0,0}};
    int[] visited = {0,0,0,0,0,0};  
    int count = 0;  
  
    void dfs_driver(){  
        for(int i = 0; i<6; i++){  
            if(visited[i] == 0){  
                dfs_recurse(i);  
            }  
        }  
    }  
  
    void dfs_recurse(int n){  
        count++;  
        visited[n] = count;  
        System.out.printf("%d, ", n);  
        for(int j = 0; j<6; j++){  
            if(adj_m[n][j] == 1){  
                if(visited[j] == 0){  
                    dfs_recurse(j);  
                }  
            }  
        }  
    }  
  
    public static void main(String[] args){  
        DFS dd = new DFS();  
        dd.dfs_driver();  
        System.out.println();  
        System.out.println(Arrays.toString(dd.visited));  
    }  
}
```