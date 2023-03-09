## Method
{:#method}
The RL-based optimizer builds a join plan by greedily adding joins that minimize the estimated execution time of the query to the join plan untill all result sets are joined. We estimate the execution time of the query using a neural network trained on previous query executions. The neural network training objective is minimizing the squared difference between predicted and actual query execution time. The neural network is fed a numerical representation of the current join plan as an input.

### Join plan representation
{:#representation} 
Like in [RTOS](cite:cites yu2020reinforcement), we represent join plans as a tree that we build from the bottom up. Each leaf node represents the result set of a triple pattern, and all other nodes represent joining two result sets. The result sets of triple patterns are represented using their cardinality, the presence and location of variables, named nodes and literals, and a dense vector representing the predicate. We learn the dense vector representations by applying [RDF2Vec](cite:cites ristoski2016rdf2vec) to the input RDF graph. The predicate vectors contain semantic information relating to the encoded predicate. We obtain the representations for intermediate joins by applying an N-ary Tree-LSTM on the result sets representations involved in the join. Finally, at the (partial) join plan root node, we apply a Child-Sum Tree-LSTM [operation](cite:cites tai2015improved) to all unjoined result sets to obtain the join plan representation. This representation is then fed into the neural network, which predicts the estimated query execution time.

### Data efficiency & SPARQL specific adjustments
{:#dataefficiency}
The model initially randomly generates query plans, which are often slow. Query execution is the most expensive part of our training procedure, thus at the start of model training we are limited by the slow query plans.
To account for this, we apply two data efficiency techniques. First, we include a time-out that is set according to existing optimizers. We effectively truncate our optimization variable, while ensuring the optimal query plan will not reach the time-out. Second, we use [experience replay](cite:cites lin1992self) to reuse previous query executions. In experience replay, we store a buffer of the $$N$$ most recent query executions. Executing queries is expensive, so by applying experience replay we can reuse query executions to further optimize our model. \\
Relational RL-based optimization approaches use one-hot [encoding](cite:cites muller2016introduction) of database attributes to create feature vectors. However, the wikidata graph has over a 100 million unique entries. This would create unwieldy vectors, thus we do not use one-hot encoding in our approach. This complicates creating informative features but should improve scalability. 


### Open Challenges
{:#openchallenges}
Our optimizer is missing features that are vital to query optimization. We do not encode the connections between triple patterns, these encodings should reflect the different types of connections between triple patterns, like object-object, subject-subject, object-subject, and subject-object. These different edge types make using a simple adjacency matrix difficult. Furthermore, our approach can only optimize basic graph patterns, in future work, this approach can be extended to more complex SPARQL query operations.
