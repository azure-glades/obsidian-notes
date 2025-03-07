

```java
class Solution {
    // Please change the array in-place
    public void insertionSort(int arr[]) {
        // code here
        /* iterative
        int len = arr.length;
        for(int i = 1; i<len; i++){
            int j = i;
            while(j >0 && arr[j]<arr[j-1]){
                int tmp = arr[j];
                arr[j] = arr[j-1];
                arr[j-1] = tmp;
                j--;
            }
        }
        */
        sort(arr, arr.length-1);
    }
	// recursive    
    void sort(int arr[], int n){
        if(n <= 0){
            return;
        }
        
        sort(arr, n-1);
        int key = arr[n];
        int j = n-1;
        while(j >= 0 && arr[j] > key){
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = key;
    }
}
```