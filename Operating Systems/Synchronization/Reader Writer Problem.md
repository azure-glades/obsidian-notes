Implemented in C
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>

// Global variables
int count = 0;   // Keeps track of the "page number" written
int rcount = 0;  // Tracks the number of readers currently reading

// Semaphores for synchronization
sem_t mutex; // To protect the critical section for readers
sem_t wr;    // To ensure mutual exclusion for writers

// Writer function
void* writer(void *p) {
    int* i = (int*)p; // Pointer to the writer ID passed as argument
    
    sem_wait(&wr); // Writer acquires exclusive access to the shared resource
    printf("\nWriter %d writes page number %d", *i, ++count); // Write operation
    sem_post(&wr); // Release access for other writers or readers
}

// Reader function
void* reader(void* p) {
    int* i = (int*)p; // Pointer to the reader ID passed as argument
    
    // Readers entering critical section
    sem_wait(&mutex); // Protect rcount update
    rcount++;         // Increment the number of readers
    if (rcount == 1) {
        sem_wait(&wr); // If this is the first reader, block writers
    }
    sem_post(&mutex); // Release access to rcount

    // Read operation
    printf("\nReader %d reads page number %d", *i, count);

    // Readers leaving critical section
    sem_wait(&mutex); // Protect rcount update
    rcount--;         // Decrement the number of readers
    if (rcount == 0) {
        sem_post(&wr); // If no readers are left, allow writers
    }
    sem_post(&mutex); // Release access to rcount
}

int main() {
    // Initialize semaphores
    sem_init(&mutex, 0, 1); // Binary semaphore for reader mutual exclusion
    sem_init(&wr, 0, 1);    // Binary semaphore for writer exclusivity
    
    // Array of IDs for 3 writers and 3 readers
    int a[6] = {1, 2, 3, 1, 2, 3};
    pthread_t p[6]; // Array of thread handles for 3 writers and 3 readers
    
    // Create writer threads
    for (int i = 0; i < 3; i++) {
        pthread_create(&p[i], NULL, writer, &a[i]);
    }

    // Create reader threads
    for (int i = 3; i < 6; i++) {
        pthread_create(&p[i], NULL, reader, &a[i]);
    }

    // Wait for all threads to complete
    for (int i = 0; i < 6; i++) {
        pthread_join(p[i], NULL);
    }

    return 0;
}

```