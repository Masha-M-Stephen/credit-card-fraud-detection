R Markdown
----------

Some important functions.

``` r
load("C:/Users/fb8502oa/Desktop/Github stuff/credit-card-fraud-detection/Regression.Rdata")
load("C:/Users/fb8502oa/Desktop/Github stuff/credit-card-fraud-detection/mult.Rdata")
load("C:/Users/fb8502oa/Desktop/Github stuff/credit-card-fraud-detection/.RData")
```

Reading the data

``` r
Creditcard= read.csv("C:/Users/fb8502oa/Desktop/Github stuff/credit-card-fraud-detection/creditcard.csv")
View(Creditcard)
```

looking at the variables

``` r
str(Creditcard)
```

    ## 'data.frame':    284807 obs. of  31 variables:
    ##  $ Time  : num  0 0 1 1 2 2 4 7 7 9 ...
    ##  $ V1    : num  -1.36 1.192 -1.358 -0.966 -1.158 ...
    ##  $ V2    : num  -0.0728 0.2662 -1.3402 -0.1852 0.8777 ...
    ##  $ V3    : num  2.536 0.166 1.773 1.793 1.549 ...
    ##  $ V4    : num  1.378 0.448 0.38 -0.863 0.403 ...
    ##  $ V5    : num  -0.3383 0.06 -0.5032 -0.0103 -0.4072 ...
    ##  $ V6    : num  0.4624 -0.0824 1.8005 1.2472 0.0959 ...
    ##  $ V7    : num  0.2396 -0.0788 0.7915 0.2376 0.5929 ...
    ##  $ V8    : num  0.0987 0.0851 0.2477 0.3774 -0.2705 ...
    ##  $ V9    : num  0.364 -0.255 -1.515 -1.387 0.818 ...
    ##  $ V10   : num  0.0908 -0.167 0.2076 -0.055 0.7531 ...
    ##  $ V11   : num  -0.552 1.613 0.625 -0.226 -0.823 ...
    ##  $ V12   : num  -0.6178 1.0652 0.0661 0.1782 0.5382 ...
    ##  $ V13   : num  -0.991 0.489 0.717 0.508 1.346 ...
    ##  $ V14   : num  -0.311 -0.144 -0.166 -0.288 -1.12 ...
    ##  $ V15   : num  1.468 0.636 2.346 -0.631 0.175 ...
    ##  $ V16   : num  -0.47 0.464 -2.89 -1.06 -0.451 ...
    ##  $ V17   : num  0.208 -0.115 1.11 -0.684 -0.237 ...
    ##  $ V18   : num  0.0258 -0.1834 -0.1214 1.9658 -0.0382 ...
    ##  $ V19   : num  0.404 -0.146 -2.262 -1.233 0.803 ...
    ##  $ V20   : num  0.2514 -0.0691 0.525 -0.208 0.4085 ...
    ##  $ V21   : num  -0.01831 -0.22578 0.248 -0.1083 -0.00943 ...
    ##  $ V22   : num  0.27784 -0.63867 0.77168 0.00527 0.79828 ...
    ##  $ V23   : num  -0.11 0.101 0.909 -0.19 -0.137 ...
    ##  $ V24   : num  0.0669 -0.3398 -0.6893 -1.1756 0.1413 ...
    ##  $ V25   : num  0.129 0.167 -0.328 0.647 -0.206 ...
    ##  $ V26   : num  -0.189 0.126 -0.139 -0.222 0.502 ...
    ##  $ V27   : num  0.13356 -0.00898 -0.05535 0.06272 0.21942 ...
    ##  $ V28   : num  -0.0211 0.0147 -0.0598 0.0615 0.2152 ...
    ##  $ Amount: num  149.62 2.69 378.66 123.5 69.99 ...
    ##  $ Class : int  0 0 0 0 0 0 0 0 0 0 ...

``` r
#they are numeric variables 
```

