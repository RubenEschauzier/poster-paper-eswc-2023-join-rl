## Related work
{:#relatedwork}
In this section, we will first introduce the relational approach which we will partially adapt to SPARQL optimization, then show methods that use machine learning to predict SPARQL query performance characteristics, and finally discuss the [April](cite:cites wang2020april) optimizer.

### Reinforcement learning with Tree-structured long short-term memory for join Order selection
{:#rtos}
In [](cite:cites yu2020reinforcement) the authors introduce a query optimizer based on Reinforcement learning with Tree-structured long short-term memory for join Order selection (RTOS). The optimizer uses tree-LSTM to approximate the Q-function of the join plan search problem and guide its greedy search. RTOS represents the current environment state as a tree, where leaf nodes represent the tables and columns present in join relations, intermediate nodes the result of joining two relations, and finally, the root node represents the (partial) join plan. This partial join plan is concatenated with a query representation and fed into a multilayer perceptron to obtain the estimated Q-value of the current (partial) join plan. RTOS uses fixed-size vectors based on the attributes present in the database tables to create the numerical vectors representing tables, columns, and the query. The vectors representing joins in the join plan are obtained by iteratively applying an N-ary tree-LSTM [](cite:cites tai2015improved) to the representations of the columns and tables used in the join. 

### Machine learning-based SPARQL query performance prediction
{:#mlbased}
In SPARQL, machine learning is ued for performance prediction of complete query plans. The authors of [](cite:cites hasan2014machine, zhang2018learning, casalssparql) use supervised machine learning. First, they generate a static dataset of queries and their execution times. They then use this dataset to train and validate their model. 
<!-- While the exact implementation details of each paper are different they follow similar featurization procedures.  -->
The papers encode query-level features, like algebraic characteristics and the graph shape of the query. To encode graph patterns, they deploy the $$k$$-medoids algorithm based on the edit distance between query graphs, and calculate the distance to the $$k$$ medoids for each query. In [](cite:cites casalssparql) they include the query plan tree and enrich each node in the tree with semantic information obtained from an existing query optimizer. These approaches do not translate to reinforcement learning. In reinforcement learning, we iteratively generate our dataset by exploring the agent's environment, which makes using k-medoids to determine graph shape clusters impractical.

### April
{:#april}
[April](cite:cites wang2020april) uses deep Q-learning to optimize basic graph pattern queries. They encode their queries using a one-hot encoded vector that denotes whether a predicate is involved in a join relation. We expect this approach to scale poorly for large datasets due to the rapidly increasing size of the input vector. Note that the authors do not show benchmark performance, so we are unsure of the speed of this approach.
