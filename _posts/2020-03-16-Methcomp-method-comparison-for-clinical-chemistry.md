---
layout: post
title: Method comparison for clinical chemistry: introducting the methcomp software package
permalink: /Method-comparison-in-clinical-chemistry/
---

# Introduction
Laboratory medicine is amongst the fastest growing specialities in the medicine, being crucial in the diagnosis, supoprt of prevention and in the monitoring of
disease states for individual patients, as well as for the evaluation of treatment for population of patients [1]. High quality and safety in laboratory testing has
therefore a crucial role in modern, high-quality healthcare. To ensure high quality and safety validation, comparison and verification of new laboratory tests is 
a crucial step in the continious innovation and implementation of new, faster, better or even more safe laboratory tests for the patients [2]. In the process of validating a new laboratory test, we often employ (statistical) tools (i.e. method comparison software) to help us guide make decisions about the new laboratory test. Unfortunately there is no such publicly available software tool to do this in the Python programming language.  

The Python programming language was invested in the 1990s by Guido van Rossum [3]. Although its been available for such a long time, its popularity really took of when
the lastest version of Python was released back in 2008 (Python 3) [4]. Python as we know today has first-class integration with a lot low of level systems (e.g. clinical chemistry analyzers), can easily handle CPU heavy tasks, has powerful toolsets for mathematics, statistics and computer science. Not only does this provide Python with direct access to the analyzers we use nowadays, but also can it be used for a lot of automation, machine learning and extensive data analysis. The Python language is especially interesting for method comparison as it would allow us to directly validate and compare new methods on the system itself rather then having to analyze it in a later stage using a distinctive language (i.e. R or even Excel). Recently, we developed a new public software package called `methcomp` which is designed to fill this gap.