``` r
head(Creditcard)
```

    ##   Time         V1          V2        V3         V4          V5          V6
    ## 1    0 -1.3598071 -0.07278117 2.5363467  1.3781552 -0.33832077  0.46238778
    ## 2    0  1.1918571  0.26615071 0.1664801  0.4481541  0.06001765 -0.08236081
    ## 3    1 -1.3583541 -1.34016307 1.7732093  0.3797796 -0.50319813  1.80049938
    ## 4    1 -0.9662717 -0.18522601 1.7929933 -0.8632913 -0.01030888  1.24720317
    ## 5    2 -1.1582331  0.87773675 1.5487178  0.4030339 -0.40719338  0.09592146
    ## 6    2 -0.4259659  0.96052304 1.1411093 -0.1682521  0.42098688 -0.02972755
    ##            V7          V8         V9         V10        V11         V12
    ## 1  0.23959855  0.09869790  0.3637870  0.09079417 -0.5515995 -0.61780086
    ## 2 -0.07880298  0.08510165 -0.2554251 -0.16697441  1.6127267  1.06523531
    ## 3  0.79146096  0.24767579 -1.5146543  0.20764287  0.6245015  0.06608369
    ## 4  0.23760894  0.37743587 -1.3870241 -0.05495192 -0.2264873  0.17822823
    ## 5  0.59294075 -0.27053268  0.8177393  0.75307443 -0.8228429  0.53819555
    ## 6  0.47620095  0.26031433 -0.5686714 -0.37140720  1.3412620  0.35989384
    ##          V13        V14        V15        V16         V17         V18
    ## 1 -0.9913898 -0.3111694  1.4681770 -0.4704005  0.20797124  0.02579058
    ## 2  0.4890950 -0.1437723  0.6355581  0.4639170 -0.11480466 -0.18336127
    ## 3  0.7172927 -0.1659459  2.3458649 -2.8900832  1.10996938 -0.12135931
    ## 4  0.5077569 -0.2879237 -0.6314181 -1.0596472 -0.68409279  1.96577500
    ## 5  1.3458516 -1.1196698  0.1751211 -0.4514492 -0.23703324 -0.03819479
    ## 6 -0.3580907 -0.1371337  0.5176168  0.4017259 -0.05813282  0.06865315
    ##           V19         V20          V21          V22         V23
    ## 1  0.40399296  0.25141210 -0.018306778  0.277837576 -0.11047391
    ## 2 -0.14578304 -0.06908314 -0.225775248 -0.638671953  0.10128802
    ## 3 -2.26185710  0.52497973  0.247998153  0.771679402  0.90941226
    ## 4 -1.23262197 -0.20803778 -0.108300452  0.005273597 -0.19032052
    ## 5  0.80348692  0.40854236 -0.009430697  0.798278495 -0.13745808
    ## 6 -0.03319379  0.08496767 -0.208253515 -0.559824796 -0.02639767
    ##           V24        V25        V26          V27         V28 Amount Class
    ## 1  0.06692807  0.1285394 -0.1891148  0.133558377 -0.02105305 149.62     0
    ## 2 -0.33984648  0.1671704  0.1258945 -0.008983099  0.01472417   2.69     0
    ## 3 -0.68928096 -0.3276418 -0.1390966 -0.055352794 -0.05975184 378.66     0
    ## 4 -1.17557533  0.6473760 -0.2219288  0.062722849  0.06145763 123.50     0
    ## 5  0.14126698 -0.2060096  0.5022922  0.219422230  0.21515315  69.99     0
    ## 6 -0.37142658 -0.2327938  0.1059148  0.253844225  0.08108026   3.67     0

``` r
#the class variable is binary in that if the transcation is fradulant it assigns 1 but if its legitimate it assigns 0.
```

\#at some point class needs to be a factor variable. \#time and amount
are the actual variables whilt the others are in principal components so
they are not the real data coz of confidencnaility.

``` r
Creditcard$Class = as.factor(Creditcard$Class)
str(Creditcard)
```

    ## 'data.frame':    284807 obs. of  31 variables:
    ##  $ Time  : num  0 0 1 1 2 2 4 7 7 9 ...
    ##  $ V1    : num  -1.36 1.192 -1.358 -0.966 -1.158 ...
    ##  $ V2    : num  -0.0728 0.2662 -1.3402 -0.1852 0.8777 ...
    ##  $ V3    : num  2.536 0.166 1.773 1.793 1.549 ...
    ##  $ V4    : num  1.378 0.448 0.38 -0.863 0.403 ...
    ##  $ V5    : num  -0.3383 0.06 -0.5032 -0.0103 -0.4072 ...
    ##  $ V6    : num  0.4624 -0.0824 1.8005 1.2472 0.0959 ...
    ##  $ V7    : num  0.2396 -0.0788 0.7915 0.2376 0.5929 ...
    ##  $ V8    : num  0.0987 0.0851 0.2477 0.3774 -0.2705 ...
    ##  $ V9    : num  0.364 -0.255 -1.515 -1.387 0.818 ...
    ##  $ V10   : num  0.0908 -0.167 0.2076 -0.055 0.7531 ...
    ##  $ V11   : num  -0.552 1.613 0.625 -0.226 -0.823 ...
    ##  $ V12   : num  -0.6178 1.0652 0.0661 0.1782 0.5382 ...
    ##  $ V13   : num  -0.991 0.489 0.717 0.508 1.346 ...
    ##  $ V14   : num  -0.311 -0.144 -0.166 -0.288 -1.12 ...
    ##  $ V15   : num  1.468 0.636 2.346 -0.631 0.175 ...
    ##  $ V16   : num  -0.47 0.464 -2.89 -1.06 -0.451 ...
    ##  $ V17   : num  0.208 -0.115 1.11 -0.684 -0.237 ...
    ##  $ V18   : num  0.0258 -0.1834 -0.1214 1.9658 -0.0382 ...
    ##  $ V19   : num  0.404 -0.146 -2.262 -1.233 0.803 ...
    ##  $ V20   : num  0.2514 -0.0691 0.525 -0.208 0.4085 ...
    ##  $ V21   : num  -0.01831 -0.22578 0.248 -0.1083 -0.00943 ...
    ##  $ V22   : num  0.27784 -0.63867 0.77168 0.00527 0.79828 ...
    ##  $ V23   : num  -0.11 0.101 0.909 -0.19 -0.137 ...
    ##  $ V24   : num  0.0669 -0.3398 -0.6893 -1.1756 0.1413 ...
    ##  $ V25   : num  0.129 0.167 -0.328 0.647 -0.206 ...
    ##  $ V26   : num  -0.189 0.126 -0.139 -0.222 0.502 ...
    ##  $ V27   : num  0.13356 -0.00898 -0.05535 0.06272 0.21942 ...
    ##  $ V28   : num  -0.0211 0.0147 -0.0598 0.0615 0.2152 ...
    ##  $ Amount: num  149.62 2.69 378.66 123.5 69.99 ...
    ##  $ Class : Factor w/ 2 levels "0","1": 1 1 1 1 1 1 1 1 1 1 ...

