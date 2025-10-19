The **Horspool algorithm** is an efficient string matching algorithm that uses a shift table to skip unnecessary comparisons when searching for a pattern in a given text. It improves the naive approach by focusing on the end of the pattern and utilizing mismatched characters to determine how far to shift the pattern.
## Premise
- It is built upon the Boyer-Moore algorithm but simplifies it by using only the "bad character heuristic."
- The algorithm avoids checking every character of the text by precomputing a **shift table**, which determines how far the pattern can be moved when a mismatch occurs.
## Complexity
- **Time Complexity**:
  - **Best case**: O(n/m), where n is the length of the text and m is the length of the pattern.
  - **Worst case**: O(n\*m), in rare cases with repeated patterns or poor shift table values.
- **Space Complexity**: O(alphabet size) for the shift table.
## Steps of the Algorithm
1. **Build the Shift Table**:
   - Create a table (array) for all possible characters in the alphabet (e.g., ASCII characters).
   - Initialize all entries in the table to the length of the pattern.
   - For each character in the pattern (except the last one), compute the shift value as:
     ```
     shift[character] = length of pattern - 1 - index of character
     ```
2. **Begin the Search**:
   - Start aligning the pattern with the leftmost part of the text.
   - Compare the pattern with the text, starting from the last character of the pattern and moving backward.
3. **Handle Mismatches**:
   - If there is a mismatch, use the shift table to determine how far to move the pattern. The shift value corresponds to the mismatched character in the text.
4. **Handle Matches**:
   - If all characters of the pattern match the text, record the index of the match.
   - Then shift the pattern by one position (or as determined by the shift table).
5. **Repeat**:
   - Continue the process until the pattern shifts beyond the end of the text.
```al
FUNCTION horspool_search(text, pattern)
//INPUT: text and pattern to be searched
//OUTPUT: index of pattern if found
	shift_table = getShiftTable(pattern)
	m = LENGTH(pattern)
	n = LENGTH(text)
	i = m
	WHILE(i < n)
		k = 0
		WHILE( k < m-1 AND patten[m-k-1] == text[i-k])
			k++ //check from back of the pattern
		IF (k == m)
			return i-m+1 //pattern has been found
		ELSE
			i = i + shift_table[text[i]] //shift by the conflicting value
RETURN

FUNCTION getShiftTable(pattern)
//INPUT: pattern
//OUTPUT: shift table
	m = LENGTH(pattern)
	//assume texts have only ASCII which goes till 256
	FOR (i< 256, i:0 -> 256)
		table[i] = m     // inits default shift
	FOR (i < m-1, i:0 -> m-1)
		table[pattern[i]] = m - i - 1    // sets shift values
RETURN table
```
In C
```c
#include <stdio.h>
#include <string.h>
#define ALPHABET_SIZE 256

// Function to create the shift table
void buildShiftTable(char *pattern, int patternLength, int shiftTable[ALPHABET_SIZE]) {
    for (int i = 0; i < ALPHABET_SIZE; i++) {
        shiftTable[i] = patternLength; // Default shift value
    }

    for (int i = 0; i < patternLength - 1; i++) {
        shiftTable[(unsigned char)pattern[i]] = patternLength - 1 - i;
    }
}

// Function to perform Horspool string matching
int horspoolSearch(char *text, char *pattern) {
    int textLength = strlen(text);
    int patternLength = strlen(pattern);
    int shiftTable[ALPHABET_SIZE];
    int steps = 0; // Counter for steps during the matching process

    // Build the shift table
    buildShiftTable(pattern, patternLength, shiftTable);

    int i = patternLength - 1; // Start from the end of the pattern
    while (i < textLength) {
        int j = patternLength - 1;
        while (j >= 0 && pattern[j] == text[i - (patternLength - 1 - j)]) {
            j--;
            steps++;
        }

        if (j < 0) {
            printf("Pattern found at index %d\n", i - patternLength + 1);
            printf("Number of steps: %d\n", steps);
            return i - patternLength + 1; // Return the starting index of the match
        } else {
            steps++;
            i += shiftTable[(unsigned char)text[i]]; // Shift the pattern
        }
    }

    printf("Pattern not found.\n");
    printf("Number of steps: %d\n", steps);
    return -1; // No match found
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

    // Call the Horspool search function
    horspoolSearch(text, pattern);

    return 0;
}
```

## Advantages
- Simple and efficient for large texts and small patterns.
- Easy to implement compared to other advanced algorithms like Boyer-Moore.
## Disadvantages
- Performs poorly with small alphabets or repetitive patterns.
- Works only with the bad character heuristic and does not use the good suffix heuristic.
## Use Cases
- Searching for substrings in large texts.
- DNA sequence analysis.
- Plagiarism detection.
