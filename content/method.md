## Method
{:#method}

{:.comment data-author="RT"}
I would use the space here to start with giving a very high-level description of your approach.
And then, you can dive into all the details.
Otherwise, readers will get lost in the details.

In this section, we discuss our RL-based optimizer,
which methods we use to improve data efficiency and tackle SPARQL-specific problems,
and which open challenges remain.

### Featurization of join plans
{:#featurization} 
Like in [RTOS](cite:cites yu2020reinforcement), we represent join plans as a tree that we build from the bottom up. Each leaf node represents the result set of a triple pattern, and all other nodes represent joining two result sets. The result sets of triple patterns are represented using their cardinality, the presence and location of variables, named nodes and literals, and a dense vector representing the predicate. We learn the dense vector representations by applying [RDF2Vec](cite:cites ristoski2016rdf2vec) to the input RDF graph. The predicate vectors contain semantic information relating to the encoded predicate. We obtain the representations for intermediate joins by applying an N-ary Tree-LSTM on the result sets representations involved in the join. Finally, at the (partial) join plan root node, we apply a Child-Sum Tree-LSTM operation

{:.comment data-author="RT"}
Citation needed for this operation?

to all unjoined result sets to obtain the join plan representation. At each optimization step, we add the join with the highest negative Q-value, estimated using our join plan representation. When the join plan is complete, we record the execution time of the query and train the model to minimize the MSE between query execution time and predicted Q-value.

{:.comment data-author="RT"}
Ok, the section above is quite dense, and may be difficult for non-RL-experts to follow.
One option might be to add a figure to illustrate the different steps, but we may not have the space for this.
Another option is to make the description more high-level.
Or we could also just leave it as-is, as it's probably ok for a poster.
Not sure about this one, just wanted to raise this concern :-)


<!-- The optimizer chooses the next join by enumerating over all possible virtual root nodes from the current plan. It predicts the Q-value of the added join based on the virtual node representation. The optimizer then chooses the join that minimizes this Q-value and adds it to the join plan. When the join plan is complete, we execute the query and record its execution time. The model, which includes the tree-LSTM layers is then trained to minimize the Mean Squared Error (MSE) between the predicted Q-value and the actual query execution time. -->

### Data efficiency & SPARQL specific adjustments
{:#dataefficiency}

The model starts by generating slow queries, stalling the training procedure.

{:.comment data-author="RT"}
Not sure what you mean with the above.

To account for this, we apply two data efficiency techniques. First, we include a time-out that is set according to existing optimizers. We effectively truncate our optimization variable, while ensuring the optimal query plan will not reach the time-out. Second, we use [experience replay](cite:cites lin1992self) to reuse previous query executions. In experience replay, we store a buffer of the $$N$$ most recent query executions. Executing queries is expensive, so by applying experience replay we can reuse query executions to further optimize our model. \\
The key difference between relational and SPARQL query optimization is the lack of rigid data aggregators in SPARQL and the large number of unique RDF terms present in large RDF graphs.

{:.comment data-author="RT"}
Is this really the key difference? Can you elaborate? Because it's not really clear to me from this sentence.
In my mind, the key difference is that in SPARQL you have way more joins.

So, we do not use one-hot encoding in our featurization approach.

{:.comment data-author="RT"}
Can we have a citation for "one-hot encoding"?

This complicates creating informative features but should improve scalability. 

### Open Challenges
{:#openchallenges}
Our optimizer is missing features that are vital to query optimization. We do not encode the shape of the query,

{:.comment data-author="RT"}
Not sure if "shape" is the right word here. (people may confuse it with things like SHACL and ShEx)
I suspect you just mean the connections between triple patterns?

this shape encoding should be related to the different types of connections between triple patterns, like object-object, subject-subject, object-subject, and subject-object. These different edge types make using a simple adjacency matrix difficult. Furthermore, our approach can only optimize basic graph patterns, in future work, this approach can be extended to more complex SPARQL query operations.
