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
fm<-aov(milk ~ food, data = foods)  # Fit the ANOVA
summary(fm)                         # ANOVA table

# Multiple comparisons

TukeyHSD(fm)                  # Tukey test for multiple comparisons
plot(TukeyHSD(fm))            # Plot for tukey test
aggregate(foods$milk, by=list(foods$food), FUN = mean) # Means by group

library(multcomp)
par(mar=c(5,4,6,2))           # Change parameters for the plot margins
tuk <- glht(fm, linfct=mcp(food="Tukey")) # Fit the general Linear Hypotheses
plot(cld(tuk, level=0.05),col="lightgrey")   # Plot the mean differences

```
