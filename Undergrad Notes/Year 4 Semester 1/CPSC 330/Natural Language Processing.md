- Interpreting language the way that humans do is difficult for computers
- "Panini" was the name of an ancient linguist, but also the name of a sandwich
- As a computer, how do you know which one of these meanings is more commonly associated with that word?
- Context is very important for understanding human language, both the context within the sentence and also the social context surrounding that language
- We implicitly understand that words that appear in similar contexts have similar meanings, in linguistics this is called the distributional hypothesis
- Natural language processing is a major field of artificial intelligence and machine learning, and covers an extremely broad range of topics
- Using this linguistic approach, processes like sentence embedding representation groups words on a vector space based on their similarities in context
- Words and sentences that are similar are closer together in the vector space
- Doing this ourselves is beyond the scope of the course, this is usually done with advanced methods like deep neural networks
- Traditionally we have used Euclidean distance to find the distance between items in vector space, but this scales poorly to higher dimensions
- Other methods like dot product and cosine distance work better on sparse data
- These are metrics of similarity, the higher the dot product the higher the similarity
- Cosine distance is the normalized version of dot product which makes the result more interpretable
- Since vectors can be represented geometrically, we can calculate geometric differences between them which creates a result within a recognizable range
- Cosine can only be between 0 and 1, so it's easier to interpret

**Word Embeddings**

- There are many pre-trained word embedding systems created by major institutions like Google and Stanford, we can use these in our models
- GloVe and word2vec are two of the most popular and effective algorithms, we'll use word2vec
- Word embeddings let us look at words associated with other words, or even calculate the similarity between specific pairs of words
- We can also use algebraic operations on vectors to find new vectors
- For example, if you calculate the value of the King vector minus the Man vector plus the Woman vector, the resulting vector is very close to the vector for Queen
- This is a very good sign, because this suggests that this algorithm understands analogies
- Of course, since these embeddings are based on public information, embeddings tend to represent social biases
- The closest pairing from "woman" compared to "man" and "computer science" is "housewife"
- As a result, most modern embedding systems debias specific associations like these
- Another popular algorithm we may use is spaCy, which is trained on a much larger corpus while word2vec was trained on Google News
- One other thing we can do is document embedding, which averages the word embeddings of a full document

**Topic Modelling**

- This is a method that examines a large corpus and then uses NLP to group documents in the corpus by topic
- This uses unsupervised machine learning strategies, and is very useful for sorting through large amounts of data
- Similar to what we did earlier, this outputs unlabelled clusters with common words within that cluster, and then we can manually label the clusters
- Topic modelling typically requires a K hyperparameter to determine how many topics to find
- In Scikit Learn, we usually use the LDA model to perform topic modelling
- This is fairly easy to do, you just take your dataset and preprocess it with bag of words representation, and then feed it into the LDA model
-