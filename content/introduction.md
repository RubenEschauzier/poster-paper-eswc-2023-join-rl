## Introduction
{:#introduction}

Optimizing the order in which database management systems execute joins is a well-studied topic in database literature because it heavily influences the performance characteristics of queries [](cite:cites yu2020reinforcement).
SPARQL endpoints over consistently evolving datasets, like Wikidata, can benefit from an algorithm that optimizes queries based on previous experiences. 
Different signals exist to inform an appropriate choice of join order, such as cardinalities. One such signal is _previous experiences_. 
We use previous experiences as a predictor to produce better join plans for future queries. \\
In recent literature, reinforcement learning(RL)-based optimizers that use _greedy search procedures_, guided by a learned _value function_, achieve impressive results in relational databases. 
[Neo](cite:cites marcus2019neo) shows that learned optimizers can match and surpass state-of-the-art commercial optimizers. \\
In SPARQL, machine learning is primarily used to predict query performance. These [approaches](cite:cites hasan2014machine, zhang2018learning, casalssparql) use supervised machine learning with a static dataset of query executions.
Learned query optimizers use reinforcement learning to dynamically generate training data, complicating the use of existing query performance prediction methods. 
The [April](cite:cites wang2020april) optimizer uses reinforcement learning for query optimization, with a one-hot [encoded](cite:cites muller2016introduction) feature vector denoting the presence of RDF terms in joins. However, the paper does not report any performance characteristics. \\
We fill this gap in the literature by exploring a fully-fledged RL-based query optimizer for SPARQL join order optimization on SPARQL endpoints. Endpoints query over the same dataset, likely making the previous experience signal stronger for join order optimization.
We model our approach after the [RTOS](cite:cites yu2020reinforcement) optimizer for relational queries, which uses Tree-LSTM neural [networks](cite:cites tai2015improved) to predict the expected latency of a join plan.