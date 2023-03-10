## Introduction
{:#introduction}
Optimizing the order in which database management systems execute joins is a well-studied topic in database literature. The order in which joins are executed significantly impacts the performance characteristics of queries. 
SPARQL endpoints processes user queries for one specific database on the serverside. Endpoints over semantically stable 
<!-- (Not sure how correct sementically stable datasets is, I mean to say datasets that don't undergo drastic changes in meaning or subject)  -->
datasets, like wikidata, can benefit from an algorithm that optimizes queries based on previous experiences. These algorithms can learn to produce better join plans, reducing server costs. \\
In recent literature, reinforcement learning(RL)-based optimizers that use greedy search procedures guided by a learned value function achieve impressive results in relational databases. [Neo](cite:cites marcus2019neo) shows that learned optimizers can match and even surpass state-of-the-art commercial optimizers.  \\
In SPARQL, machine learning is primarily used to predict query performance, however these [approaches](cite:cites hasan2014machine) use supervised machine learning with a static dataset of query executions and use methods that exploit this. Learned query optimizers use reinforcement learning to dynamically generate training data by exploring the search space, complicating the use of existing query performance prediction methods. 
The [April](cite:cites wang2020april) optimizer uses reinforcement learning for query optimization, however its approach to encoding the query state into a feature vector is relatively simplistic and the paper does not report any performance characteristics. 
We fill this gap in the literature by exploring a fully-fledged RL-based query optimizer for SPARQL join order optimization. We expect RL-based approaches to perform well for static datasets with a public SPARQL endpoint.
We model our approach after the [RTOS](cite:cites yu2020reinforcement) optimizer for relational queries, which uses Tree-LSTM to predict the expected latency of a join plan. 

<!-- 
{:.comment data-author="RT"}
The structure of the intro is already quite good, but I think we can improve things.
The introduction is currently one large paragraph, so I would suggest splitting it up, where each paragraph has its own focus.
Also, we need a better motivation for this work than just "wouldn't it be nice to do this?".
We can use the DBpedia/Wikidata use case here, as something we would like to optimize.

{:.comment data-author="RT"}
Suggestion for a new intro structure:
- Talk about SPARQL querying in general, and introduce the DBpedia/Wikidata use case.
- The use of RL in RDBs, and the benefits they give there.
- The potential of RL in SPARQL, and that you investigate it. -->
