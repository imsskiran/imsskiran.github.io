Objective:
* Mine the text documents and find recurring topics across them

Chosen unsupervised methodology:
* LDA

Limitations of LDA followed by solutions
* Purely based on frequency of tokens 
	- Tokens from industry specific nomenclature are likely to repeat across docs and hence the topics, whereas in reality they add little to no value to the definition of topic
	- Their frequency might dominate so much to an extent that multiple topics can have these tokens among the top characteristic set. This could result in certain docs having enhanced probabilties for multiple topics even if those topics are not relevant
	-  Removal of such words is not very straigtforward - these tokens need not be among the top percentile of most repeating ones
* Solution
	- Basic text processing steps - stop words removal, lemmitization and removal of tokens in top 10 and bottom 10 percentile frequencies
	- Unigrams may not capture true meaning conveyed, hence generate bigrams or trigrams as per the problem, that capture the entities and context of topics better
	- Now compute the frequency of remaining tokens and identify the top N. These could be the industry specific nomnenclature potentially
	- Now identify all tokens that are close to these domain tokens based on levenshtine distance, all tokens closer to the domain tokens can be removed from corpus based on a threshold
	- After building the LDA model, identify the commonly occuring ngrams across the topics, remove them from corpus and retrain LDA

* Number of topics is a parameter
	- LDA tries to identify as many topics as the user states. This could lead to huge overlap among topics as the number increases
	- Without optimal number known, the real exhaustive set of topics would never be identified

* Solution
	 - Gensim LDA module has a built-in coherence score - it quantifies the loyalty between a topic and its top N tokens
	 - Also, compute pair-wise jaccard similarity for top N (20) tokens of each topic, then compute the mean jaccard similarity score
	 - Then using pyLDAvis package, find the coordinates of each topic on the transformed 2D space. Compute the pair-wise euclidean distance and then the mean euclidean distance
	 - Coherence score should be higher, jaccard similarity should be close to zero and euclidean score should be the highest. Such number of topics is optimal because, the topics are dissimilar and have reasonable loyalty with corresponding tokens

* Topics have to be manually read and interpreted from top N tokens. 
	- Cannot spit a subset of 5 or 6 tokens to headline the topic

* Solution
	- Define a weighing mechanism to quantify the importance of each token. This can be based on POS of words in ngram. A noun-noun, noun-verb (vice-versa) tokens are meant to indicate some sort of call to action
	- Apart from POS score, use the  frequency in topic / total frequency ratio of a bigram estimated by pyLDAvis or compute them manually
	- A combination of these two metrics can filter top 5/6 ngrams that would headline the topic