## Initial Experiments
{:#initialexperiments}
We use the WatDiv benchmark to test our method. In the absence of an extensive benchmark of our explored method, we show performance characteristics of an old iteration of the optimizer that is severely undertrained and unoptimized. We implement the optimizer in Comunica. In [](#initresults), we compare the incomplete optimizer to the optimizer used in [Comunica](cite:cites taelman2018comunica). The Table shows that while the RL-based optimizer mostly generates worse query plans, it can find better join plans than the standard optimizer for some query templates.

<figure id="initresults" class="table" markdown="1">

| Query Template           | C1     | C2     | C3     | F1    | F2    | F3    | F4     | F5    | L1    |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Search RL                | 0.5028 | 1.000  | 0.277  | 0.214 | 0.347 | 0.160 | 0.800  | 0.278 | 0.027 |
| RL Plan Execution        | 3.116  | 2.577  | 0.583  | 0.100 | 0.090 | 0.062 | 1.906  | __0.059__ |__0.006__ |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Search Standard          | 0.007  | 0.008  | 0.017  | 0.002 | 0.003 | 0.005 | 0.005  | 0.005 | 0.002 |
| Standard Plan Execution  | __0.076__  | __0.001__  | __0.490__  | __0.001__ |__0.005__ |__0.008__ | __0.012__  | 0.194 | 0.032 |

</figure>

<figure id="initresults2" class="table" markdown="1">

| Query Template           | L2     | L5     | S1     | S2    | S3    | S4    | S5     | S6    | S7    |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Search RL                | 0.025  | 0.024  | 0.689  | 0.060 | 0.059 | 0.066 | 0.059  | 0.021 | 0.028 |
| RL Plan Execution        | __0.001__  | __0.002__  | 2.242  | 0.011 | __0.005__ | __0.000__ | __0.002__  | 0.008 | 0.002 |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Search Standard          | 0.001  | 0.001  | 0.006  | 0.002 | 0.002 | 0.002 | 0.002  | 0.002 | 0.002 |
| Standard Plan Execution  | 0.006  | 0.007  | __0.139__  | __0.009__ | 0.008  | 0.005 | 0.009 | __0.001__ | __0.000__ |

<figcaption markdown="block">
Comparison of the query optimization and plan execution time, in seconds, of a previous version of our optimizer and the standard [Comunica](cite:cites taelman2018comunica) optimizer.
</figcaption>
</figure>
