An encoding algorithm. Uses frequency of occurance of characters and re-represents them as shorter codes to save space. Simple substitution
- The size of the compressed file depends on the codes chosen to represent characters
- Codes can be fixed-length, where every character gets the same length code
- Codes can be variable length, where the code a character gets depends on how commonly it occurs, and usually shorter codes are given for more frequent characters
- The efficiency of compression depends heavily on the codes chosen
- The codes cannot be prefixes of other codes

Codes are represented as binary trees (decision tree). An efficient encoding system is always a full binary tree. The huffman encoding tree is a full binary tree
- Leaf nodes are the characters (with their freq)
- Internal nodes store the sum of frequencies of their child nodes
- Each node is hence a decision, with 0 → right child, 1 → left child. The tree is traversed when encoding and decoding

Huffman’s algorithm is a [[Greedy Algorithms]] that constructs an optimal prefix-free code
- Algorithm always chooses the first 2 minimum freq elements (choice is greedy)

1. Add characters and frequencies to a min-priority queue
2. Pop the first two elements, and join them into a full binary tree (parent node is sum of freq of child nodes)
3. Push the new node into the min-priority queue
4. Repeat

``` al
FUNC huffmanEncoding(chars[], n)
//INPUT: chars is the set of chars with freq
	pQ = getPriorityQueue(chars)
	FOR (i<n, i:0 -> n)
		x = getMin(pQ);
		y = getMin(pQ);
		z.left = x
		z.right = y
		z.freq = x.freq + y.freq
		insert(pQ, z)
	END-FOR
	root = getMin(pQ)
RETURN root
```
