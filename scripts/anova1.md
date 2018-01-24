## One-Way ANOVA
```R
# Example 1, One Way ANOVA
# Create Dataframe
foods<-data.frame(milk=c(25.40,26.31,24.10,23.74,25.10,
                         23.40,21.80,23.50,22.75,21.60,
                         20.00,22.20,19.75,20.60,20.40),
                  food=c("Food1","Food1","Food1","Food1","Food1",
                         "Food2","Food2","Food2","Food2","Food2",
                         "Food3","Food3","Food3","Food3","Food3"),
                  stringsAsFactors = TRUE)

# ANOVA test
fm<-aov(milk ~ food, data = foods)
summary(fm)
# Multiple comparisons

TukeyHSD(fm)
plot(TukeyHSD(fm))
aggregate(foods$milk, by=list(foods$food), FUN = mean)

library(multcomp)
par(mar=c(5,4,6,2))
tuk <- glht(fm, linfct=mcp(food="Tukey"))
plot(cld(tuk, level=0.05),col="lightgrey")

#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# NOTE: to obtain type II and III SS use car package. 
# This defines a new function, Anova(), 
# which can calculate type II and III SS directly.

# Type II
# Anova(lm(var ~ fac1 * fac2, data=data, type=2))

# Type III:
# Anova(lm(var ~ fac1 * fac2, data=data, contrasts=list(topic=contr.sum, sys=contr.sum)), type=3))
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
######################################

```