i divided the data into 10s just to see their distribution. this step is
just for fun nothing too serious here.

``` r
pairs.plus(Creditcard[, c(1:10)])
```

![](creditcardfraud_files/figure-markdown_github/unnamed-chunk-6-1.png)

``` r
#this function takes too long to run. be patient with it.
```

``` r
plot(Creditcard$Class)
```

![](creditcardfraud_files/figure-markdown_github/unnamed-chunk-7-1.png)

``` r
library(ggplot2)
```

    ## Warning: package 'ggplot2' was built under R version 3.6.2

``` r
#looking at the density of the transactions thoughout time
Fraud.yes = Creditcard[Creditcard$Class ==1, ]
Fraud.no = Creditcard[Creditcard$Class ==0, ]

ggplot()+
  geom_density(data = Fraud.yes,
               aes(x= Time), color = "Red",
               fill = "Red", alpha = 0.15)+
  geom_density(data = Fraud.no,
               aes(x= Time), color = "steelblue",
               fill = "steelblue", alpha = 0.15)
```

![](creditcardfraud_files/figure-markdown_github/unnamed-chunk-8-1.png)
time interval is only for two months. during the begining of each month,
the real transcations are not frequent.The fradulant go throughout with
equal density no so much inflactuations.

data cleaning. Removing unrelated variables, checking for typos,
verifying that the variables values make sense and removing missing
values.

``` r
#to check if  any rows or columns have missing values.
colnames(Creditcard)[colSums(is.na(Creditcard))> 0]
```

    ## character(0)

``` r
nrow(Creditcard[!complete.cases(Creditcard), ])
```

    ## [1] 0

\#now handling imbalance in the dataset.

``` r
#for this, lets go back to the facto variable which is class 
summary(Creditcard$Class)
```

    ##      0      1 
    ## 284315    492

as u can see, only 492 are fraud while the rest are legitmet. we have to
balance this shit

when trying to balance this kind of data u can use : undersampling
oversampling combining the two above.

simple model first withouth balancing. if the result is good, the
imbalance isnt a problem but if its awful, we will need to balance it.
that all depends on how it does with the classification

``` r
#without a model 
predictions = rep.int(0, nrow(Creditcard))
predictions = factor(predictions, levels= c(0,1))

#using confusion matrix 
library(caret)
```

    ## Warning: package 'caret' was built under R version 3.6.2

    ## Loading required package: lattice

``` r
confusionMatrix(data = predictions, reference = Creditcard$Class)
```

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction      0      1
    ##          0 284315    492
    ##          1      0      0
    ##                                           
    ##                Accuracy : 0.9983          
    ##                  95% CI : (0.9981, 0.9984)
    ##     No Information Rate : 0.9983          
    ##     P-Value [Acc > NIR] : 0.512           
    ##                                           
    ##                   Kappa : 0               
    ##                                           
    ##  Mcnemar's Test P-Value : <2e-16          
    ##                                           
    ##             Sensitivity : 1.0000          
    ##             Specificity : 0.0000          
    ##          Pos Pred Value : 0.9983          
    ##          Neg Pred Value :    NaN          
    ##              Prevalence : 0.9983          
    ##          Detection Rate : 0.9983          
    ##    Detection Prevalence : 1.0000          
    ##       Balanced Accuracy : 0.5000          
    ##                                           
    ##        'Positive' Class : 0               
    ## 

