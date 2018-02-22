## Mixed RBD
```R
rm(list = ls()) # Clean the workspace 
#install.packages("lme4")  # If necesary install the library
library(lme4)              # Call the library to the workspace
library(car)               # Call the library to the workspace
library(lsmeans)           # Call the library to the workspace
library(multcomp)          # Call the library to the workspace

# Read the data
rbd<-read.table(file="../Dropbox/UNIPD/Biostatistics Curse  R Spring 2018/curso STAT phD 2018 Mixed Models/data/yield_rbd.txt",
                 stringsAsFactors = TRUE,header = TRUE,sep = "\t")

rbd$block<-as.factor(rbd$block)           # Set block as factor
rbd$fertilizer<-as.factor(rbd$fertilizer) # Set fertilizer as factor
contrasts(rbd$block)<-contr.SAS           # Change the reference grid to SAS   
contrasts(rbd$fertilizer)<-contr.SAS      # Change the reference grid to SAS

# Fit the linear model
model.1<-lm(yield ~ fertilizer + block, data=rbd) # Fit the model
summary(model.1)                             # See the results
Anova(model.1, type=3,test.statistic = "F")  # ANOVA table SS type III
lsmeans(model.1,"fertilizer")                # LSM for factor

# Fit the mixed model
model.2<-lmer(yield ~ fertilizer + (1 | block) ,data = rbd, REML = TRUE)
summary(model.2)            # Results of the mixed model
AIC(model.2)                # Akaike's Information Criterion (small is better)
BIC(model.2)                # Bayesian Information Criterion (small is better)
Anova(model.2, type=3,test.statistic = "F") # ANOVA table SS type III
lsmeans(model.2,"fertilizer")      # LSM  
```
