$$\text{STA} 9705 $$
$$\text{Final Project}$$


Directions: You are not allowed to discuss this exam with anyone but your instructor. When
answering a question, first write down ***your complete answer**, and **then show relevant SAS**
output (if any). You cannot only show SAS output without any illustration. Clearly label all
the answers. Attach your full version of SAS code to the end. Any submission not in such
format will not be accepted. The data sets are available on Blackboard. Good luck!

# Q1

*The data in the file iris.txt contain observations on X_1 = Sepal length, X_2 = Sepal width, X_3 = Petal length and X_4 = Petal width for samples from **three species of iris** (1 = Iris setosa; 2 = Iris versicolor; 3 = Iris virginica).*

> #### QUESTION 1.A 
Is there any difference between the three species of iris in sepal and petal? Conduct an appropriate and complete test using α = 0.05. List all assumptions for the chosen test and explain every notation you may use.

The insect  data set comprise of n=150 observation, for the three diferrent species $u_1 = 5.006, u_2 = 1.326,u_3 = 5.552$. We are trying to identify the  difference between the three species of insects using the variables X3=sepal and X4=petal.  We can conduct a test on the the population mean vectors to meausre how heavily the two variables correlate. The null hypothesis and alternative hypothesis (H1) of the significance test for correlation can be expressed by condfucting a two-tailed significance test to test how heavily two variables correlate. 
Two-tailed significance test:

$H_0: ρ = 0$`the population correlation coefficient is 0; there is no association`


$H1: ρ ≠ 0$ `the population correlation coefficient is not 0; a nonzero correlation could exist`


The sample correlation coefficient between two variables x and y is denoted r or rxy, and can be computed as:



$$r_{xy} = \frac{\mathrm{cov}(x,y)}{\sqrt{\mathrm{var}(x)} \dot{} \sqrt{\mathrm{var}(y)}}$$




<br> 
 
