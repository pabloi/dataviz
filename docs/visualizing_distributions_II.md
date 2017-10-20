


# Visualizing distributions: Empirical cumulative density functions and q-q plots

In Chapter \@ref(histograms-density-plots), I described how we can visualize distributions with histograms or density plots. Both of these approaches are highly intuitive and visually appealing. However, as discussed in that chapter, they both share the limitation that the resulting figure depends to a substantial degree on parameters the user has to choose, such as the bin width for histograms and the bandwidth for density plots. As a result, both have to be considered as an interpretation of the data rather than a direct visualization of the data itself.

As an alternative to using histograms or density plots, we could simply show all the data points individually, as a point cloud (see e.g. Chapter \@ref(boxplots-violins)). However, this approach becomes unwieldy for very large datasets, and in any case there is value in aggregate methods that highlight properties of the distribution rather than the individual data points. To solve this problem, statisticians have invented empirical cumulative density functions (ecdfs) and quantile--quantile (q-q) plots. These types of visualizations require no arbitrary parameter choices, and they show all of the data at once. Unfortunately, they are a little less intuitive than a histogram or a density plot is, and I don't see them used frequently outside of highly technical publications. They are quite popular among statisticians, though, and I think anybody interested in data visualization should be familiar with these techniques.


## Empirical cumulative density functions

To illustrate cumulative empirical density functions, I will begin with a hypothetical example that is closely modeled after something I deal with a lot as a professor in the classroom: a dataset of student grades. Assume our hypothetical class has 50 students, and the students just completed an exam on which they could score between 0 and 100 points. How can we best visualize the class performance, for example to determine appropriate grade boundaries?

We can plot the total number of students that have received at least a certain number of points versus all possible point scores. This plot will be an ascending function, starting at 0 for 0 points and ending at 50 for 100 points. A different way of thinking about this visualization is the following: We can rank all students by the number of points they obtained, in ascending order (so the student with the fewest points receives the lowest rank and the student with the most points the highest), and then plot the rank versus the actual points obtained. The result is an *empirical cumulative distribution function* (ecdf) or simply *cumulative distribution.* Each dot represents one student, and the lines visualize the highest student rank observed for any possible point value.

<img src="visualizing_distributions_II_files/figure-html/student-grades-1.png" width="576" style="display: block; margin: auto;" />


You may wonder what happens if we rank the students the other way round, in descending order. This ranking simply flips the function on its head. The result is still an empirical cumulative distribution function, but the lines now represent the lowest student rank observed for any possible point value. 

<img src="visualizing_distributions_II_files/figure-html/student-grades-desc-1.png" width="576" style="display: block; margin: auto;" />

Ascending cumulative distribution functions are more widely known and more commonly used than descending ones, but both have important applications. Descending cumulative distribution functions are critical when we want to visualize highly skewed distributions (see below).

In practical applications, it is quite common to draw the ecdf without highlighting the individual points, and to normalize the ranks by the maximum rank, so that the *y* axis represents the cumulative frequency. For the student grades example, these modifications yield the following plot.


<img src="visualizing_distributions_II_files/figure-html/student-grades-normalized-1.png" width="576" style="display: block; margin: auto;" />

We can directly read off key properties of the student grade distribution from this plot. For example, a quarter of the students (25%) received less than 75 points. The median point value is 81. Approximately 20% of the students received 90 points or more.

I find ecdfs handy for assigning grade boundaries because they help me locate the exact cutoffs that minimize student unhappiness. For example, in this example, there's a fairly long horizontal line right below 80 points, followed by a steep rise right at 80. This feature is caused by three students receiving 80 points on their exam while the next poorer performing student received only 76. In this scenario, I might decide that everybody with a point score of 80 or more receives a B and everybody with 79 or less receives a C. The three students with 80 points are happy that they just made a B, and the student with 76 realizes that they would have had to perform much better to not receive a C. If I had set the cutoff at 77, the distribution of letter grades would have been exactly the same, but I might find the student with 76 points visiting my office hoping to negotiate their grade up. Likewise, if I had set the cutoff at 81, I would likely have three students in my office trying to negotiate their grade.

## Highly skewed distributions

Many empirical datasets display highly skewed distributions, in particular to the right, and these distributions can be challenging to visualize. Examples include *list* (@Clauset-et-al-2009).

<img src="visualizing_distributions_II_files/figure-html/county-populations-1.png" width="576" style="display: block; margin: auto;" />

<img src="visualizing_distributions_II_files/figure-html/county-populations-log-1.png" width="576" style="display: block; margin: auto;" />

<img src="visualizing_distributions_II_files/figure-html/county-populations-tail-log-log-1.png" width="576" style="display: block; margin: auto;" />

<img src="visualizing_distributions_II_files/figure-html/word-counts-tail-log-log-1.png" width="576" style="display: block; margin: auto;" />

## Quantile--quantile plots


<img src="visualizing_distributions_II_files/figure-html/student-grades-qq-1.png" width="576" style="display: block; margin: auto;" />

<img src="visualizing_distributions_II_files/figure-html/county-populations-qq-1.png" width="576" style="display: block; margin: auto;" />

The agreement between the observed and the theoretical values is exceptional. This demonstrates that the distribution of population counts among counties is indeed log-normal, as I suggested earlier in this chapter. *Give brief explanation for why. Random, multiplicative growth.*