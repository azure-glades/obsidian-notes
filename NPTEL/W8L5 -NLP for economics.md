NLP (**Natural Language Processing**) is a field of AI that gives computers the ability to understand, interpret, and generate human language. It begins with **text mining**, which involves organizing and preparing text data from a large body of text, or **corpus**, for analysis.

---

### Core Concepts

* **Words and Vocabulary:** A corpus is a collection of documents, which are sequences of **word tokens**. The **vocabulary** is the set of all unique words in the corpus.
* **Challenges:** The main challenges in NLP are representing a word or document's **meaning (semantics)** and **grammatical rules** in a mathematical format that a computer can understand.

---

### Key NLP Tasks

NLP tasks range from simple to complex, including:

* **Part-of-Speech (POS) Tagging:** Identifying the grammatical role of each word (e.g., noun, verb, adjective).
* **Word Sense Disambiguation:** Determining the correct meaning of a word with multiple definitions based on its context.
* **Named Entity Recognition (NER):** Identifying and classifying proper nouns, such as names of people, organizations, and locations.
* **Sentiment Analysis:** Determining the emotional tone of a text (positive, negative, or neutral). This is a complex task because it must account for sarcasm and context.
* **Topic Modeling:** An unsupervised method for discovering abstract "topics" in a corpus. It models each document as a mixture of topics and each topic as a mixture of words. This can help researchers quickly find the main themes in a large collection of documents without reading them all.
* **Summarization:** Condensing a long text into a shorter, coherent summary.

---

### NLP Methods

Traditionally, NLP tasks were solved using **statistical methods**, such as:

* **N-gram Models:** These models predict the next word in a sequence based on the probability of it following the previous one or two words.
* **Latent Variable Models:** These use probabilistic models like Hidden Markov Models (HMMs) or Latent Dirichlet Allocation (LDA) to infer hidden, or **latent**, information (e.g., a word's part of speech or topic) from the observable text.

However, since 2012, **neural network-based methods** have become the state of the art.

* **Word Embeddings:** This is a key innovation where each word is represented as a dense numerical vector. The goal is to create these vectors in a way that the geometric distance between them reflects their semantic similarity. For example, the vectors for "cat" and "kitten" would be closer than the vectors for "cat" and "house." Models like **Word2Vec** learn these embeddings by predicting nearby words in a context.
* **Attention and Transformers:** Recent advances in neural networks, particularly the **Transformer** architecture and the concept of **attention**, have revolutionized language modeling. Attention mechanisms allow a model to weigh the importance of different words in a sentence when processing a particular word, giving it a much richer understanding of context. Models like **BERT** use this bidirectional attention to create powerful language representations.

---

### Applications in Economics

NLP offers a huge potential for economic analysis by using text as a data source.

1.  **Reading Policy Documents:** Topic modeling can be used to automatically analyze large collections of policy documents, like urban resilience plans, to identify key themes and topics. This saves policymakers time and provides a quick overview of the most discussed issues.
2.  **Tracking Economic Sentiment:** By analyzing news articles and social media data, researchers can gauge public sentiment on issues like **inflation expectations** or **stock prices**. Studies have shown that a model's ability to predict stock prices improves significantly when it incorporates sentiment from news and social media.
3.  **Recommender Systems:** E-commerce and service platforms use **sentiment analysis** and **topic modeling** on user reviews to understand which aspects of a product or service are most important to consumers (e.g., food quality vs. customer service in a restaurant review). This information is then used to provide more personalized recommendations.
4.  **Economic Worth of Words:** New research is exploring how to create word embeddings that reflect a word's "economic worth." This allows researchers to analyze how economic concepts are discussed and how their meaning evolves over time.
5.  **Poverty Mapping:** Geographically tagged articles (e.g., from Wikipedia) can be analyzed using NLP to extract information about a region's economic well-being. This text-based data can be combined with other data sources like satellite imagery in a **multimodal approach** to create detailed economic maps, similar to what's done with computer vision.