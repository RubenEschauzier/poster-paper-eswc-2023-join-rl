## Conclusion
{:#conclusion}
In this paper, we explore a novel RL-based join plan optimizer for SPARQL endpoint query execution.
Initial experiments show that the model can generate better join plans than existing cardinality-based optimizers for 7 query templates of the WatDiv benchmark. 
We plan to improve the model by enhancing data efficiency during training. 
We propose to use query _time-outs_ based on existing query optimizers to reduce time spent executing bad query plans.
Additionally, we propose to use _experience replay_ to reuse query execution information during training. 
For future work, we should include information on how triple pattern result sets connect to other result sets in the query and extend our approach to more complex SPARQL operations.