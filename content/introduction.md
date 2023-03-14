## Introduction
{:#introduction}
Optimizing the order in which database management systems execute joins is a well-studied topic in database literature.
<span class="comment" data-author="RV">After such a sentence, you'd normally expect a bunch of references; but given that this is a poster paper, we don't have the space for it. Suggestion: combine sentences 1 and 2, with a focus on 2: the fact that it impacts performance is key. Is there perhaps a reference we already use that can be used to back this point up?</span>
The order in which joins are executed significantly impacts the performance characteristics of queries. 
<del class="comment" data-author="RV">A SPARQL endpoint processes user queries for one specific database on the server side.</del>
<span class="comment" data-author="RV">(commonly known)</span>
SPARQL endpoints over <del class="comment" data-author="RV">semantically stable</del> 
<ins class="comment" data-author="RV">consistently evolving</ins>
<!-- (Not sure how correct sementically stable datasets is, I mean to say datasets that don't undergo drastic changes in meaning or subject)  -->
datasets, like Wikidata, can benefit from an algorithm that optimizes queries based on previous experiences. These algorithms can learn to produce better join plans <del class="comment" data-author="RV">, reducing server costs</del>.

<span class="comment" data-author="RV">Alternate take for the above, that emphasizes <q>previous experiences</q> more:</span>
<ins class="comment" data-author="RV">Different signals exist to inform an appropriate choice of join order, such as cardinalities. One such signal is _previous experiences_, where previous queries over datasets are used as a predictor to produce better join plans for future queries.</ins>

In recent literature, reinforcement learning(RL)-based optimizers that use _greedy search procedures_, guided by a learned _value function_, achieve impressive results in relational databases. [Neo](cite:cites marcus2019neo) shows that learned optimizers can match and even surpass state-of-the-art commercial optimizers.

In SPARQL, machine learning is primarily used to predict query performance, these [approaches](cite:cites hasan2014machine) use supervised machine learning with a static dataset of query executions. Learned query optimizers use reinforcement learning to dynamically generate training data by exploring the search space, complicating the use of existing query performance prediction methods. 
The [April](cite:cites wang2020april) optimizer uses reinforcement learning for query optimization, with a one-hot [encoded](cite:cites muller2016introduction) feature vector denoting the presence of RDF terms in joins. We expect this to scale poorly for RDF graphs with many unique RDF terms. Furthermore, the paper does not report any performance characteristics. 
We fill this gap in the literature by exploring a fully-fledged RL-based query optimizer for SPARQL join order optimization. We expect RL-based approaches to perform well for static datasets with a public SPARQL endpoint.
We model our approach after the [RTOS](cite:cites yu2020reinforcement) optimizer for relational queries, which uses <ins class="comment" data-author="RV">the</ins> Tree-LSTM <ins class="comment" data-author="RV">algorithm ???</ins> <span class="comment" data-author="RV">to give a sense of what exactly this thing is</span> to predict the expected latency of a join plan. 

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