``` r
#to see how the true positives and true negatives. in this case, the fraud has to be i the lower right hand side
```

``` r
#since the confusion matrix doesnt correctly identify the fraud cases, we will use another method but we first have to divive our data into training and test sets.
library(caTools)
```

    ## Warning: package 'caTools' was built under R version 3.6.3

``` r
set.seed(1)
sampledata = sample.split(Creditcard$Class, SplitRatio = 0.75)
trainset = subset(Creditcard, sampledata == TRUE)
testset = subset(Creditcard, sampledata == FALSE)
```

``` r
dim(trainset)
```

    ## [1] 213605     31

``` r
dim(testset)
```

    ## [1] 71202    31

``` r
summary(trainset$Class)
```

    ##      0      1 
    ## 213236    369

``` r
# as u can see. its still imbalanced.
```

``` r
#handling imbalance using Random  Sampling (ROS)
legitrans = 213605
newfraq_legit = 0.50 #50% legit 50% fraud
newtotallegit = legitrans/newfraq_legit
```

``` r
library(ROSE)
```

    ## Warning: package 'ROSE' was built under R version 3.6.3

    ## Loaded ROSE 0.0-3

``` r
#both under sampling and oversampling 
legitrans = nrow(trainset)
fractionfraud = 0.50

samplingresults = ovun.sample(Class~., data = trainset, method = "both", N = legitrans, p = fractionfraud, seed = 2020)
```

Looking at the “balanced data” from random sampling

``` r
sampledcredit = samplingresults$data
summary(sampledcredit$Class)
```

    ##      0      1 
    ## 107216 106389

ploting to see the random sampling distribution

``` r
library(ggplot2)

ggplot(data = sampledcredit, aes(x=V1, y=V2, color =Class)) +
  geom_point(position = position_jitter(width = 0.2))+
  theme_bw()+
  scale_color_manual(values = c("steelblue", "red"))
```

![](creditcardfraud_files/figure-markdown_github/unnamed-chunk-19-1.png)

``` r
#using smoote to balance the dataset
library(smotefamily)
```

    ## Warning: package 'smotefamily' was built under R version 3.6.2

``` r
table(trainset$Class)
```

    ## 
    ##      0      1 
    ## 213236    369

``` r
#legitimate and fraud cases in the training set
n0 = 213236
n1 = 369
r0 = 0.6
```

``` r
#training will be the first 
ntimes = ((1-r0)/r0) * (n0/n1)-1
ntimes 
```

    ## [1] 384.2502

``` r
smote_output = SMOTE(X = trainset[ , -c(1,31)], 
                     target = trainset$Class,
                     K=6,
                     dup_size = ntimes)
```

Kesho anza hapa \#\#

``` r
Creditcard_smote  = smote_output$data
colnames(Creditcard_smote)[30]= "Class"
View(Creditcard_smote)
```

``` r
prop.table(table(Creditcard_smote$Class))
```

    ## 
    ##         0         1 
    ## 0.6001559 0.3998441

``` r
#distribution after applying smote

ggplot(Creditcard_smote, aes(x= V1, y = V2, color = Class))+
  geom_point()+
  scale_color_manual(values = c("steelblue", "red"))
```

![](creditcardfraud_files/figure-markdown_github/unnamed-chunk-25-1.png)

``` r
library(rpart)
```

    ## Warning: package 'rpart' was built under R version 3.6.2

``` r
library(rpart.plot)
```

    ## Warning: package 'rpart.plot' was built under R version 3.6.3

``` r
cart_model = rpart(Class~., Creditcard_smote)
#cart_model
rpart.plot(cart_model, extra = 0, type = 5, tweak = 1.2)
```

![](creditcardfraud_files/figure-markdown_github/unnamed-chunk-26-1.png)

``` r
#prediciting fraud cases 
predict_val = predict(cart_model, testset, type = "class")
#building a confusion matrix 
library(caret)
confusionMatrix(predict_val, testset$Class)
```

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction     0     1
    ##          0 69890    21
    ##          1  1189   102
    ##                                          
    ##                Accuracy : 0.983          
    ##                  95% CI : (0.982, 0.9839)
    ##     No Information Rate : 0.9983         
    ##     P-Value [Acc > NIR] : 1              
    ##                                          
    ##                   Kappa : 0.1416         
    ##                                          
    ##  Mcnemar's Test P-Value : <2e-16         
    ##                                          
    ##             Sensitivity : 0.98327        
    ##             Specificity : 0.82927        
    ##          Pos Pred Value : 0.99970        
    ##          Neg Pred Value : 0.07901        
    ##              Prevalence : 0.99827        
    ##          Detection Rate : 0.98157        
    ##    Detection Prevalence : 0.98187        
    ##       Balanced Accuracy : 0.90627        
    ##                                          
    ##        'Positive' Class : 0              
    ## 

