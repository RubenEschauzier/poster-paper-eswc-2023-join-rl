## Conclusion
{:#conclusion}
<!-- In this poster paper we explore a novel RL-based join plan optimizer based on Q-learning.
<span class="comment" data-author="RV">That's a new word to me, and to some readers; should be mentioned before?</span>
<span class="comment" data-author="RV">The sentences below do not seem to form a coherent paragraph. There's also a variety in grammatical tenses (discuss/will improve/create) that obscure the message: are we analyzing things that we have done? will do? plan to do? that others can do?</span>
We discuss key points required to translate RL-based relational optimizers to SPARQL. 
We will improve sampling efficiency by using experience replay and query time-outs. Additionally, we create feature vectors that do not depend on the number of unique RDF entities in the graph. 
Furthermore, we briefly touch on unsolved problems in our current methodology. The main problems are the absence of triple pattern connection encoding and the restriction of our method to basic graph patterns. 
Finally, we show that a simple version of our approach can find better join plans than existing optimizers. Combined with the previously mentioned improvements, our optimizer should generate highly efficient join plans.
<span class="comment" data-author="RV">Try slightly longer sentences with more connection between them.</span>

<span class="comment" data-author="RV">The conclusion should be what you learn from the analysis of your results. Which is: promising, we should look more into this direction. and then what further research is needed. But don't promise what you will do, explain what should be done and what anyone can do (how they can build on top of this work). There is no need for a summary, this is a very short paper. Should be all about lessons learned, and lessons you still want to learn.</span> -->
In this poster paper we explore a novel RL-based join plan optimizer for SPARQL endpoint query execution. 
Initial experiments using an incomplete version of the model show that the model can generate better join plans than existing, cardinality based, optimizers for 7 query templates. 
We plan to improve the model by enhancing the data efficiency during training. 
We propose to use a query time-outs based on existing query optimizers to reduce time spent executing bad query plans.
Additionally, we propose to use _experience replay_ to reuse query execution information during training. 
For future work, we should include information on how triple pattern result sets are connected to other result sets in the query and extend our approach to more complex SPARQL operations.
