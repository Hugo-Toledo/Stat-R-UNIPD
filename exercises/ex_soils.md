# Homework

## 1st Part

Use the data "Soils" included in the package "car"  in R, it contains Soil characteristics measured on samples from three types of contours 
(Top, Slope, and Depression) and at four depths (0-10cm, 10-30cm, 30-60cm, and 60-90cm). The area was divided into 4 blocks, 
in a randomized block design.

Use *?Soil* to have more information about the data.

To open the data use: 
```R
library(car) 
data(soils)
ls()
```
### For the variable "N": 
   
   1. calculate the *mean*, *SD* and *range*.
   2. stablish the  hypothesis and test normality with *Shapiro-Wilk*. 
   3. analyse the distribution to test normality using a density plot with a normal distribution curve.
      - If there are outliers (*mean+3sd*) remove them and do again the previous steps.
      - If the variable does not have a normal distribution use a logaritmic transformation and do again the previous steps.
      To transform the variable you can use:
```R 
Soils$Log_N<-log(Soils$N) 
```
   4. calculate the means by **Depth**.
   5. stablish the hypothesis test using **Depth** as factor.
   6. fit an One-Way ANOVA using **Depth**, and interpret the results.
   7. fit the ANOVA with SS III, and interpret the results.
   8. use a multiple comparison test (*TukeyHSD*) for **Depth**, plot the LSM using the "multcomp" library,  and write your conclusions.

## 2nd Part

### For the variable "Mg": 
   
   1. calculate the *mean*, *SD* and *range*.
   2. stablish the  hypothesis and test normality with *Shapiro-Wilk*. 
   3. analyse the distribution to test normality using a density plot with a normal distribution curve.
      - If there are outliers (*mean+3sd*) remove them and do again the previous steps.
      - If the variable does not have a normal distribution use a logaritmic transformation and do again the previous steps.
      To transform the variable you can use:
```R 
Soils$Log_Mg<-log(Soils$Mg) 
```
   4. calculate the means of **Depth** by **Contour**.
   5. stablish the hypothesis test using **Depth** and **Contour** as factors.
   6. fit a Two-Way ANOVA using **Depth**, **Contour** (and interaction between them), and include **Block** as blocking factor, then interpret the results.
   7. fit the ANOVA with SS III for the previous model, and interpret the results.
   8. estimate the LSM for **Depth** and **Contour**
   9. use a multiple comparison test (*TukeyHSD*) for **Depth** and **Contour** and plot the LSM using the "multcomp" library.
   10. plot the interaction between **Depth** and **Contour**, then write your conclusions.