``` r
#seeing without smote
cart_model = rpart(Class~., trainset[,-1])
rpart.plot(cart_model, extra = 0, type = 5, tweak = 1.2)
```

    ## Warning: Bad 'data' field in model 'call' (expected a data.frame or a matrix).
    ## To silence this warning:
    ##     Call rpart.plot with roundint=FALSE,
    ##     or rebuild the rpart model with model=TRUE.

![](creditcardfraud_files/figure-markdown_github/unnamed-chunk-28-1.png)

``` r
#predicting 
predict_val = predict(cart_model, testset[-1], type = 'class')

library(caret)
confusionMatrix(predict_val, testset$Class)
```

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction     0     1
    ##          0 71072    34
    ##          1     7    89
    ##                                           
    ##                Accuracy : 0.9994          
    ##                  95% CI : (0.9992, 0.9996)
    ##     No Information Rate : 0.9983          
    ##     P-Value [Acc > NIR] : < 2.2e-16       
    ##                                           
    ##                   Kappa : 0.8125          
    ##                                           
    ##  Mcnemar's Test P-Value : 4.896e-05       
    ##                                           
    ##             Sensitivity : 0.9999          
    ##             Specificity : 0.7236          
    ##          Pos Pred Value : 0.9995          
    ##          Neg Pred Value : 0.9271          
    ##              Prevalence : 0.9983          
    ##          Detection Rate : 0.9982          
    ##    Detection Prevalence : 0.9987          
    ##       Balanced Accuracy : 0.8617          
    ##                                           
    ##        'Positive' Class : 0               
    ## 

``` r
#prediction on all 

predict_val = predict(cart_model, Creditcard[,-1], type = 'class')
confusionMatrix(predict_val, Creditcard$Class)
```

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction      0      1
    ##          0 284286    102
    ##          1     29    390
    ##                                           
    ##                Accuracy : 0.9995          
    ##                  95% CI : (0.9995, 0.9996)
    ##     No Information Rate : 0.9983          
    ##     P-Value [Acc > NIR] : < 2.2e-16       
    ##                                           
    ##                   Kappa : 0.856           
    ##                                           
    ##  Mcnemar's Test P-Value : 3.161e-10       
    ##                                           
    ##             Sensitivity : 0.9999          
    ##             Specificity : 0.7927          
    ##          Pos Pred Value : 0.9996          
    ##          Neg Pred Value : 0.9308          
    ##              Prevalence : 0.9983          
    ##          Detection Rate : 0.9982          
    ##    Detection Prevalence : 0.9985          
    ##       Balanced Accuracy : 0.8963          
    ##                                           
    ##        'Positive' Class : 0               
    ## 

``` r
#decision tree without smot
cart_model = rpart(Class~., trainset[, -1])
rpart.plot(cart_model, extra = 0, type = 4, tweak = 1.2)
```

    ## Warning: Bad 'data' field in model 'call' (expected a data.frame or a matrix).
    ## To silence this warning:
    ##     Call rpart.plot with roundint=FALSE,
    ##     or rebuild the rpart model with model=TRUE.

![](creditcardfraud_files/figure-markdown_github/unnamed-chunk-31-1.png)

``` r
#predict
#for the test set
predict_val = predict(cart_model, testset[,-1], type = 'class')

library(caret)
confusionMatrix(predict_val, testset$Class)
```

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction     0     1
    ##          0 71072    34
    ##          1     7    89
    ##                                           
    ##                Accuracy : 0.9994          
    ##                  95% CI : (0.9992, 0.9996)
    ##     No Information Rate : 0.9983          
    ##     P-Value [Acc > NIR] : < 2.2e-16       
    ##                                           
    ##                   Kappa : 0.8125          
    ##                                           
    ##  Mcnemar's Test P-Value : 4.896e-05       
    ##                                           
    ##             Sensitivity : 0.9999          
    ##             Specificity : 0.7236          
    ##          Pos Pred Value : 0.9995          
    ##          Neg Pred Value : 0.9271          
    ##              Prevalence : 0.9983          
    ##          Detection Rate : 0.9982          
    ##    Detection Prevalence : 0.9987          
    ##       Balanced Accuracy : 0.8617          
    ##                                           
    ##        'Positive' Class : 0               
    ## 

Final prediction on the actual dataset