# Methcomp
Methcomp is a Python software package designed to provide users with an easy to access, flexible interface to perform method comparison,
validation and verification. It allows us to create a variety of graphical plots showing us for example the differences between a new
versus old measurement method for an analyte. Methcomp is easily accessible by downloading it from the Python software repository
(direct link is [here](https://pypi.org/project/methcomp/)]) using the command: 

{% highlight python %}
pip install methcomp
{% endhighlight %}

Source code for the project is available through [Github](https://github.com/wptmdoorn/methcomp). In this blog post, I will provide
examples using the methcomp software library to provide three type of plots for method comparison:
1. Scatter plot with regression
2. Difference plots 
3. Glucose sensor error grids 

# Scatter plots: Passing-Bablok and Deming
One of the most frequently used approaches to compare two methods is to produce a scatter plot with a regression technique to examine
the relationship between the first and second method. Although linear regression is still often used, it has several serious drawbacks which
limits the use in method comparison. Deming [5, 6] and Passing-Bablok [7] regression are statistical techniques that also allow, in contrast to
linear regression, random measurement errors in the X-axis values. In the case of Deming regression, the assumption is made that these errors
are normally distributed, and in case of Passing-Bablok, no assumptions are made. In the example provided below we generated a random set of measurements
for method 1 and method 2 and analysed them using Deming (left; blue) and Passing-Bablok (right; red) techniques.

<p>
<img src="/assets/02methcomp/deming.png" alt="drawing" width="49%"/> 
<img src="/assets/02methcomp/pb.png" alt="drawing" width="49%"/> <br>
  <span style="color:gray; font-size:0.8em;"><b>Figure 1:</b> Illustrative examples of Deming (left) and Passing-Bablok (right) on a random
generated dataset of measurements for method 1 and method 2. Shaded areas present the 95% confidence interval for both regression lines. </span>
</p>

# Difference plots: Bland-Altman
A second approach to method comparison is to obtain information about the actual "difference" between two methods, often done by "Bland-Altman" plots [8, 9]. 
Bland-Altman plots depict the differences (or alternatively the ratios) between the two techniques which are are plotted against the averages of the two techniques. 
Horizontal lines are drawn at the mean difference, and at the limits of agreement, which are defined as the mean difference plus and minus 1.96 times the standard deviation of the differences (although this can be altered in specific context). Bland-Altman plots especially excel in detecting bias in one of the two methods
and are therefore often used complementary to the regression techniques. 

<p>
<img src="/assets/02methcomp/blandaltman_abs.png" alt="drawing" width="49%"/> 
<img src="/assets/02methcomp/blandaltman_rel.png" alt="drawing" width="49%"/> <br>
  <span style="color:gray; font-size:0.8em;"><b>Figure 2:</b> Illustrative examples of Bland-Altman plots for the absolute (left) and relative
differences (right) on a random generated dataset of measurements for method 1 and method 2. Shaded areas present the 95% confidence interval for mean and limit of
agreement lines.</span>
</p>


# Glucose sensor error grids
The third current available feature of methcomp may seem a bit misplaced, but was not available as a standard plot in the Python package index which made us
implement this also. Glucose sensor error grids, Clarke (1987) [9] and Parkes (2000) [10, 11] are specifically designed as a method comparison tool for reference
and new blood glucose measurement systems. These graphical plots are simple scatter plots complemented with a Cartesian grid which labels each of the points to a specific zone. Each of these zones has a different clinical interpretation and consequence, allowing us to do a clinical evaluation of the new versus the old
method. For instance, values that are in zones C to E can potentially lead to dangerous situations causing harm for the individual wearing the glucose sensor. 
In the example provided below we generated a random set of measurements for a new and old glucose measurement system and analysed them using the Clarke (left) and
Parkes (right) error grids.

<p>
<img src="/assets/02methcomp/clarke.png" alt="drawing" width="49%"/> 
<img src="/assets/02methcomp/parkes.png" alt="drawing" width="49%"/> <br>
  <span style="color:gray; font-size:0.8em;"><b>Figure 3:</b> Illustrative examples of Clarke (left) and Parkes (right) error grids on a random set of
measurements from an old versus a new glucose sensor system. Zone A and B depict clinically safe zones, whilst zones C to E are potentially dangerous (see 
respective papers for detailed description of zones [9-11].</span>
</p>

# Conclusion



## References
1. Seyhan, A.A., Carini, C. Are innovation and new technologies in precision medicine paving a new era in patients centric care?. J Transl Med 17, 114 (2019). https://doi.org/10.1186/s12967-019-1864-9
2. Jensen, A. L., & Kjelgaard-Hansen, M. (2006). Method comparison in the clinical laboratory. Veterinary Clinical Pathology, 35(3), 276–286. https://doi.org/10.1111/j.1939-165x.2006.tb00131.x 
3. van Rossum, G., Python tutorial, Technical Report CS-R9526, Centrum voor Wiskunde en Informatica (CWI), Amsterdam, May 1995
4. http://pypl.github.io/PYPL.html. Consulted on 16 March, 20120.
5. Koopmans, T. C. (1937). Linear regression analysis of economic time series. DeErven F. Bohn, Haarlem, Netherlands.
6. Deming, W. E. (1943). Statistical adjustment of data. Wiley, NY (Dover Publications edition, 1985).
7. Passing H and Bablok W. J Clin Chem Clin Biochem, vol. 21, no. 11, 1983, pp. 709 - 720
8. Altman, D. G., and Bland, J. M. Series D (The Statistician), vol. 32, no. 3, 1983, pp. 307–317.
9. Altman, D. G., and Bland, J. M. Statistical Methods in Medical Research, vol. 8, no. 2, 1999, pp. 135–160.
10. Clarke, W. L., Cox, D., et al. Diabetes Care, vol. 10, no. 5, 1987, pp. 622–628.
11. Parkes, J. L., Slatin S. L. et al. Diabetes Care, vol. 23, no. 8, 2000, pp. 1143-1148.
12. Pfutzner, A., Klonoff D. C., et al. J Diabetes Sci Technol, vol. 7, no. 5, 2013, pp. 1275-1281.
