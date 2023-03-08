## Initial Experiments
{:#initialexperiments}
We use the WatDiv benchmark to test our method. In the abscence of an extensive benchmark of our new method, we show performance characteristics of an old iteration of the optimizer that is severly undertrained and unoptimized. We show have how long the query optimizer explored in this paper takes to create a join plan. These results are shown in [](#initresults) and compared to the bind join operator in [Comunica](cite:cites taelman2018comunica). From the Table we find that while the model mostly generates worse query plans, it can in some cases outperform the standard optimizer. Note that the benchmarked model is severely undertrained and has not been optimized.

<figure id="initresults" class="table" markdown="1">

| Query Template           | C1     | C2     | C3     | F1    | F2    | F3    | F4     | F5    | L1    |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Search RL-Old            | 11.517 | 16.427 | 2.105  | 1.024 | 2.782 | 1.076 | 11.466 | 1.055 | 0.029 |
| Search RL-new            |        |        |        |       |       |       |        |       |       |
| RL Plan Execution-Old    | 3.116  | 2.577  | 0.583  | 0.100 | 0.090 | 0.062 | 1.906  | 0.059 | 0.006 |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Search Standard          | 0.007  | 0.008  | 0.017  | 0.002 | 0.003 | 0.005 | 0.005  | 0.005 | 0.002 |
| Standard Plan Execution  | 0.076  | 0.001  | 0.490  | 0.001 | 0.005 | 0.008 | 0.012  | 0.194 | 0.032 |

</figure>

<figure id="initresults2" class="table" markdown="1">

| Query Template           | L2     | L5     | S1     | S2    | S3    | S4    | S5     | S6    | S7    |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Optimization RL-Old      | 0.030  | 0.029  | 10.967 | 0.160 | 0.135 | 0.137 | 0.136  | 0.032 | 0.034 |
| Optimization RL-new      |        |        |        |       |       |       |        |       |       |
| RL Plan Execution-Old    | 0.001  | 0.002  | 2.242  | 0.011 | 0.005 | 0.000 | 0.002  | 0.008 | 0.002 |
| ------------------------ |--------|--------|--------|-------|-------|-------|--------|-------|-------|
| Search Standard          | 0.001  | 0.001  | 0.006  | 0.002 | 0.002 | 0.002 | 0.002  | 0.002 | 0.002 |
| Standard Plan Execution  | 0.006  | 0.007  | 0.139  | 0.009 | 0.008  | 0.005 | 0.009 | 0.001 | 0.000 |

<figcaption markdown="block">
Comparison of the query optimization and plan execution time, in seconds, of an old implementation of our optimizer, the improved implementation, and the standard [Comunica](cite:cites taelman2018comunica) optimizer.
</figcaption>
</figure>