``` r
#whole dataset
predict_val = predict(cart_model, Creditcard[,-1], type = 'class')
confusionMatrix(predict_val, Creditcard$Class)
```

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction      0      1
    ##          0 284286    102
    ##          1     29    390
    ##                                           
    ##                Accuracy : 0.9995          
    ##                  95% CI : (0.9995, 0.9996)
    ##     No Information Rate : 0.9983          
    ##     P-Value [Acc > NIR] : < 2.2e-16       
    ##                                           
    ##                   Kappa : 0.856           
    ##                                           
    ##  Mcnemar's Test P-Value : 3.161e-10       
    ##                                           
    ##             Sensitivity : 0.9999          
    ##             Specificity : 0.7927          
    ##          Pos Pred Value : 0.9996          
    ##          Neg Pred Value : 0.9308          
    ##              Prevalence : 0.9983          
    ##          Detection Rate : 0.9982          
    ##    Detection Prevalence : 0.9985          
    ##       Balanced Accuracy : 0.8963          
    ##                                           
    ##        'Positive' Class : 0               
    ## 

END OF THE MAIN PROBLEM

TYING WITH NEURAL NETWORKS

``` r
library(nnet)
```

    ## Warning: package 'nnet' was built under R version 3.6.2

``` r
#trainset = we will use the initial train and test sets
#testset
```

``` r
creditcard.nn = nnet(trainset$Class~.,data=trainset,size=9,decay=.025,maxit=4000)
```

    ## # weights:  289
    ## initial  value 198590.128045 
    ## iter  10 value 69713.696615
    ## iter  20 value 4411.452338
    ## iter  30 value 3172.666358
    ## iter  40 value 3159.781002
    ## iter  50 value 3138.666197
    ## iter  60 value 2275.078255
    ## iter  70 value 2045.703356
    ## iter  80 value 1685.359847
    ## iter  90 value 1390.431291
    ## iter 100 value 1094.132361
    ## iter 110 value 851.710522
    ## iter 120 value 740.144062
    ## iter 130 value 709.668318
    ## iter 140 value 689.771086
    ## iter 150 value 674.008698
    ## iter 160 value 651.267289
    ## iter 170 value 626.328019
    ## iter 180 value 598.129073
    ## iter 190 value 583.316789
    ## iter 200 value 571.559027
    ## iter 210 value 564.668005
    ## iter 220 value 557.448318
    ## iter 230 value 552.495720
    ## iter 240 value 548.261987
    ## iter 250 value 546.239350
    ## iter 260 value 544.746378
    ## iter 270 value 544.427243
    ## iter 280 value 542.658704
    ## iter 290 value 540.165103
    ## iter 300 value 538.053668
    ## iter 310 value 537.354902
    ## iter 320 value 536.693358
    ## iter 330 value 535.338649
    ## iter 340 value 533.745362
    ## iter 350 value 532.213371
    ## iter 360 value 530.308140
    ## iter 370 value 524.757193
    ## iter 380 value 518.230219
    ## iter 390 value 515.073402
    ## iter 400 value 514.708494
    ## iter 410 value 513.896569
    ## iter 420 value 513.434299
    ## iter 430 value 513.319079
    ## iter 440 value 512.380652
    ## iter 450 value 510.490203
    ## iter 460 value 509.987219
    ## iter 470 value 509.185482
    ## iter 480 value 508.732026
    ## iter 490 value 507.796634
    ## iter 500 value 505.279531
    ## iter 510 value 502.620732
    ## iter 520 value 500.671600
    ## iter 530 value 500.139222
    ## iter 540 value 498.961107
    ## iter 550 value 496.731865
    ## iter 560 value 492.952960
    ## iter 570 value 486.638769
    ## iter 580 value 481.465760
    ## iter 590 value 473.729518
    ## iter 600 value 468.763050
    ## iter 610 value 464.952939
    ## iter 620 value 461.137585
    ## iter 630 value 441.443082
    ## iter 640 value 428.590227
    ## iter 650 value 420.050003
    ## iter 660 value 417.665600
    ## iter 670 value 415.272254
    ## iter 680 value 413.297686
    ## iter 690 value 412.193591
    ## iter 700 value 412.141610
    ## iter 710 value 410.604195
    ## iter 720 value 409.150714
    ## iter 730 value 406.321867
    ## iter 740 value 403.871113
    ## iter 750 value 401.770781
    ## iter 760 value 400.198676
    ## iter 770 value 399.253176
    ## iter 780 value 395.789543
    ## iter 790 value 393.772333
    ## iter 800 value 392.144025
    ## iter 810 value 390.752505
    ## iter 820 value 389.761456
    ## iter 830 value 388.863030
    ## iter 840 value 388.015283
    ## iter 850 value 387.448169
    ## iter 860 value 386.611507
    ## iter 870 value 386.115804
    ## final  value 386.114771 
    ## converged

``` r
creditcard.nn
```

    ## a 30-9-1 network with 289 weights
    ## inputs: Time V1 V2 V3 V4 V5 V6 V7 V8 V9 V10 V11 V12 V13 V14 V15 V16 V17 V18 V19 V20 V21 V22 V23 V24 V25 V26 V27 V28 Amount 
    ## output(s): trainset$Class 
    ## options were - entropy fitting  decay=0.025

