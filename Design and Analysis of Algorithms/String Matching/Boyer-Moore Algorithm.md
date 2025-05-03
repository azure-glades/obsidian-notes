The **Boyer-Moore algorithm** is a highly efficient string matching algorithm that uses two heuristics: the **bad character heuristic** and the **good suffix heuristic**. It compares the pattern against the text from right to left and skips sections of the text instead of checking every character, making it much faster than naive string matching in many cases.
## Premise
- The Boyer-Moore algorithm is designed to minimize the number of comparisons by skipping sections of the text based on mismatches.
- It uses precomputed tables (bad character and good suffix) to determine how far the pattern can be shifted when a mismatch or partial match occurs.
- By starting comparisons from the rightmost character of the pattern, the algorithm can often skip large portions of the text.
## Complexity
- **Time Complexity**:
  - **Best case**: O(n/m), where `n` is the length of the text and `m` is the length of the pattern.
  - **Worst case**: O(n + m), when the pattern is repetitive or the text contains many mismatches.
- **Space Complexity**: O(alphabet size + pattern length) for the bad character and good suffix tables.
## Steps of the Algorithm
### 1. Preprocessing
#### a. **Bad Character Table**:
   - For every character in the alphabet, store the index of its last occurrence in the pattern.
   - If a character does not appear in the pattern, set its value to `-1`.
   - The bad character heuristic determines how far the pattern can be shifted when a mismatch occurs.
#### b. **Good Suffix Table**:
   - Identify all suffixes of the pattern that match substrings of the pattern itself.
   - For each suffix, calculate the shift value to align the next occurrence of the suffix (or prefix) with the text.
   - If no such occurrence exists, align the pattern beyond the mismatch.
### 2. Search
- Start by aligning the pattern with the leftmost part of the text.
- Compare characters of the pattern and text from right to left.
- If all characters match, print the starting index of the match.
- If a mismatch occurs:
  - Use the **bad character table** to determine how far to shift the pattern based on the mismatched text character.
  - Use the **good suffix table** to determine how far to shift the pattern based on the matched suffix.
  - Shift the pattern by the maximum value from the two heuristics.
- Repeat the process until the pattern shifts beyond the end of the text.

In C
```c
#include <stdio.h>
#include <string.h>
#define ALPHABET_SIZE 256

// Function to create the bad character heuristic table
void buildBadCharTable(char *pattern, int patternLength, int badCharTable[ALPHABET_SIZE]) {
    for (int i = 0; i < ALPHABET_SIZE; i++) {
        badCharTable[i] = -1; // Initialize all characters to -1
    }

    for (int i = 0; i < patternLength; i++) {
        badCharTable[(unsigned char)pattern[i]] = i; // Store the last occurrence of each character
    }
}

// Function to create the good suffix heuristic table
void buildGoodSuffixTable(char *pattern, int patternLength, int goodSuffixTable[]) {
    int i = patternLength, j = patternLength + 1;
    int borderPositions[patternLength + 1]; // Temporary array to store borders

    borderPositions[i] = j;
    while (i > 0) {
        while (j <= patternLength && pattern[i - 1] != pattern[j - 1]) {
            if (goodSuffixTable[j] == 0) {
                goodSuffixTable[j] = j - i;
            }
            j = borderPositions[j];
        }
        i--;
        j--;
        borderPositions[i] = j;
    }

    // Fill remaining entries in the goodSuffixTable
    j = borderPositions[0];
    for (i = 0; i <= patternLength; i++) {
        if (goodSuffixTable[i] == 0) {
            goodSuffixTable[i] = j;
        }
        if (i == j) {
            j = borderPositions[j];
        }
    }
}

// Function to perform Boyer-Moore string matching
void boyerMooreSearch(char *text, char *pattern) {
    int textLength = strlen(text);
    int patternLength = strlen(pattern);

    int badCharTable[ALPHABET_SIZE];
    int goodSuffixTable[patternLength + 1];

    // Build the bad character table
    buildBadCharTable(pattern, patternLength, badCharTable);

    // Build the good suffix table
    memset(goodSuffixTable, 0, sizeof(goodSuffixTable));
    buildGoodSuffixTable(pattern, patternLength, goodSuffixTable);

    int steps = 0; // Counter for steps during the matching process
    int shift = 0; // Start aligning pattern at the beginning of the text

    while (shift <= textLength - patternLength) {
        int j = patternLength - 1;

        // Compare pattern from right to left
        while (j >= 0 && pattern[j] == text[shift + j]) {
            j--;
            steps++;
        }

        if (j < 0) {
            // Match found
            printf("Pattern found at index %d\n", shift);
            shift += goodSuffixTable[0];
        } else {
            // Use the larger shift value between bad character and good suffix heuristics
            steps++;
            int badCharShift = j - badCharTable[(unsigned char)text[shift + j]];
            int goodSuffixShift = goodSuffixTable[j + 1];
            shift += (badCharShift > goodSuffixShift) ? badCharShift : goodSuffixShift;
        }
    }

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

    // Call the Boyer-Moore search function
    boyerMooreSearch(text, pattern);

    return 0;
}
```
## Example
### Given:
- **Text**: "hello world"
- **Pattern**: "world"
### Steps:
1. Preprocess the pattern:
   - **Bad Character Table**:
     ```
     'w' -> 0
     'o' -> 1
     'r' -> 2
     'l' -> 3
     'd' -> 4
     All other characters -> -1
     ```
   - **Good Suffix Table**:
     ```
     Suffix shifts based on pattern structure.
     ```
2. Start matching:
   - Align "world" with "hello".
   - Compare from right to left. Mismatch occurs at 'd' and 'o'.
   - Use the bad character and good suffix tables to determine the shift.
   - Repeat until a match is found or the pattern shifts beyond the text.

### Result:
The pattern "world" is found at index 6.

## Advantages
- Extremely efficient for long texts and relatively small patterns.
- Reduces unnecessary comparisons by leveraging precomputed tables.
- Works well with larger alphabets.
## Disadvantages
- Preprocessing the pattern is complex and requires extra space.
- Not ideal for very short patterns or small alphabets.
## Use Cases
- Searching for substrings in large texts.
- DNA sequence matching.
- Text editors and word processors for find-and-replace functionality.