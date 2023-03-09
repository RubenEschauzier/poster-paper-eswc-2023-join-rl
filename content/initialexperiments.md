## Preliminary Results
{:#initialexperiments}
We use the WatDiv benchmark to test our method.

{:.comment data-author="RT"}
Cite watdiv!

In the absence of an extensive benchmark of our explored method,

{:.comment data-author="RT"}
What do you mean by this? Is watdiv not extensive enough?

we show performance characteristics of an old iteration of the optimizer that is severely undertrained and unoptimized.

{:.comment data-author="RT"}
"old" does not apply anymore?

We have implemented our optimizer in the TypeScript-based [Comunica query engine](cite:cites taelman2018comunica) and compare it to its default optimizer.

{:.comment data-author="RT"}
Might be good to explain in a sentence how this optimizer works.
Because we want to compare **approaches**, and implementations just provide us with a way to achieve this.

[](#initresults) shows that while the RL-based optimizer mostly generates worse query plans, it can find better join plans than the standard optimizer for some query templates.

{:.comment data-author="RT"}
Avoid imprecise terms like "mostly".
Be exact here, like "in X% of the cases, Y is Z times faster".
But be honest about the downsides as well.

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
Comparison of the query optimization and plan execution time, in seconds, of a previous version of our optimizer and the standard [Comunica](cite:cites taelman2018comunica) optimizer.

{:.comment data-author="RT"}
Say what you put in bold.
</figcaption>
</figure>
