## Randomized Complete Block Design 
```R
rm(list = ls())
# Create Dataframe
rcbd<-data.frame(trt=c("T1","T1","T1","T1","T1",
                       "T2","T2","T2","T2","T2",
                       "T3","T3","T3","T3","T3"),
                 litter=c("1","2","3","4","5",
                          "1","2","3","4","5",
                          "1","2","3","4","5"),
                 y=c(7.86,8.00,7.93,7.62,7.81,
                     7.76,7.73,7.74,7.43,7.44,
                     7.46,7.68,7.51,7.21,7.42),
                 stringsAsFactors = TRUE)
rcbd #See the Data

# ANOVA test

fm<-aov(y ~ trt + litter, data = rcbd) # Fit the ANOVA
summary(fm)                            # ANOVA Table

tm<-lm(y ~  trt + litter, data = rcbd) # Fit the linear model
summary(tm)                            # Linear Model Summary 

# Compare two Models
# tm1<-lm(y ~  litter, data = rcbd)
# anova(tm,tm1)

# Multiple comparisons

TukeyHSD(fm,"trt")         # Tukey test for multiple comparisons
plot(TukeyHSD(fm,"trt"))   # Plot for tukey test
aggregate(rcbd$y, by=list(rcbd$trt), FUN = mean) # Means by group

library(multcomp)
par(mar=c(5,4,6,2)) # Change parameters for the plot margins
tuk <- glht(fm, linfct=mcp(trt="Tukey")) # Fit the general Linear Hypotheses
plot(cld(tuk, level=0.05),col="lightgrey") # Plot the mean differences

#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# NOTE: to obtain type II and III SS use car package. 
# This defines a new function, Anova(), 
# which can calculate type II and III SS directly.
library(car)
# Type II
 Anova(lm(y ~ trt + litter, data=rcbd), type=2)

# Type III:
 Anova(lm(y ~ trt + litter, data=rcbd, contrasts = c("contr.sum", "contr.poly")), type=3)
 #~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
######################################

```
