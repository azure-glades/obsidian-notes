```c
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>

#define N 8 // Number of philosophers
#define THINKING 2 // State when a philosopher is thinking
#define HUNGRY 1   // State when a philosopher is trying to pick up forks
#define EATING 0   // State when a philosopher is eating
#define LEFT (phnum + N - 1) % N  // Index of the left neighbor
#define RIGHT (phnum + 1) % N     // Index of the right neighbor

int state[N];      // Array to keep track of each philosopher's state
int phil[N] = {0, 1, 2, 3, 4, 5, 6, 7}; // Philosophers numbered 0 to N-1

sem_t mutex;       // Semaphore to ensure mutual exclusion
sem_t S[N];        // Semaphore for each philosopher to control access to forks

// Function to test if a philosopher can start eating
void test(int phnum) {
    // Check if the philosopher is hungry and both neighbors are not eating
    if (state[phnum] == HUNGRY && state[LEFT] != EATING && state[RIGHT] != EATING) {
        state[phnum] = EATING; // Update state to eating
        sleep(2); // Simulate eating time
        printf("Philosopher %d takes fork from %d and %d\n", phnum + 1, LEFT + 1, phnum + 1);
        printf("Philosopher %d is eating\n", phnum + 1);
        sem_post(&S[phnum]); // Signal the philosopher to proceed
    }
}

// Function for a philosopher to take forks
void take_fork(int phnum) {
    sem_wait(&mutex); // Ensure mutual exclusion
    state[phnum] = HUNGRY; // Mark the philosopher as hungry
    printf("Philosopher %d is hungry\n", phnum + 1);
    test(phnum); // Check if the philosopher can eat
    sem_post(&mutex); // Release mutex
    sem_wait(&S[phnum]); // Wait until forks are available
    sleep(1); // Simulate time to pick up forks
}

// Function for a philosopher to put down forks
void put_fork(int phnum) {
    sem_wait(&mutex); // Ensure mutual exclusion
    state[phnum] = THINKING; // Mark the philosopher as thinking
    printf("Philosopher %d places down fork %d and %d\n", phnum + 1, LEFT + 1, phnum + 1);
    printf("Philosopher %d is thinking\n", phnum + 1);
    test(LEFT); // Test if the left neighbor can eat
    test(RIGHT); // Test if the right neighbor can eat
    sem_post(&mutex); // Release mutex
}

// Function representing the philosopher's actions
void *philosopher(void *num) {
    while (1) {
        int *i = num;
        sleep(1); // Simulate thinking time
        take_fork(*i); // Try to pick up forks and eat
        sleep(0); // Simulate eating time
        put_fork(*i); // Put down forks after eating
    }
}

int main() {
    int i;
    pthread_t thread_id[N]; // Thread IDs for philosophers

    sem_init(&mutex, 0, 1); // Initialize the mutex semaphore with a value of 1

    // Initialize semaphores for each philosopher
    for (i = 0; i < N; i++) 
        sem_init(&S[i], 0, 0);

    // Create philosopher threads
    for (i = 0; i < N; i++) {
        pthread_create(&thread_id[i], NULL, philosopher, &phil[i]);
        printf("Philosopher %d is thinking\n", i + 1);
    }

    // Wait for all philosopher threads to complete (in practice, this will run indefinitely)
    for (i = 0; i < N; i++) 
        pthread_join(thread_id[i], NULL);

    return 0;
}

```