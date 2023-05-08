Download Link: https://assignmentchef.com/product/solved-stat823-homework-8-simple-regression
<br>
Using RMarkdown in RStudio, complete the following questions. Launch RStudio and open a new RMarkdown file or use the class RMarkdown template provided and save it on your working directory as a .Rmd file. At the end of the activity, save your <strong>pdf </strong>generated from RMarkdown+Knitr and submit your homework on the Blackboard.

<h1>1              Goodness of Fit</h1>

It is useful to have some measure of how well a model fits the data. One common choice for linear regression is <em>R</em><sup>2</sup>, the coeficient of determination, which is interpreted as the proportion of variance (of the outcome) explained by the model:

2                   unexplained variation in y                <sup>P</sup>(<em>y</em>ˆ<em><sub>i </sub>− y<sub>i</sub></em>)<sup>2                     </sup><em>SSE</em>

<em>R </em>= 1 <em>−     </em> = 1 <em>−    </em> = 1 <em>−</em>

total variation in y                       <sup>P</sup>(<em>y<sub>i </sub>− y</em>¯)<sup>2                     </sup><em>SSY</em>

Its range is 0 <em>≤ R</em><sup>2 </sup><em>≤ </em>1. Values closer to 1 indicating better fits. For simple linear regression,

<em>R</em><sup>2 </sup>= <em>r</em><sup>2 </sup>where <em>r </em>is the linear correlation between <em>x </em>and <em>y</em>. The linear correlation coeficient <em>r</em>

(Pearson’s correlation coeficient) has a range <em>−</em>1 <em>≤ r ≤ </em>1, with values close to <em>−</em>1 indicating a strong negative linear association between <em>x </em>and <em>y</em>, and values close to +1 indicating a strong positive linear association between <em>x </em>and <em>y</em>. Let’s investigate using simulation.

Page -1- of 4

<ol>

 <li>Generate a vector <em>x </em>containing 100 random numbers from a standard normal distribution and visualize the data:</li>

</ol>

x &lt;- <strong>rnorm</strong>(100) <strong>par</strong>(mfrow = <strong>c</strong>(2, 2)) <strong>plot</strong>(x, las = 1, cex = 1.5) <strong>hist</strong>(x, las = 1, cex = 1.5) <strong>boxplot</strong>(x, las = 1, cex = 1.5)

<strong>Histogram of x</strong>

Index                                                                                        x

<ol start="2">

 <li>To induce a linear relationship between <em>x </em>and a dependent variable <em>y</em>, generate the vector <em>y </em>using a linear transformation of the vector <em>x</em>:</li>

</ol>

y1 &lt;- 0 <strong>+ </strong>1 <strong>* </strong>x <em>## A perfect linear association </em>y2 &lt;- 0 <strong>+ </strong>1 <strong>* </strong>x <strong>+ </strong><strong>rnorm</strong>(<strong>length</strong>(x)) <em># Add a little N(0,1) noise (error)</em>

<ol start="3">

 <li>In this context, the variance of the Normal distribution used to generate the noise in the linear relationship is equivalent to the <em>error variance</em>, <em>σ</em><sup>2</sup>, in the simple linear regression model:</li>

</ol>

<em>y<sub>i </sub></em>= <em>β</em><sub>0 </sub>+ <em>β</em><sub>1</sub><em>x<sub>i </sub></em>+ <em>ε<sub>i</sub>,ε<sub>i </sub>∼ N</em>(0<em>,σ</em><sup>2</sup>)

Using this connection, generate four more vectors <em>y</em><sub>3</sub>, <em>y</em><sub>4</sub>, <em>y</em><sub>5</sub>, and <em>y</em><sub>6 </sub>by varying the amount of error (unexplained) variation in the linear relationship with <em>x</em>. Choose values of the error variation that span the range 0 <em>− </em>10. For example, let <em>y</em><sub>3 </sub><em>∼ N</em>(<em>x,</em>0<em>.</em>1):

