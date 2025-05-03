The naive string matching algorithm is a straightforward method for finding all occurrences of a pattern within a text. While simple to implement, it has notable efficiency limitations.
## Definition
A brute-force algorithm that checks **every possible position** in the text to find matches for the pattern. It compares characters sequentially without optimization[1](https://blog.heycoach.in/naive-string-matching-algorithm/)[3](https://www.scaler.in/naive-string-matching-algorithm/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm).
>*See further:* [[Horspool Algorithm]]
## Premise
- **Core Idea**: Slide the pattern over the text one character at a time, checking for matches at each position[1](https://blog.heycoach.in/naive-string-matching-algorithm/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)
- **Use Cases**: Suitable for small texts/patterns, educational purposes, or scenarios prioritizing simplicity over speed[1](https://blog.heycoach.in/naive-string-matching-algorithm/)[4](https://www.upgrad.com/blog/naive-string-matching-algorithm-in-python/)
- **Key Characteristics**
    - No pre-processing required[4](https://www.upgrad.com/blog/naive-string-matching-algorithm-in-python/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)
    - Works with any comparison direction (left-right or right-left)[3](https://www.scaler.in/naive-string-matching-algorithm/)[4](https://www.upgrad.com/blog/naive-string-matching-algorithm-in-python/)
    - Space complexity: O(1)[3](https://www.scaler.in/naive-string-matching-algorithm/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)
## Algorithm Steps
1. **Initialize**: Set text index `i=0`
2. **Slide Window**:
    - For each `i` from 0 to `n-m` (where `n`=text length, `m`=pattern length)
3. **Character Comparison**:
    - Compare text[i+j] with pattern[j] for `j=0` to `m-1`
4. **Match Check**:
    - If all characters match: Record position `i`
    - If mismatch occurs: Increment `i` by 1 and repeat[1](https://blog.heycoach.in/naive-string-matching-algorithm/)[2](https://www.studocu.com/in/messages/question/5082666/b-write-the-pseudocode-for-naive-string-matching-algorithm)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)

```al
FUNCTION NAIVE_SEARCH(text, pattern)
// Finds all pattern occurrences in text
// Input: text string, pattern string
// Output: array of match positions
    n = LENGTH(text)
    m = LENGTH(pattern)
    matches = EMPTY_ARRAY
    
    FOR (i: 0 TO n - m)
        j = 0
        WHILE (j < m AND text[i+j] == pattern[j])
            j = j + 1
        IF (j == m)
            APPEND(matches, i)
    
    RETURN matches

```
## Time Complexity

|Scenario|Complexity|Description|
|---|---|---|
|Best Case|O(n)|Pattern found at first position[3](https://www.scaler.in/naive-string-matching-algorithm/)|
|Average Case|O(m*(n-m))|Partial matches common[1](https://blog.heycoach.in/naive-string-matching-algorithm/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)|
|Worst Case|O(m*n)|No matches or repeated mismatches[3](https://www.scaler.in/naive-string-matching-algorithm/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)|

## Drawbacks
1. **Inefficiency**: Worst-case complexity makes it impractical for large texts[3](https://www.scaler.in/naive-string-matching-algorithm/)[4](https://www.upgrad.com/blog/naive-string-matching-algorithm-in-python/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)
2. **Redundant Comparisons**: Doesn't reuse information from previous matches/mismatches[4](https://www.upgrad.com/blog/naive-string-matching-algorithm-in-python/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)
3. **Sliding Limitation**: Always slides by 1 position, even when mismatches occur early[1](https://blog.heycoach.in/naive-string-matching-algorithm/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)

## Comparison with Optimized Algorithms

| Feature        | Naive                                                                                                                                                                               | KMP Algorithm | Rabin-Karp | Horspool-Boyer-Moore     |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | ---------- | ------------------------ |
| Pre-processing | None[4](https://www.upgrad.com/blog/naive-string-matching-algorithm-in-python/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm) | O(m)          | O(m)       | O(m) bad-character table |
| Worst Time     | O(m*n)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)                                                                          | O(n)          | O(n+m)     | O(m) bad-character table |
| Space          | O(1)[3](https://www.scaler.in/naive-string-matching-algorithm/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm)                 | O(m)          | O(1)       | O(m + alphabet size)     |

While inefficient for large-scale applications, the naive algorithm remains valuable for understanding fundamental pattern matching concepts and serves as a baseline for comparing optimized approaches[1](https://blog.heycoach.in/naive-string-matching-algorithm/)[4](https://www.upgrad.com/blog/naive-string-matching-algorithm-in-python/)[5](https://www.tutorialspoint.com/data_structures_algorithms/naive_pattern_searching_algorithm.htm).

```c
#include <stdio.h>
#include <string.h>

// Function to perform naive string matching
void naiveStringMatch(char *text, char *pattern) {
    int textLength = strlen(text);
    int patternLength = strlen(pattern);
    int found = 0;
    int steps = 0; // Counter to keep track of the number of steps

    // Loop through the text and check for matches
    for (int i = 0; i <= textLength - patternLength; i++) {
        int j;

        // Check if the pattern matches at this position
        for (j = 0; j < patternLength; j++) {
            steps++; // Increment step counter for each comparison
            if (text[i + j] != pattern[j]) {
                break;
            }
        }

        // If the pattern matches, print the starting index
        if (j == patternLength) {
            printf("Pattern found at index %d\n", i);
            found = 1;
        }
    }

    // If no match is found
    if (!found) {
        printf("Pattern not found in the text.\n");
    }

    // Print the number of steps it took to match
    printf("Number of steps: %d\n", steps);
}

int main() {
    char text[100], pattern[50];

    // Input the text
    printf("Enter the text: ");
    fgets(text, sizeof(text), stdin);

    // Remove trailing newline character if present
    size_t len = strlen(text);
    if (len > 0 && text[len - 1] == '\n') {
        text[len - 1] = '\0';
    }

    // Input the pattern
    printf("Enter the pattern to search: ");
    fgets(pattern, sizeof(pattern), stdin);

    // Remove trailing newline character if present
    len = strlen(pattern);
    if (len > 0 && pattern[len - 1] == '\n') {
        pattern[len - 1] = '\0';
    }

    // Call the naive string match function
    naiveStringMatch(text, pattern);

    return 0;
}
```