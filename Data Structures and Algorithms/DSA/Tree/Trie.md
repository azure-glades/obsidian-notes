*Definition:* 
	A specialized tree-like data structure used for efficiently storing and retrieving a dynamic set of strings. Each node in a trie represents a single character of the string, and the path from the root to any node corresponds to a prefix of the strings stored in the trie.
- A tree used to efficiently store a set of words/strings, using minimal memory
- The root node is null and does not store any data
- Trie comes from Re*trie*val

The path from the root to any leaf of the Trie lists out a string.
### 1. Classification
- **Standard trie**: Each node stores a character
- **Compressed trie**: Each node stores a character or a set of character.
	- All internal nodes have at least 2 or more children
- **Compact trie:** A modified compressed trie where each node contains a segment of a word represented as 3 integers $(i, j, k)$.
	- Suppose we have a list of words stored in an array/set as $A_0, A_1, A_2, A_3$.
	- Suppose $A_0 = dark$.
	- A segment "ark" of the word "dark" is represented as (0, 1, 3). Watch [GRS](https://www.youtube.com/watch?v=1Wn1aZ_r_Dw&list=PLtg1mdkLERgkJX3pOmHAqf-Gwp5P5PcKh&index=60) 
	- Therefore,
		- i = Index of the word in the set/array
		- j = index of the first character of the segment, from its word
		- k = index of last character of the segment, from its word
- **Suffix tree:**  A compressed tree for all the suffixes of a word
	- Ex:
		- Suffixes of minimize:
			e
			ze
			ize
			mize
			imize
			nimize
			inimize
			minimize
### 2. Applications
- NLP
- Spell checkers
- Auto suggest
- Auto completions
- Dictionaries in word processors
- Search engines
- Auto command completion
- DNA sequencing (because a lot of DNA is repetitive)
