## Mixed Nested
```R
rm(list = ls()) # Clean the workspace
#install.packages("lme4")  # If necesary install the library
library(lme4)              # Call the library to the workspace
library(car)               # Call the library to the workspace
library(lsmeans)           # Call the library to the workspace
library(multcomp)          # Call the library to the workspace

# Read the data
myfile<-"C:/Users/toledo/Dropbox/UNIPD/Biostatistics Curse  R Spring 2018/curso STAT PhD 2018 ANOVA/data/cows.txt"
mydata<-read.table(file=myfile,stringsAsFactors = TRUE,header = TRUE,sep = "\t")

options(contrasts = c("contr.SAS","contr.poly")) # Change contrast options
mydata$parity<-as.factor(mydata$parity)   # Set as factor
mydata$herd<-as.factor(mydata$herd)       # Set as factor

# Fit the mixed model
model.1<-lmer(milk ~ parity + dim + breed + (1 |breed:herd), data = mydata, REML = TRUE)
summary(model.1)            # Results of the mixed model
AIC(model.1)                # Akaike's Information Criterion (small is better)
BIC(model.1)                # Bayesian Information Criterion (small is better)
Anova(model.1, type=3,test.statistic = "F") # ANOVA table SS type III
lsmeans(model.1,"parity")      # LSM
lsmeans(model.1,"breed")      # LSM

# Model including just fixed effects
model.2<-lm(milk ~ parity + dim + breed + herd%in%breed, data = mydata)
summary(model.2)            # Results of the mixed model
anova(model.2) # ANOVA table 
lsmeans(model.2,"parity",test.statistic = "F")      # LSM
lsmeans(model.2,"breed")      # LSM
```