functions

``` r
 misclass.nnet <- function(fit,y) {
temp <- table(predict(fit,type="class"),y)
cat("Table of Misclassification\n")
cat("(row = predicted, col = actual)\n")
print(temp)
cat("\n\n")
numcor <- sum(diag(temp))
numinc <- length(y) - numcor
mcr <- numinc/length(y)
cat(paste("Misclassification Rate = ",format(mcr,digits=3)))
cat("\n")
  }
```

``` r
misclass.nnet(creditcard.nn,trainset$Class)
```

    ## Table of Misclassification
    ## (row = predicted, col = actual)
    ##    y
    ##          0      1
    ##   0 213204     43
    ##   1     32    326
    ## 
    ## 
    ## Misclassification Rate =  0.000351

``` r
creditcard.nn2 = nnet(trainset$Class~.,data=trainset,size=15,decay=.05,maxit=5000)
```

    ## # weights:  481
    ## initial  value 67437.207930 
    ## iter  10 value 2718.305334
    ## iter  20 value 2716.000763
    ## iter  30 value 2491.106474
    ## iter  40 value 1348.397899
    ## iter  50 value 960.872495
    ## iter  60 value 897.126767
    ## iter  70 value 868.301744
    ## iter  80 value 843.938262
    ## iter  90 value 823.407067
    ## iter 100 value 814.662470
    ## iter 110 value 813.190607
    ## iter 120 value 800.857901
    ## iter 130 value 753.420267
    ## iter 140 value 725.888268
    ## iter 150 value 705.542384
    ## iter 160 value 692.576726
    ## iter 170 value 674.331226
    ## iter 180 value 661.386526
    ## iter 190 value 635.320541
    ## iter 200 value 606.341544
    ## iter 210 value 594.792160
    ## iter 220 value 584.215279
    ## iter 230 value 573.197060
    ## iter 240 value 563.154655
    ## iter 250 value 553.849649
    ## iter 260 value 547.616165
    ## iter 270 value 546.555228
    ## iter 280 value 546.106116
    ## final  value 546.032796 
    ## converged

``` r
misclass.nnet(creditcard.nn2,trainset$Class)
```

    ## Table of Misclassification
    ## (row = predicted, col = actual)
    ##    y
    ##          0      1
    ##   0 213217     94
    ##   1     19    275
    ## 
    ## 
    ## Misclassification Rate =  0.000529

now with the test data

``` r
creditcard.nn3 = nnet(trainset$Class~.,data=trainset,size=15,decay=.025,maxit=4000)
```

    ## # weights:  481
    ## initial  value 122897.982867 
    ## iter  10 value 69333.274576
    ## iter  20 value 2823.463988
    ## iter  30 value 2730.548762
    ## iter  40 value 2726.685110
    ## iter  50 value 2718.308467
    ## iter  60 value 2717.607283
    ## iter  70 value 2715.800981
    ## iter  80 value 2709.962546
    ## iter  90 value 1760.002334
    ## iter 100 value 1010.498918
    ## iter 110 value 785.952086
    ## iter 120 value 729.363365
    ## iter 130 value 698.291484
    ## iter 140 value 686.304103
    ## iter 150 value 674.233726
    ## iter 160 value 661.379569
    ## iter 170 value 649.998960
    ## iter 180 value 636.793127
    ## iter 190 value 614.324816
    ## iter 200 value 586.711651
    ## iter 210 value 579.050086
    ## iter 220 value 578.361464
    ## iter 230 value 575.103242
    ## iter 240 value 571.620995
    ## iter 250 value 569.282945
    ## iter 260 value 565.150353
    ## iter 270 value 558.255802
    ## iter 280 value 556.096291
    ## iter 290 value 554.849367
    ## iter 300 value 554.368358
    ## iter 310 value 550.453530
    ## iter 320 value 546.473686
    ## iter 330 value 538.941431
    ## iter 340 value 533.636987
    ## iter 350 value 528.388702
    ## iter 360 value 526.671076
    ## iter 370 value 525.356169
    ## iter 380 value 523.231865
    ## iter 390 value 522.225045
    ## iter 400 value 522.071495
    ## iter 410 value 521.817256
    ## iter 420 value 520.506066
    ## iter 430 value 520.064640
    ## iter 440 value 519.607088
    ## iter 450 value 517.679026
    ## iter 460 value 514.897921
    ## iter 470 value 510.947491
    ## iter 480 value 503.132190
    ## iter 490 value 495.777389
    ## iter 500 value 493.400020
    ## iter 510 value 489.654285
    ## iter 520 value 485.298260
    ## iter 530 value 482.101655
    ## iter 540 value 480.071427
    ## iter 550 value 478.444286
    ## iter 560 value 473.780226
    ## iter 570 value 470.310077
    ## iter 580 value 467.606988
    ## iter 590 value 462.463599
    ## iter 600 value 460.894431
    ## iter 610 value 460.183521
    ## iter 620 value 459.333747
    ## iter 630 value 459.099442
    ## iter 640 value 458.900361
    ## iter 650 value 458.676843
    ## final  value 458.656854 
    ## converged

