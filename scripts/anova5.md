## Completely Randomized Design with a covariate
```R
rm(list = ls())

gain<-data.frame(trt=c("A","A","A","A","A",
                       "B","B","B","B","B",
                       "C","C","C","C","C"),
                 in_weight=c(350,400,360,350,340,
                             390,340,410,430,390,
                             400,320,330,390,420),
                 gain=c(970,1000,980,980,970,
                       990, 950,980,990,980,
                       990,940,930,1000,1000),
                 stringsAsFactors = TRUE)
gain

contrasts(gain$trt)<-contr.SAS

tm<-lm(gain ~ in_weight + trt, data=gain) # Fit the linear model
summary(tm) 
fm<-aov(gain ~ in_weight + trt, data=gain) # Fit the ANOVA
summary(fm) #ANOVA table

car::Anova(tm,type="III") #Anova table with SS III

TukeyHSD(fm,"trt")         # Tukey test for multiple comparisons
plot(TukeyHSD(fm,"trt"))   # Plot for tukey test
aggregate(gain$gain, by=list(gain$trt), FUN = mean) # Means by group
lsmeans::lsmeans(tm,"trt")          #LSM for treatment

library(multcomp)
par(mar=c(4,4,6,2)) # Change parameters for the plot margins
tuk <- multcomp::glht(fm, linfct=multcomp::mcp(trt="Tukey")) # Fit the general Linear Hypotheses
plot(multcomp::cld(tuk, level=0.05),col="lightgrey") # Plot the mean differences
```
