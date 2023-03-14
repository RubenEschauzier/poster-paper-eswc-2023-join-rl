## Preliminary Results
{:#initialexperiments}
We implemented our optimizer in the TypeScript-based [Comunica query engine](cite:cites taelman2018comunica) and compare it to its default, cardinality-based, optimizer.
We use the WatDiv [benchmark](cite:cites alucc2014diversified) to test our method,
and show performance characteristics for an incomplete version <span class="comment" data-author="RV">why?</span> of the model.
<span class="comment" data-author="RV">Perhaps can be better phrased as <q>note that … is incomplete</q>, depending on what you mean with it</span>

[](#initresults) shows that the undertrained model can find better plans for 7 templates, which we believe we can improve using the data efficiency and SPARQL specific adjustments mentioned in [](#method). 
<!-- The search time of our method is longer than the comunica optimizer, however we expect this to be irrelevant for the large wikidata graph (Should I mention this, removed for the sake of getting to four pages) -->

<figure id="initresults" class="table" markdown="1">

| Query Template           | C1     | C2     | C3     | F1    | F2    | F3    | F4     | F5    | L1    |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Planning (RL)            | 0.5028 | 1.000  | 0.277  | 0.214 | 0.347 | 0.160 | 0.800  | 0.278 | 0.027 |
| Execution (RL)           | 3.116  | 2.577  | 0.583  | 0.100 | 0.090 | 0.062 | 1.906  | __0.059__ |__0.006__ |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Planning (Comunica)      | 0.007  | 0.008  | 0.017  | 0.002 | 0.003 | 0.005 | 0.005  | 0.005 | 0.002 |
| Execution (Comunica)     | __0.076__  | __0.001__  | __0.490__  | __0.001__ |__0.005__ |__0.008__ | __0.012__  | 0.194 | 0.032 |

| Query Template           | L2     | L5     | S1     | S2    | S3    | S4    | S5     | S6    | S7    |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Planning (RL)            | 0.025  | 0.024  | 0.689  | 0.060 | 0.059 | 0.066 | 0.059  | 0.021 | 0.028 |
| Execution (RL)           | __0.001__  | __0.002__  | 2.242  | 0.011 | __0.005__ | __0.000__ | __0.002__  | 0.008 | 0.002 |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Planning (Comunica)      | 0.001  | 0.001  | 0.006  | 0.002 | 0.002 | 0.002 | 0.002  | 0.002 | 0.002 |
| Execution (Comunica)     | 0.006  | 0.007  | __0.139__  | __0.009__ | 0.008  | 0.005 | 0.009 | __0.001__ | __0.000__ |

<figcaption markdown="block">
Comparison of the query optimization and plan execution time, in seconds, of a previous version of our optimizer and the standard [Comunica](cite:cites taelman2018comunica) optimizer, with the faster plan execution in bold.
</figcaption>
</figure>

<span class="comment" data-author="RV">For a poster paper, this space might be better spent on a graph to make it more visual. If you have time.</span>