y3 &lt;- 0 <strong>+ </strong>1 <strong>* </strong>x <strong>+ </strong><strong>rnorm</strong>(<strong>length</strong>(x), mean = 0, sd = <strong>sqrt</strong>(0.1)) <em>#sigma^2 = 0.1</em>

<ol start="4">

 <li>Generate scatterplots, <em>r</em>, and <em>R</em><sup>2 </sup>for each of the bivariate relationships: (<em>x</em>, <em>y</em><sub>1</sub>), (<em>x</em>, <em>y</em><sub>2</sub>), (<em>x</em>, <em>y</em><sub>3</sub>), (<em>x</em>, <em>y</em><sub>4</sub>), (<em>x</em>, <em>y</em><sub>5</sub>), (<em>x</em>, <em>y</em><sub>6</sub>). For example:</li>

</ol>

r.1 &lt;- <strong>cor</strong>(x, y1) <em># Calculates the correlation coefficient.</em>

R2.1 &lt;- r.1<strong>^</strong>2 <em># Relies on relationship in simple linear regression.</em>

R2.1a &lt;- <strong>summary</strong>(<strong>lm</strong>(y1 <strong>~ </strong>x))<strong>$</strong>r.squared <em># R^2 from linear regression model.</em>

## Warning in summary.lm(lm(y1 ~ x)): essentially ## perfect fit: summary may be unreliable

<strong>plot</strong>(x, y1, las = 1, cex = 1.5) <strong>mtext</strong>(<strong>bquote</strong>(<strong>paste</strong>(R<strong>^</strong>2 <strong>== </strong>.(R2.1a), “, “, <strong>~</strong>r <strong>== </strong>.(r.1))), col = “blue”)

<ol start="5">

 <li>Plot <em>r </em>versus <em>σ</em><sup>2 </sup>and <em>R</em><sup>2 </sup>versus <em>σ</em><sup>2</sup>. Comment on the relationship.</li>

</ol>

<h1>2              Simple Linear Regression</h1>

The director of admissions of a small college selected 120 students at random from the new freshman class in a study to determine whether a student’s grade point average (GPA) at the end of the freshman year (Y) can be predicted from the ACT test score (X). Using the attached dataset GPA, answer the following questions.

##

## No. of observations = 120

##

##         Var. name obs. mean            median s.d.          min.

## 1 GPA                   120 3.07         3.08         0.64        0.5

## 2 ACT                     120 24.73 25                 4.47       14

##       max.

## 1 4

## 2 35

<ol>

 <li>Write out the regression model that would explore the proposed relationship and state the model assumptions.</li>

 <li>Using the methods discussed in the lesson, test each model assumption. If any assumptions appear to be violated, comment on the potential consequences of moving forward with the simple linear regression model.</li>

 <li>Assume the simple linear regression model is appropriate and fit the model using R to obtain least squares estimates of <em>β</em><sub>0 </sub>and <em>β</em><sub>1</sub>. State the estimated regression function and interpret these estimates in the context of the problem.</li>

 <li>Plot the estimated regression function over a scatterplot of the raw data. Does the estimated regression function appear to fit the data well?</li>

 <li>What percentage of the variation in freshman GPA is explained by ACT test scores?</li>

 <li>Obtain a 95% confidence interval for <em>β</em><sub>1 </sub>and interpret. Why might the director of admissions be interested in whether the confidence interval includes the value zero?</li>

 <li>Test whether or not a linear association exists between student’s ACT score(X) and GPA at the end of the freshman year (Y). Use a level of significance of 0<em>.</em> State the hypotheses (<em>H</em><sub>0</sub>, <em>H</em><sub>1</sub>) and conclusion.</li>

 <li>What is the <em>p</em>-value for the test? Interpret it (i.e., how exactly does it support the conclusion you reached?).</li>

</ol>