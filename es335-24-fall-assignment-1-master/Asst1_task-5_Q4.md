## Time Complexity Analysis of the code

**Variables definition:**

1. $N$: Total Number of Samples given _(Test + Train)_
2. $M$: Number of Attributes in the given data
3. $N_{train}$: Number of Samples used to construct the Decision Tree
4. $N_{test}$: Number of Samples used to test the Decision Tree

### Construction Timing Analysis:

The time complexity for construction is based on the maximum depth till which we would construct the Decision Tree. In our analysis, we would be considering the worst case $i.e$ the model builds up to the maximum possible depth.

From the scatter plots in (experiments-nb.ipynb) file we see that the time consumptions for the cases RIRO and RIDO are very similar. This is true for DIDO and DIRO too. From this observation we see that the time complexity is goverened majorly by the different types of input.

For each different type of input:

#### Case I: Real Input

##### Time for finding the best attribute:

The total time complexity will be = $Time\ Complexity\ for\ finding\ the\ best\ attribute \times Time\ Complexity\ of\ total\ number\ of \ splits$

For given series of size $n$, the function will calculate the entropy for all possible splits $(n - 1)$ which is of order $O(n)$. To calculate the entropy, we need to calculate the variance of $n$ samples which is a function of order $O(n)$.
There are $M$ such columns, and we need to iterate over all the columns to find the best attribute to split upon. Therefore, complexity: $O(n^2M)$

**Total Complexity:** $O(N_{train}^3 M)$

#### Case II: Discrete Input

##### Time for finding the best attribute:

The total time complexity will be = $Time\ Complexity\ for\ finding\ the\ best\ attribute \times Time\ Complexity\ of\ total\ possible\ splits$

To calculate the entropy, we need to calculate the entropy of $n$ samples which is a function of order $O(n)$.There are $M$ such columns, and we need to iterate over all the columns to find the best attribute to split upon.The total number of splits are constrained by the total number of combinations of all unique values from each attribute and the sample size. The minimum of both of them would govern the time complexity.

There are two scenarios:
- Constrained by Sample size.
  The maximum possible splits would be $(N_{train} - 1)$ which is of order $O(N_{train})$.
- Constrained by all the possible combinations.
  The total combinations would be of order $\prod_{i=1}^{M} a_{i}$ , where $a_i$ is the number of unique values. Let us consider this as $C$.


**Total Complexity:** $O(min(N_{train}, C) MN)$

### Prediction Timing Analysis:

To predict the output for a given set of attributes, we traverse through the constructed graph then the algorithm terminate at the leaf value and returns the value of the same. So, in the worst case scenario we iterate over the maximum possible depth.

#### Case I: Real Input

##### Maximum depth:

Since, there are $N_{train}$ samples so the total possible number of splits are $(N_{train} - 1)$. The worst case scenario is when at each split the division of $n$ samples occurs in the ratio $1:(n - 1)$. So, at every split _"Yes"_ part always has 1 sample. Therefore, the maximum depth is of the order $O(N_{train})$.The maximum depth as calculated above depends on the total possible splits $(N_{train} - 1)$, which is of order $O(N_{train})$. Then, we have $N_{test}$ such samples, so we iterate over the depth those many times.

**Total Complexity:** $O(N_{train}) \times O(N_{test}) = O(N_{train}N_{test})$

#### Case II: Discrete Input

##### Maximum depth:

Since, there are $N_{train}$ samples and $M$ attributes. The depth would be constrained by $N$ or $M$, so the order is of $O(min(N_{train}, M))$.The maximum depth as calculated above is of order $O(min(N_{train}, M))$. Then, we have $N_{test}$ such samples, so we iterate over the depth those many times.

**Total Complexity:** $O(min(N_{train}, M)) \times O(N_{test}) = O(N_{test}*min(N_{train}, M))$









