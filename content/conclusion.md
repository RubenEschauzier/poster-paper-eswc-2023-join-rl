## Conclusion
{:#conclusion}
In this poster paper we explore a novel RL-based join plan optimizer based on Q-learning. We discuss key points required to translate RL-based relational optimizers to SPARQL. 
We will improve sampling efficiency by using experience replay and query time-outs. Additionally, we create feature vectors that do not depend on the number of unique RDF entities in the graph. 
Furthermore, we briefly touch on unsolved problems in our current methodology. The main problems are the absence of triple pattern connection encoding and the restriction of our method to basic graph patterns. 
Finally, we show that a simple version of our approach can find better join plans than existing optimizers. Combined with the previously mentioned improvements, our optimizer should generate highly efficient join plans.
