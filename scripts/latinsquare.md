## Latin Square
```R
rm(list = ls())
# Create Dataframe
latinsquare<-data.frame(period=c("1","2","3",
                        "1","2","3",
                        "1","2","3"),
                 animal=c("1","1","1",
                         "2","2","2",
                         "3","3","3"),
                 diet=c("a","b","c",
                        "b","c","a",
                        "c","a","b"),
                 y=c(823.2,869.4,928.2,
                     945.0,1037.4,869.4,
                     970.2,894.6,924.0),
                 stringsAsFactors = TRUE)
latinsquare #See the Data
#str(latinsquare)

# Three-Way ANOVA test

fm<-aov(y ~ animal + period + diet, data = latinsquare) # Fit the ANOVA
summary(fm)                            # ANOVA Table


mymodel<-lm(y ~ animal + period + diet, data = latinsquare)    # Fit the model with Nesting
summary(mymodel)                    # See the results
anova(mymodel)                      # ANOVA table SS type III

tm<-lm(y ~ animal + period + diet, data = latinsquare) # Fit the linear model
summary(tm)                            # Linear Model Summary 

# LSM
# install.packages("lsmeans")
library(lsmeans)
lsmeans(tm,"diet")          #LSM for diet


# Multiple comparisons

TukeyHSD(fm,"diet")         # Tukey test for multiple comparisons
plot(TukeyHSD(fm,"diet"))   # Plot for tukey test
aggregate(latinsquare$y, by=list(latinsquare$diet), FUN = mean) # Means by group


library(multcomp)
par(mar=c(5,4,6,2)) # Change parameters for the plot margins
tuk <- glht(fm, linfct=mcp(diet="Tukey")) # Fit the general Linear Hypotheses
plot(cld(tuk, level=0.05),col="lightgrey") # Plot the mean differences
```
