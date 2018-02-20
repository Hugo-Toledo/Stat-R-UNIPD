
## Nested Model

```R
rm(list = ls())   # Clean the workspace
library(lsmeans)  # Call the library
# Read Data
mydata<-read.table(file = "../Dropbox/UNIPD/Biostatistics Curse  R Spring 2018/curso STAT PhD 2018 ExpDesign/data/nested.txt",
                     sep = "\t",header = TRUE,stringsAsFactors = TRUE)
mydata$Boar<-as.factor(mydata$Boar) # Set the variable as factor
str(mydata)                         # See the structure of my data
contrasts(mydata$Boar)<-contr.SAS   # Set the contrast as SAS
contrasts(mydata$Sow)<-contr.SAS    # Set the contrast as SAS
table(mydata$Sow,mydata$Boar)       # Frequencies for factors


mymodel<-lm(ADG ~ Boar + Sow%in%Boar, data = mydata )    # Fit the model with Nesting
summary(mymodel)                    # See the results
anova(mymodel)                      # ANOVA table SS type III
#ref.grid(mymodel)
lsmeans(mymodel,"Boar")             # LSM for factor
lsmeans(mymodel,"Sow")              # LSM for factor
mymodel.1<-aov(ADG ~ Boar + Error(Sow), data = mydata)   # Set the factor as an error term
summary(mymodel.1)                  # See the results
```
