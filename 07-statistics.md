# Statistics

# Table of Contents

[1. Introduction](#section-a)  
[2. Why We Are Using Think Stats](#section-b)  
[3. Instructions for Cloning the Repo](#section-c)  
[4. Required Exercises](#section-d)  
[5. Optional Exercises](#section-e)  
[6. Recommended Reading](#section-f)  
[7. Resources](#section-g)

## <a name="section-a"></a>1.  Introduction

[<img src="img/think_stats.jpg" title="Think Stats"/>](http://greenteapress.com/thinkstats2/)

Use Allen Downey's [Think Stats (second edition)](http://greenteapress.com/thinkstats2/) book for getting up to speed with core ideas in statistics and how to approach them programmatically. This book is available online, or you can buy a paper copy if you would like.

Use this book as a reference when answering the 6 required statistics questions below.  The Think Stats book is approximately 200 pages in length.  **It is recommended that you read the entire book, particularly if you are less familiar with introductory statistical concepts.**

Complete the following exercises along with the questions in this file. Some can be solved using code provided with the book. The preface of Think Stats [explains](http://greenteapress.com/thinkstats2/html/thinkstats2001.html#toc2) how to use the code.  

Communicate the problem, how you solved it, and the solution, within each of the following [markdown](https://guides.github.com/features/mastering-markdown/) files. (You can include code blocks and images within markdown.)

## <a name="section-b"></a>2.  Why We Are Using Think Stats 

The stats exercises have been chosen to introduce/solidify some relevant statistical concepts related to data science.  The solutions for these exercises are available in the [ThinkStats repository on GitHub](https://github.com/AllenDowney/ThinkStats2).  You should focus on understanding the statistical concepts, python programming and interpreting the results.  If you are stuck, review the solutions and recode the python in a way that is more understandable to you. 

For example, in the first exercise, the author has already written a function to compute Cohen's D.  **You could import it, or you could write your own code to practice python and develop a deeper understanding of the concept.** 

Think Stats uses a higher degree of python complexity from the python tutorials and introductions to python concepts, and that is intentional to prepare you for the bootcamp.  

**One of the skills to learn here is to understand other people’s code.  And this author is quite experienced, so it’s good to learn how functions and imports work.**

---

## <a name="section-c"></a>3.  Instructions for Cloning the Repo 
Using the [code referenced in the book](https://github.com/AllenDowney/ThinkStats2), follow the step-by-step instructions below.  

**Step 1. Create a directory on your computer where you will do the prework.  Below is an example:**

```
(Mac):      /Users/yourname/ds/metis/metisgh/prework  
(Windows):  C:/ds/metis/metisgh/prework
```

**Step 2. cd into the prework directory.  Use GitHub to pull this repo to your computer.**

```
$ git clone https://github.com/AllenDowney/ThinkStats2.git
```

**Step 3.  Put your ipython notebook or python code files in this directory (that way, it can pull the needed dependencies):**

```
(Mac):     /Users/yourname/ds/metis/metisgh/prework/ThinkStats2/code  
(Windows):  C:/ds/metis/metisgh/prework/ThinkStats2/code
```

---


## <a name="section-d"></a>4.  Required Exercises

*Include your Python code, results and explanation (where applicable).*

### Q1. [Think Stats Chapter 2 Exercise 4](statistics/2-4-cohens_d.md) (effect size of Cohen's d)  
Cohen's D is an example of effect size.  Other examples of effect size are:  correlation between two variables, mean difference, regression coefficients and standardized test statistics such as: t, Z, F, etc. In this example, you will compute Cohen's D to quantify (or measure) the difference between two groups of data.   

You will see effect size again and again in results of algorithms that are run in data science.  For instance, in the bootcamp, when you run a regression analysis, you will recognize the t-statistic as an example of effect size.

**My Solution**
This question tasked me with computing Cohen's D to measure the effect size for the difference in weight between first born babies and other babies. I wrote the following function to check for the effect size of Cohen's D(checked against the ThinkStats book):
```
def Cohen_d(group1, group2):
    diff = group1.mean() - group2.mean()
    n1 = len(group1)
    n2 = len(group2)
    var1 = group1.var()
    var2 = group2.var()
    pooled_s = math.sqrt((n1 * var1 + n2 * var2) / (n1 + n2))
    d = diff / pooled_s
    return d
```
After importing the dataset, the dataset was split between babies who were the first born and the babies born after the first child. I ran the means of both groups with first born babies having a mean weight of 7.2 lbs and the other babies having a mean weight of 7.33. 
```
preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]
firsts.totalwgt_lb.mean()
others.totalwgt_lb.mean()
```
Using the Cohen D function, I found an effect size of -0.09 standard deviations which is larger than the difference between pregnancies. I also checked my Cohen's D function against the one written in the book to make sure there were no errors.
```
Cohen_d(firsts.totalwgt_lb, others.totalwgt_lb)
```

### Q2. [Think Stats Chapter 3 Exercise 1](statistics/3-1-actual_biased.md) (actual vs. biased)
This problem presents a robust example of actual vs biased data.  As a data scientist, it will be important to examine not only the data that is available, but also the data that may be missing but highly relevant.  You will see how the absence of this relevant data will bias a dataset, its distribution, and ultimately, its statistical interpretation.

**My Solution**
This pyoblem borrows from the issue of the class size paradox explained in chapter three. Exercise 1 asks for what the dataset actually looks like versus what the data would look like from the perspective of a randomly selected case. In this case, I'm looking at what the data would look like if children were serveyed on the size of their family. The following functions were used:
```
def Bias_pmf(pmf, label):
    bias_pmf = pmf.Copy(label=label)
    
    for c, r in pmf.Items():
        bias_pmf.Mult(x, x)
        
    bias_pmf.normalize()
    return bias_pmf

def Normal_pmf(pmf, label):
    normal_pmf = pmf.Copy(label=label)
    
    for c, r in pmf.Items():
        normal_pmf.Mult(x, 1 / x)
        
    normal_pmf.normalize()
    return normal_pmf
```
I created a pmf for the data and then loaded in a biased pmf. I also plotted the two pmfs against each other.
```
Samplepmf = thinkstats2.Pmf(resp.numkdhh, label='#_of_kids')
biased = BiasPmf(Samplepmf, label='biased_sample')
thinkplot.PrePlot(2)
thinkplot.Pmfs([Samplepmf, biased])
thinkplot.Config(xlabel='Number of children', ylabel='PMF')
```
Afterwards the means were calculated.
```
Samplepmf.Mean()
biased.Mean()
```
The mean of the sample was one child where the mean of the biased sample was 2.4 children. The question states that familes with no children had no chance of being selected which was one notable bias on the mean. 

### Q3. [Think Stats Chapter 4 Exercise 2](statistics/4-2-random_dist.md) (random distribution)  
This questions asks you to examine the function that produces random numbers.  Is it really random?  A good way to test that is to examine the pmf and cdf of the list of random numbers and visualize the distribution.  If you're not sure what pmf is, read more about it in Chapter 3.  

**My Solution**
The problem here is to compare the pmf and cdf of a large amount of random numbers. This code was used to plot the pmf and cdf:
```
pmf = thinkstats2.Pmf(t)
thinkplot.Pmf(pmf, linewidth=0.1)
thinkplot.Config(xlabel='Random variate', ylabel='PMF')

cdf = thinkstats2.Cdf(t)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Random variate', ylabel='CDF')
```
It's almost impossible to read the pmf as there are so many different values. However the cdf shows a uniform distribution.

### Q4. [Think Stats Chapter 5 Exercise 1](statistics/5-1-blue_men.md) (normal distribution of blue men)
This is a classic example of hypothesis testing using the normal distribution.  The effect size used here is the Z-statistic. 

**My Solution**
The question is asking what percentage of the US adult male population is between 5'10(177.8 cm) and 6'1(185.4 cm). The following code sets up the normal distribution:
```
import scipy.stats
mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)
```
A cumulative distribution function is used to find the percentage of the sample that is between 5'10 and 6'1:
```
Min = dist.cdf(177.8)
Max = dist.cdf(185.4)
Max-Min
```
The code shows that 34% of the population is between 5'10 and 6'1. The difference is betweem -.03 and .96 Z-scores.


### Q5. Bayesian (Elvis Presley twin) 

Bayes' Theorem is an important tool in understanding what we really know, given evidence of other information we have, in a quantitative way.  It helps incorporate conditional probabilities into our conclusions.

Elvis Presley had a twin brother who died at birth.  What is the probability that Elvis was an identical twin? Assume we observe the following probabilities in the population: fraternal twin is 1/125 and identical twin is 1/300.  

**My Solution**
I apporached this problem by calculating by hand the population of fraternal and identical twins out of a population of 100,000. In a total population of 1,133 twins, 800(71%) would be fraternal and 333(31%) would be identical. We also know that Evlis' twin was male and since identical twins are always the same gender but fraternal twins are not, I multipled the chances of being a fraternal twin by .5 while keeping identical the same. I normalized the numbers which leaves a 45% chance that Elvis was a twin.

---

### Q6. Bayesian &amp; Frequentist Comparison  
How do frequentist and Bayesian statistics compare?

**My Solution**
Bayesian statistics factor in conditional probablities while Frequentists will consider the long term frequencies of an event occuring. A Baysian statistician can assign probabilities to unknown events while a Frequentist will not. 

---

## <a name="section-e"></a>5.  Optional Exercises

The following exercises are optional, but we highly encourage you to complete them if you have the time.

### Q7. [Think Stats Chapter 7 Exercise 1](statistics/7-1-weight_vs_age.md) (correlation of weight vs. age)
In this exercise, you will compute the effect size of correlation.  Correlation measures the relationship of two variables, and data science is about exploring relationships in data.    

### Q8. [Think Stats Chapter 8 Exercise 2](statistics/8-2-sampling_dist.md) (sampling distribution)
In the theoretical world, all data related to an experiment or a scientific problem would be available.  In the real world, some subset of that data is available.  This exercise asks you to take samples from an exponential distribution and examine how the standard error and confidence intervals vary with the sample size.

### Q9. [Think Stats Chapter 6 Exercise 1](statistics/6-1-household_income.md) (skewness of household income)
### Q10. [Think Stats Chapter 8 Exercise 3](statistics/8-3-scoring.md) (scoring)
### Q11. [Think Stats Chapter 9 Exercise 2](statistics/9-2-resampling.md) (resampling)

---

## <a name="section-f"></a>6.  Recommended Reading

Read Allen Downey's [Think Bayes](http://greenteapress.com/thinkbayes/) book.  It is available online for free, or you can buy a paper copy if you would like.

[<img src="img/think_bayes.png" title="Think Bayes"/>](http://greenteapress.com/thinkbayes/) 

---

## <a name="section-g"></a>7.  More Resources

Some people enjoy video content such as Khan Academy's [Probability and Statistics](https://www.khanacademy.org/math/probability) or the much longer and more in-depth Harvard [Statistics 110](https://www.youtube.com/playlist?list=PL2SOU6wwxB0uwwH80KTQ6ht66KWxbzTIo). You might also be interested in the book [Statistics Done Wrong](http://www.statisticsdonewrong.com/) or a very short [overview](http://schoolofdata.org/handbook/courses/the-math-you-need-to-start/) from School of Data.
