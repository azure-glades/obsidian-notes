```c
#include <stdio.h>
#include <semaphore.h>
#include <pthread.h>
#include <stdlib.h>

#define SIZE 16 // Buffer size for the producer-consumer problem

// Synchronization primitives and shared data
pthread_mutex_t mutex;          // Mutex to protect shared resources (buffer and counter)
pthread_t producer_id[20], consumer_id[20]; // Thread IDs for producers and consumers
sem_t full, empty;              // Semaphores to track buffer availability
int counter;                    // Index for the buffer (tracks the current number of items)
int buffer[SIZE];               // Shared buffer

// Initialize synchronization primitives and variables
void init() {
    pthread_mutex_init(&mutex, NULL); // Initialize mutex
    sem_init(&full, 0, 0);           // Semaphore to count the number of filled slots (initially 0)
    sem_init(&empty, 0, SIZE);       // Semaphore to count the number of empty slots (initially SIZE)
    counter = 0;                     // Initialize counter to 0
}

// Function to write an item to the buffer
void write(int item) {
    buffer[counter++] = item; // Add item to buffer and increment counter
}

// Function to read an item from the buffer
int read() {
    return (buffer[--counter]); // Decrement counter and return the item
}

// Producer thread function
void *producer(void *p) {
    int wait_time, item;
    item = rand() % 5;           // Generate a random item
    wait_time = rand() % 5;      // Generate a random wait time (not used here but can simulate delays)

    sem_wait(&empty);            // Decrement empty slots (wait if buffer is full)
    pthread_mutex_lock(&mutex);  // Lock mutex to protect shared resources
    printf("\nProducer produced %d\n", item); // Print item produced
    write(item);                 // Write item to buffer
    pthread_mutex_unlock(&mutex);// Unlock mutex
    sem_post(&full);             // Increment filled slots
}

// Consumer thread function
void *consumer(void *p) {
    int wait_time, item;
    wait_time = rand() % 5;      // Generate a random wait time (not used here but can simulate delays)

    sem_wait(&full);             // Decrement filled slots (wait if buffer is empty)
    pthread_mutex_lock(&mutex);  // Lock mutex to protect shared resources
    item = read();               // Read item from buffer
    printf("\nConsumer consumed %d\n", item); // Print item consumed
    pthread_mutex_unlock(&mutex);// Unlock mutex
    sem_post(&empty);            // Increment empty slots
}

// Main function
int main() {
    int n1, n2, i;

    init(); // Initialize semaphores, mutex, and shared variables

    // Get the number of producers and consumers from the user
    printf("Number of Producers: ");
    scanf("%d", &n1);
    printf("Number of Consumers: ");
    scanf("%d", &n2);

    // Create producer threads
    for (i = 0; i < n1; i++) 
        pthread_create(&producer_id[i], NULL, producer, NULL);

    // Create consumer threads
    for (i = 0; i < n2; i++) 
        pthread_create(&consumer_id[i], NULL, consumer, NULL);

    // Wait for all producer threads to finish
    for (i = 0; i < n1; i++) 
        pthread_join(producer_id[i], NULL);

    // Wait for all consumer threads to finish
    for (i = 0; i < n2; i++) 
        pthread_join(consumer_id[i], NULL);

    exit(0); // Exit the program
}

```