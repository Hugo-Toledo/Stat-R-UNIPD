## Split Plot

```R
rm(list = ls())      # Clean the workspace
library(lsmeans)     # Call the library
# Read Data
mydata<-read.table(file = "../Dropbox/UNIPD/Biostatistics Curse  R Spring 2018/curso STAT PhD 2018 ExpDesign/data/splitplot.txt",
                     sep = "\t",header = TRUE,stringsAsFactors = TRUE)
mydata$Room<-as.factor(mydata$Room)    # Set the variable as factor
str(mydata)                            # See the structure of my data
contrasts(mydata$Energy)<-contr.SAS    # Set the contrast as SAS
contrasts(mydata$Protein)<-contr.SAS   # Set the contrast as SAS
contrasts(mydata$Room)<-contr.SAS      # Set the contrast as SAS

table(mydata$Energy,mydata$Protein,mydata$Room) # Frequencies for factors

mymodel<-lm(ADG ~ Room + Energy + Room:Energy + Protein + Energy:Protein, data = mydata )   # fit the model with interactionssummary(mymodel)              # See the results
anova(mymodel)                # ANOVA table SS type I
#ref.grid(mymodel)
lsmeans(mymodel,"Protein")    # LSM for factor
lsmeans(mymodel,"Energy")     # LSM for factor
lsmeans(mymodel,~Energy:Protein) # LSM for factor with interaction

# Fit the model with the interaction as an error term
mymodel.1<-aov(ADG ~ Room + Energy + Error(Room:Energy) + Protein + Energy:Protein, data = mydata)
summary(mymodel.1) # See the results
lsmeans(mymodel.1,"Energy") # LSM for factor interaction
```