``` r
misclass.nnet(creditcard.nn,trainset$Class)
```

    ## Table of Misclassification
    ## (row = predicted, col = actual)
    ##    y
    ##          0      1
    ##   0 213204     43
    ##   1     32    326
    ## 
    ## 
    ## Misclassification Rate =  0.000351

``` r
str(testset)
```

    ## 'data.frame':    71202 obs. of  31 variables:
    ##  $ Time  : num  1 2 4 12 13 15 16 23 26 27 ...
    ##  $ V1    : num  -0.966 -0.426 1.23 -2.792 -0.437 ...
    ##  $ V2    : num  -0.185 0.961 0.141 -0.328 0.919 ...
    ##  $ V3    : num  1.793 1.1411 0.0454 1.6418 0.9246 ...
    ##  $ V4    : num  -0.863 -0.168 1.203 1.767 -0.727 ...
    ##  $ V5    : num  -0.0103 0.421 0.1919 -0.1366 0.9157 ...
    ##  $ V6    : num  1.2472 -0.0297 0.2727 0.8076 -0.1279 ...
    ##  $ V7    : num  0.23761 0.4762 -0.00516 -0.42291 0.70764 ...
    ##  $ V8    : num  0.3774 0.2603 0.0812 -1.9071 0.088 ...
    ##  $ V9    : num  -1.387 -0.569 0.465 0.756 -0.665 ...
    ##  $ V10   : num  -0.055 -0.3714 -0.0993 1.1511 -0.738 ...
    ##  $ V11   : num  -0.226 1.341 -1.417 0.845 0.324 ...
    ##  $ V12   : num  0.178 0.36 -0.154 0.793 0.277 ...
    ##  $ V13   : num  0.508 -0.358 -0.751 0.37 0.253 ...
    ##  $ V14   : num  -0.288 -0.137 0.167 -0.735 -0.292 ...
    ##  $ V15   : num  -0.6314 0.5176 0.0501 0.4068 -0.1845 ...
    ##  $ V16   : num  -1.06 0.402 -0.444 -0.303 1.143 ...
    ##  $ V17   : num  -0.68409 -0.05813 0.00282 -0.15587 -0.92871 ...
    ##  $ V18   : num  1.9658 0.0687 -0.612 0.7783 0.6805 ...
    ##  $ V19   : num  -1.2326 -0.0332 -0.0456 2.2219 0.0254 ...
    ##  $ V20   : num  -0.208 0.085 -0.22 -1.582 -0.047 ...
    ##  $ V21   : num  -0.108 -0.208 -0.168 1.152 -0.195 ...
    ##  $ V22   : num  0.00527 -0.55982 -0.27071 0.22218 -0.67264 ...
    ##  $ V23   : num  -0.1903 -0.0264 -0.1541 1.0206 -0.1569 ...
    ##  $ V24   : num  -1.1756 -0.3714 -0.7801 0.0283 -0.8884 ...
    ##  $ V25   : num  0.647 -0.233 0.75 -0.233 -0.342 ...
    ##  $ V26   : num  -0.222 0.106 -0.257 -0.236 -0.049 ...
    ##  $ V27   : num  0.0627 0.2538 0.0345 -0.1648 0.0797 ...
    ##  $ V28   : num  0.06146 0.08108 0.00517 -0.03015 0.13102 ...
    ##  $ Amount: num  123.5 3.67 4.99 58.8 0.89 ...
    ##  $ Class : Factor w/ 2 levels "0","1": 1 1 1 1 1 1 1 1 1 1 ...

``` r
creditcard.nn2 = nnet(trainset$Class~.,data=trainset,size=15,decay=.05,maxit=5000)
```

    ## # weights:  481
    ## initial  value 167043.611904 
    ## iter  10 value 8099.007366
    ## iter  20 value 7056.507715
    ## iter  30 value 7044.844965
    ## iter  40 value 5588.718920
    ## iter  50 value 5546.930072
    ## iter  60 value 5544.608221
    ## iter  70 value 5538.808382
    ## iter  80 value 5499.106186
    ## final  value 5499.097488 
    ## converged

``` r
misclass.nnet(creditcard.nn2,trainset$Class)
```

    ## Table of Misclassification
    ## (row = predicted, col = actual)
    ##    y
    ##          0      1
    ##   0 213236    369
    ## 
    ## 
    ## Misclassification Rate =  0.00173

``` r
yhat = predict(creditcard.nn2, newdata = testset, type ="class")
#misclass(yhat, testset$Class)
```