![](https://raw.githubusercontent.com/BenitaDiop/students/master/bin/stat.png)

From our SAS output testing the correlation between the variable of sepal and petal and additionally the correlation between the mean vector of the sepal and petal grouped by species; both results  rejected the null and confirmed a large/strong correlation between the two variables.
$$z_{xy}=\frac{1}{2}\log\dfrac{1+r_{xy}}{1-r_{xy}}$$
The fisher transformation concluded with 95% confidence that the high correlation lies between the interval of 94% to 97% 
<br>




![](https://gm1.ggpht.com/-xl2yeJpe6VMsis1ENXs3QHlbGlDBA_dyNoZFdJ4DeFu7r7Gt56OPg_i5DfrYbMmpUrRfRpno5AwJC-zP7q1dPvDzm1Qv1CUlF_0jrQas90mJhYdLLXR3OGOUKBFPTPsztKarO1TF_2HqXWKaDF9GI5xBXUhHj22HECEepz1AHrZTZ44Vh6ApW6DD5V9yoD_l7NBxFIS6gzkQcquVi82irBoyd125S2_g0TfkSXJb07xVBBAPJugBQgs5Tti_QAuSqVu_d7XrAk-erTihjf6WS196eP8aJzG2QuB-DmsS8O2-rETik8YwtiIPmdnC2K3NHrRBjAwPKzKsjyftB6idCJz5RjQuU-66ql4m6jH6rn5iRVxG3wt1sIn6xCnp5w0MVMmKbaSIohQVYKKfRljt0pDI2k3wVD33BB_nKefbq_Jj0ojopg_4hmj0S6PCEbIxKJrcDZTrEtXV3oBhYqFD1UpP-qi9ixIUINPoZ5I6wkIxz5JO9twedq5fJJ5DTWkMxWSIMby3PY507ne1oYLi9z0QWqOuhKXHWpikwJXjpcE956-bG6HApEXx_KZSEySUk7-73zyfzejFbwVdUkLD7Ek7Ax99LDSEhFBF554n3MFJtafF2yMRJj7y2rWhIeWGT-FK1tfUN-oDydp8Z3IcsX35FTaX_RQA_qeaacPLcAQNcp87Hfo2PLb6Lqrbm7B39su2adnG2waVAango_C4DvPK_03d6PP84KdFdC5ynuHbcFMSMTgusqzh3XiA-gv4Dwu5GA=s0-l75-ft-l75-ft)






![collinearity](https://raw.githubusercontent.com/BenitaDiop/students/master/bin/colin.png)

```SAS   
title "Mean Sepal and Petal Grouped by Species Type";
PROC SQL;
CREATE TABLE WORK.Q1a
AS
SELECT avg(X3) as M3, avg(X4) as M4 FROM iris GROUP BY species  ;
RUN;
QUIT;
PROC PRINT DATA=WORK.Q1a;
/* RUN; */

proc corr data=iris cov fisher plots=matrix;
var X3; 
with X4;
run;
````



### QUESTION 1.B 


> Conduct a discriminant analysis and write down the resulting discriminant functions.
Plot the first discriminant function against the second one, and discuss the separation.


The linear discriminant function is given by 


$$d_{i0} = -\dfrac{1}{2}\mathbf{\mu'_i\Sigma^{-1}\mu_i}$$

The resulting discriminant function yield [0.98,0.48]

| Disc                     |           Function         |
|------------------------------:|:---------------------------------:|
| 1                   |          $             0.98                    $|
| 2                                | $     0.48 $           |

Performin a multivariate oneway analysis of variance (one-way MANOVA) via SAS we can cna produce the four multivariate test on the hypothsis of the groups in species being equal.  The test indicate thst not all meanvectors are equal (p>0.0001).

![image.png](attachment:image.png)


![](data:image/png;base64,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v6qtra2trS0qKiovL+/Xr5/scvAr3jL6x3snVKh+N4VGAF9++eXKSITLL7/c5Q4JCQmVlZXKY6vVKoRo1apV8OqDE5e/rG7dui1duvSnn36qq6uTWBsceMuECt47+qf63RQaAbx//35lJML+/ftd7nDttdeWlpYqjz/77DOj0cigQVnc/bKU/0GNxtD4Xy7s8ZYJIbx3dE71uylMfqPjx4+32+1ZWVkHDhzIycm54oorZFcEIYQYPXr0gAEDdu/evXv37vvvv/+yyy6TXRF+xVtG53jvhBDV76YwCeC4uLgXXnhhzZo1Xbp0sdls69atk10RhBAiLy+vpKQkPT29Z8+eycnJW7ZskV0RfsVbRud474QQ1e8mbsYAAECwcTMGAADkIIABAJCAAAYAQAICGAAACQhgAAAkIIABAJCAAAYAQAICGAAACQhgAAAkIIABAJCAAAYAQAICGAAACQhgICDeeOONlJQUo9FoMBhiY2Nvu+228vLyQJzoX//6V2xsrE8H37lzp8FgqLexRYsW/fr1q7cxNjZ29OjRftbw1VdfNTydyxrcsVqta9eubd++PTctRjghgAHt/fWvf7377rsvu+yyzz777Oeff3799dePHDnSMN40kZqaarVamzZt6udx7r777i+//NJqtTq2vPjii1VVVc8991zQanDnD3/4w5/+9KezZ88G6PiAFAQwoLGzZ8/Omzdv0KBBW7duzcjIaNOmTVZWlsVi2blzpxBi9uzZiYmJBoMhOjr6z3/+s/itgZiTk2M2m41G43XXXacc55133mnevLnRaIyNjZ01a5a7PZ2bkps2bWrTpo3RaDSbzffcc4+yseEZXZo7d67dbp89e7ZjS0FBQWpqqtLodFm20Wh85plnjEZjTk6OowZ3p3vggQeioqJMJtOYMWPqnXrt2rUtWrQwGo3x8fFLly5tWNupU6eqq6szMzO9/y0AIcBisdgBaCc/P18IUVpa6vKnrVq1evLJJ8+cOTN37lwhxJ49e7788kshxJVXXllUVPSPf/xDCPH3v//9+PHjRqNx6NChR48enTt3rsFgePvtt13uuWPHDiGE3W4/efKkyWS6/vrrDx48uGLFivbt27s7o+Mp9dxwww3JycnK43379gkh3nvvPQ9lGwyGTp06/fTTT84HdPcPvPjiiw8ePFhYWGgwGBYtWuR4ys8//2w0GjMyMo4fPz5lyhSDwVBSUuLypbvtttvatm2r/hcD6InFYiGAAY3de++9UVFR3uxpMpkKCwuVfHJsTExMvO+++3Jzc2NjYx0bU1NTu3bt6nJPR5JNnz49Jiamtra20TO6C2Bl+8aNG+12e//+/Zs1a9Zo2a+++qrjiZ73PH/+vLLxqquuSktLczxl6tSpMTExjqckJyePHTvW5XkJYIQTi8VCFzSgsQ4dOtTW1lZUVLj86aRJk5KTk00mk8FgqKmpcb7mqjCZTDU1NSUlJc2bN3ds7NSp0+nTp13u6fj2wIEDSUlJRmP9N3WjZ3To2bNnSkrKzJkza2pqPv/887vvvrvRgzg6uhvd03GF+KKLLnK+mltSUlJVVWX4zZkzZw4cOOCuQiCcEMCAxrKzsw0Gw4QJExr+6LHHHnv11VfvueeeXbt2lZaWxsTEuDtIp06dSktLHd/+8MMPrVq18nzeLl26nD17tq6uTt0ZFbm5ubt27ZoxY0ZdXZ3Sl+7TQTzseerUKeXBjz/+2LZtW+eyExMTnVsG27dv91wkEB4IYEBjKSkp99xzz1tvvXXLLbds3br11KlTq1ev7tWrV8eOHffv35+YmDhx4sTq6urBgwdXVVVVVVW5PEheXl51dfXNN9987Nixxx577IcffsjLy/N83lmzZtnt9t69ex86dOidd95p06bN2bNnvT+j4uGHH46Ojn7++ed79eoVFxenbPT+IB727NWr16FDh55//vnvv/9+xowZzmesqKgYOnTokSNHvvnmm0GDBt10002e/6VAmOAaMBAICxYsaNmypTI2OCYmpl+/fidPnjx8+HBSUpIQwmw2jxgxIikpaciQIfWu7CYlJU2cONFut69atUoZTmw2mx9++GG73e5yT+frr1u2bGnTpo0yAnno0KHV1dUuz+jukq1iyJAhQogdO3Y4tjRatuOAHvbMy8szGo0mkyk7O9v++8vGGzZsUMo2Go2dOnXasmWLy8K4BoxwYrFYDBaLJS0tTUb0AwAQoYqLi+mCBgBAAgIYAAAJCGAAACQggAEAkIAABgBAAgIYAAAJCGAAACQggAEAkIAABgBAAgIYAAAJCGAAACQggAEAkIAABgBAAgIYAAAJCGAAACQwCSGKi4tllwEAQGT5fzDPdR68ykXzAAAAAElFTkSuQmCC)


```SAS
proc sgrender data=outcan template=scatter;
run;
proc template;
define statgraph scatter;
begingraph / attrpriority=none;
entrytitle 'Species Measurement Data';
layout overlayequated / equatetype=fit
xaxisopts=(label='Canonical Variable 1')
yaxisopts=(label='Canonical Variable 2');
scatterplot x=Can1 y=Can2 / group=species name='species'
markerattrs=(size=3px);
layout gridded / autoalign=(topright);
discretelegend 'species' / border=false opaque=false;
endlayout;
endlayout;
endgraph;
end;
run;

```

#### QUESTION 1.C 
>Do we need both discriminant functions for the separation? Conduct test(s) to explain.

The first canonical correlation is at least as large as the multiple correlation between the groups and any
of the original variables. If the original variables have high within-group correlations, the first canonical
correlation can be large even if all the multiple correlations are small. In other words, the first canonical
variable can show substantial differences between the classes, even if none of the original variables do.

A test for seperation usingthe dominant eigenvalue will determine how the mean vectors are distributed in dimensional space.  If there is only one dominant eigenvalue (above 90% ) then the mean vestors will lie close to a line and will be collinear. Otherwise two or more ddominant eigenvalues
shows thst mean vectors diffuse. The null hypothesis is that all the mean vectors are the same, for all k-samples.The alternate hypothesis is where there is at least one pair of mean vectors that are not the same. In the MANOVA tests, if we reject H0, we know that there is at least one inequality where the mean vectors are not statistically different from each other, but we don’t know which mean vectors.

Our test shows that there is indeed a dominant eignevalue at 99% and the mean vector are collinear. The P value  of all our four multivaraiate test reject the null and so does the p-value of the Approimates F-value; hence we can conclude atleast one inequality.
![image.png](attachment:image.png)

### QUESTION 1.D 
> Conduct an appropriate and complete contrast test to find out specific differences among the species, based on what you find in (b)




$$H^{(1)}_0\colon \mu_1 = \mu_2$$
$$H^{(2)}_0\colon \mu_1 = \mu_3$$
$$H^{(3)}_0\colon \mu_2 = \mu_3$$


When we reject the null hypothesis in our MANOVA tests, that means there is at least one inequality in the hypothesis and finding the contrast can help to narrow which mean vectors have that inequality. This can be comparing 1 mean vector to another mean vector, comparing 1 mean vector to 2 other mean vectors, or comparing a group of mean vectors to another group of mean vectors.

![](https://raw.githubusercontent.com/BenitaDiop/students/master/dun.png)

```SAS
proc glm;
  class species;
  model X1 X2 X3 X4 = species;
  contrast '1 v/s 2&3'
    species -1 .5 .5;
  contrast '2 v/s 3'
    species 0 1 -1;
  manova H=species/printe printh mstat=exact;
run;
```




#### QUESTION 1.E 
> Which variable does contribute most to separating the species? Explain



                |   MSE |   VAL |
                |-------|-------|
                |X1     |  0.205|
                |X2     |  0.115|
                |X3     |  0.185| 
                |X4     |  0.041|
                
                
                
                
Variable X1 has the highest root mean square error and the lowest F-value indicating the means unqual means.

#### QUESTION 1.F 
> Among linear, quadratic and k nearest neighbor classification methods, which is the best method for the iris data based on their error rates? Show all necessary work 

Among linear, quadratic and KNN claissfication methods. Based of the error rates, quadratic peformed the best. Possibly due to to its flexibility.



![](https://raw.githubusercontent.com/BenitaDiop/students/master/l.png)


```SAS
title "Quadratic Classification";
proc discrim data=iris  posterr crossvalidate; 
priors proportional; id species; class species; var X1-X4; run;
title "Linear Classification";
proc discrim data=iris pool=no crossvalidate posterr; 
priors proportional; id species; class species; var X1-X4; run;
title "KNN Classification";
proc discrim data=iris method=npar k=5 crossvalidate posterr; 
priors proportional; id species; class species; var X1-X4; run;

```

#### QUESTION 1.G 
> Use the linear classification method to assign a new observation x 0 0 = (5.1, 3.5, 1.75, 0.3) into an appropriate species. Show all necessary work.

The new observation has been classified into species 1. 


![](https://raw.githubusercontent.com/BenitaDiop/students/master/T.png)


```SAS                  
PROC SQL;
INSERT INTO iris (X1, X2, X3, X4) \
values (5.1, 3.5, 1.75, 0.3); \
RUN; \ 
proc discrim data=iris tcorr \
method=normal pool=yes  outcross=iris;\
class species; \
var X1 X2 X3 X4; run; \ 
QUIT; 
PROC PRINT DATA=iris;run;  
```

># Q2
The weekly rates of return for five stocks: JP Morgan, Citibank, Wells Fargo, Royal Dutch Shell and Exxon Mobil, listed on the New York Stock Exchange are given in file stock_price.txt.

- (a) Should we use covariance matrix or correlation matrix if we want to apply principal component analysis (PCA) to this data set? Explain.

A covariance matrix will be be a good option to use so we can see which variable most dominates the total variance. 

![](https://raw.githubusercontent.com/BenitaDiop/students/master/c.jpg)


```SAS
options ls=89;

title "stock";
data stock;
infile "/folders/myfolders/final/stock_price.txt" DLM='09'x;
input J  C  W R E;
run;
proc princomp data=stock cov plots=matrix;
proc princomp data=stock plots=matrix;
run;
```

- (b) Following your decision in part (a), show the coefficients of all principal components and the variance explained by each component.

Using the covariance matrix the percent of variation explained by the eigenvalues are 52%, 27%,  10% , 0.05% and .05% 

- (c) Show principal components for the first five observations (Use SAS output only).

![](https://raw.githubusercontent.com/BenitaDiop/students/master/tpr.jpg)

- (d) How many principal components should we keep? Explain

The first three components should be sufficient. They explain ober 89% of the total variation. But using the 90% cutoff rule I would go with the first two componenets becasue for onyl two componenets they are explaining the a lot og variation at 80%

- (e) What are the interpretations of the components retained in part (d)?

The interpretation of  the componenets retaine is thatthe first component does explains most about JP Morgran, Citibank and Wells Fargo. However the second principal component explains the remaining two variable, Royal Dutch shell and Exxon Mobil much better. 

- (f) Is there any outlier in this data set? Explain.

Observing the distribution of the component scores I would say there are no outliers. 

>#                            Q3 
A firm is attempting to evaluate the quality of its sales staff and is trying to find an examination or series of tests that may reveal the potential for good performance in sales. The firm has selected a random sample of 50 sales people and has evaluated each on 3 measures of performance: X 1 = growth of sales, X 2 = profitability of sales, and X 3 = new-account sales. Each of the 50 individuals took each of 4 tests, which purported to measure X 4 = creativity, X 5 = mechanical reasoning, X 6 = abstract reasoning, and X 7 = mathematicalability, respectively. 
The data are given in file salesman.txt

- (a) Fit a factor model with 3 factors using iterated principal factor method. Show initial estimates of communalities, and final estimates of loadings, communalities, specific variances, and the proportion of variance explained by each factor.

![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image.png)
![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(1).png)

- (b) Did you find any ‘unusual’ estimate in (a)? If so, explain why it happened.

The unsual estimates were in the communalities that exceeded one and the high covariance almost at the value of one between x2 and other variables. 

- (c) Do an orthogonal rotation to the factors obtained in (a). Show the resulting loadings,communalities, specific variances, and the proportion of variance explained by each factor. Does any of those estimates not change after rotation? Explain.



The final communality estimates for the the first variable labeled x1, which accounts for the growth of sales, remains unchanged after rotation. The variance explained has spread over all factors which changed the the variance explained by each of the factors. 

![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(2).png)

- (d) On which factor does profitability of sales depend most? Why? Use rotated loadings.

Profitability of sales, labeled X2 depends most on the first factor when comapred to the second and third factor laodings. Factor 1, explains most of the variance in profitability of sales. 



![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(4).png)

- (e) Show the complexity of each variable using threshold 0.6, and interpret rotated factors.
Variable X1 X2 X3 and X7 passes the complexity threshold of 0.6 with factor 1, variable X4 is the only one that passes the compelixity threshold of 0.6 in factor 2 while X6 is the only one the passes the complexity threshold in factor 3. Variable X5 is the only one that fails to reach the 0.6 threshold in all three factors.
 

![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(5).png)

- (f) Is the model fit in (a) sufficient for doing factor analysis to the data? If yes, explain why. If no, try to improve it.

Mechanical Reasoning, X5, has no assoicated factor, hence I would sy that the factor analysis is not sufficient. To improve the model, I believe that  introducing an additional factor will help explain the unassociated variable. 

![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(3).png)





```SAS
options ls=89;
data salesman;
infile "/folders/myfolders/salesman.txt";
input X1 X2 X3 X4 X5 X6 X7;
run;

title 'Factor Analysis of Salesman';
proc factor method=prin nfact=3 rotate=varimax plots=all;
var X1-x7; 

proc factor method=prinit nfact=3 priors=smc 
heywood maxiter=100 rotate=varimax corr plots=all; run; 

proc factor method=prin priors=smc nfact=3 rotate=varimax plots=all; 
var X1-X7; run;

proc factor method=prin priors=smc nfact=4 rotate=varimax plots=all; 
var X1-X7; run; 


```

> # Q4  
*The file university.txt gives the data on some universities for certain variables used to compare or rank major universities. These variables include X 1 = average SAT score of new freshmen, X 2 = percentage of new freshmen in top 10% of high school class, X 3 = percentage of applicants accepted, X 4 = student-faculty ratio, X 5 = estimated annual expenses and
X 6 = graduation rate (%). Because SAT and Expenses are on a much different scale from that of the other variables, you need to standardize the data first.*

(a) Use hierarchical clustering with average linkage and answer the following questions.
(i) Show the resulting dendrogram and cluster history.
(ii) Decide the value of g (number of clusters) using both methods given in the lecturenotes, and show the resulting clus
Observing the distance we can see that the largest distance is between cluster 1 and cluster 2 in the cluster history. So I would decide on a value of g=2

![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(7).png)


![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(9).png)


```SAS
options ls=89;

title "uni";
data uni;
infile "/folders/myfolders/university.txt" dlm=' ';
input uni $ X1 X2 X3 X4 X5 X6;
run;
proc standard data=uni out=uni mean=0 std=1;
var X1 X2 X3 X4 X5 X6;
run;
proc sort;by uni; run;
title "Average Linkage Cluster Analysis";    
proc cluster method=average outtree=clust1;
 var X1 X2 X3 X4 X5 X6;
  id uni;
  run;

```

- (b) Cluster the universities with K-means method. Use the first 3 observations that are at least r = 1.5 apart as seeds. Show the seeds and resulting clusters, and plot the first two discriminant functions against each other

![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(13).png)




![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(11).png)

![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(10).png)



```SAS
title "uni";
data uni;
infile "/folders/myfolders/university.txt" dlm=' ';
input uni $ X1 X2 X3 X4 X5 X6;
run;
proc standard data=uni out=uni mean=0 std=1;
var X1 X2 X3 X4 X5 X6;
run;
proc sort;by uni; run;
proc fastclus data=uni radius=1.5 maxc=3 replace=none maxiter=10 out=out ;
var X1 X2 X3 X4 X5 X6;
id uni;
run;
```

- (c) Redo (b) using the 3 centroids given by the hierarchical clustering in (a) as seeds. Show the seeds and resulting clusters, and compare them to those given in (b). Which seeds do give us a better clustering, the centroids in (a) or those used in (b)? Explain.




The seeds that give us a better clustering are X1 and X2 accounting for the largest correlation; Cluster two has the least relative change in cluster seeds and the smallest maximum distance from the seed to the observations.  

![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(14).png)

![](https://raw.githubusercontent.com/BenitaDiop/students/master/env/image%20(15).png)


```SAS
options ls=89;

title "uni";
data uni;
infile "/folders/myfolders/university.txt" dlm=' ';
input uni $ X1 X2 X3 X4 X5 X6;
run;
proc standard data=uni out=uni mean=0 std=1;
var X1 X2 X3 X4 X5 X6;
run;
proc sort;by uni; run;
proc fastclus data=uninew maxc=3 maxiter=50 seed=Seeds out=out;
var X1 X2 X3 X4 X5 X6;
id uni;
run;
```
