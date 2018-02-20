## Mixed Models

```R
rm(list = ls()) # Clean the workspace 
# Read the data
cows<-read.table(file="../Dropbox/UNIPD/Biostatistics Curse  R Spring 2018/curso STAT phD 2018 Mixed Models/data/cows.txt",
                  stringsAsFactors = TRUE,header = TRUE,sep = "\t")
cows$parity<-as.factor(cows$parity) # Set parity as factor
cows$herd<-as.factor(cows$herd)     # Set herd as factor
contrasts(cows$parity)<-contr.SAS   # Change the reference grid to SAS   
contrasts(cows$herd)<-contr.SAS     # Change the reference grid to SAS

#install.packages("lme4")  # If necesary install the library
library(lme4)              # Call the library to the workspace
library(car)               # Call the library to the workspace
library(lsmeans)           # Call the library to the workspace
# Fit the model
lmm<-lmer(milk ~ parity + weight + (1 | herd) ,data = cows, REML = TRUE)
summary(lmm)            # Results of the mixed model
AIC(lmm)                # Akaike's Information Criterion (small is better)
BIC(lmm)                # ABayesian Information Criterion (small is better)
Anova(lmm, type=3,test.statistic = "F") # ANOVA table SS type III
lsmeans(lmm,"parity")      # LSM  
getME(lmm, name=c("X"))    #  Extract the matrix X 
getME(lmm, name=c("Z"))    #  Extract the matrix Z
getME(lmm, name=c("fixef"))#  Extract the BLUE
ranef(lmm)                 # Extract the BLUP

# Reshape Weight createing levels for weight
cows$weight_c<-NA
cows$weight_c[cows$weight <= 600]<-1
cows$weight_c[cows$weight > 600 & cows$weight <= 630]<-2
cows$weight_c[cows$weight > 630 & cows$weight <= 660]<-3
cows$weight_c[cows$weight > 660]<-4
table(cows$weight_c)
cows$weight_c<-as.factor(cows$weight_c) # Set Variable as Factor
contrasts(cows$weight_c)<-contr.SAS       # Set Contrasts as SAS
# Fit the model and test contrasts
lmm<-lmer(milk ~ parity + weight_c + (1 | herd) ,data = cows, REML = TRUE)
summary(lmm)            # Results of the mixed model
AIC(lmm)                # Akaike's Information Criterion (small is better)
BIC(lmm)                # ABayesian Information Criterion (small is better)
ranef(lmm)                 # Extract the BLUP
Anova(lmm, type=3,test.statistic = "F") # ANOVA table SS type III
lsmeans(lmm,"parity")      # LSM  
coef(lmm)                  # See the coefficients of you model
K <- matrix(c(0, 1, -1, 0, 0, 0), 1)   # Contrast Parity1 vs Parity2
t <- glht(lmm, linfct = K)             # fit a general linear hipotesis test 
summary(t)                             # See the results
K <- matrix(c(0, 0, 1, 0, 0, 0), 1)    # Contrast Parity2 vs Parity3   
t <- glht(lmm, linfct = K)             # fit a general linear hipotesis test
summary(t)                             # See the results
K <- matrix(c(0, 1, 1, 0, 0, 0), 1)    # Contrast Parity1+Parity2 vs Parity3
t <- glht(lmm, linfct = K)             # fit a general linear hipotesis test
summary(t)                             # See the results

```
