## Two-Way ANOVA
```R

rm(list = ls())
# Create Dataframe
gain<-data.frame(vitI=c("1","1","1","1","1",
                        "1","1","1","1","1",
                        "2","2","2","2","2",
                        "2","2","2","2","2"),
                 vitII=c("1","1","1","1","1",
                         "2","2","2","2","2",
                         "1","1","1","1","1",
                         "2","2","2","2","2"),
                 gain=c(0.585,0.536,0.458,0.486,0.536,
                        0.567,0.545,0.589,0.536,0.549,
                        0.473,0.450,0.869,0.473,0.464,
                        0.684,0.702,0.900,0.698,0.693),
                 stringsAsFactors = TRUE)
gain #See the Data

# Two-Way ANOVA test

fm<-aov(gain ~ vitI + vitII + vitI*vitII, data = gain) # Fit the ANOVA
summary(fm)                            # ANOVA Table

tm<-lm(gain ~ vitI + vitII + vitI*vitII, data = gain) # Fit the linear model
summary(tm)                            # Linear Model Summary 

# LSM
library(lsmeans)
lsmeans(tm,"vitI")
lsmeans(tm,"vitII")
summary(ref.grid(tm))
aggregate(gain$gain, by=list(gain$vitI,gain$vitII), FUN = mean) # Means by group

#contrast(ref.grid(tm))

# Multiple comparisons

TukeyHSD(fm)         # Tukey test for multiple comparisons
plot(TukeyHSD(fm))   # Plot for tukey test

par(mar=c(3,4,3,2)) # Change parameters for the plot margins
interaction.plot(gain$vitI,gain$vitII,response = gain$gain,
               col=c("red","blue"),pch = c(16,18),
               main="Interaction Between VitI and VitII",
               ylab = "gain (kg)")

#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# NOTE: With the package "HH" you can get an overview of the main factors 
#install.packages("HH")
#library(HH)
#interaction2wt(gain$gain ~ gain$vitI + gain$vitII + gain$vitI*gain$vitII)
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
######################################
```
