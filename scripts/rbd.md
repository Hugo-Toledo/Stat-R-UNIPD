### RBD

```R
rm(list = ls())
# Create Dataframe
filedir<-"C:/Users/toledo/Dropbox/UNIPD/Biostatistics Curse  R Spring 2018/curso STAT PhD 2018 ExpDesign/rbd/rbd.txt"
BD<-read.table(file = filedir,stringsAsFactors = TRUE,header = TRUE, sep = "\t")

table(BD$Block,BD$Variety) #Frequency table for factors
table(BD$Block)
table(BD$Variety)
str(BD)
BD$Block<-as.factor(BD$Block)   # Set the numerical variable block as factor
str(BD)                         # See the structure of my data in file block
View(BD) #see all data

#contrasts(BD$Block)<-contr.SAS   # Set the contrast as SAS
#contrasts(BD$Variety)<-contr.SAS    # Set the contrast as SAS
mymodel<-lm(y ~ Variety + Block, data=BD)    # Fit the model with Nesting
summary(mymodel)                    # See the results
#anova(mymodel)                      # ANOVA table SS type III
fm<-aov(y ~  Variety + Block, data=BD) # Fit the ANOVA
summary(fm) # Linear Model Summary 

# LSM
# install.packages("lsmeans")
library(lsmeans)
lsmeans(fm,"Variety")          #LSM for Variety

# Multiple comparisons
TukeyHSD(fm,"Variety")         # Tukey test for multiple comparisons
plot(TukeyHSD(fm,"Variety"))   # Plot for tukey test
aggregate(BD$y, by=list(BD$Variety), FUN = mean) # Means by group


library(multcomp)
par(mar=c(5,4,6,2)) # Change parameters for the plot margins
tuk <- glht(fm, linfct=mcp(Variety="Tukey")) # Fit the general Linear Hypotheses
plot(cld(tuk, level=0.05),col="lightgrey") # Plot the mean differences

# Orthogonal Contrasts For Variety


c1<-c(1,1,-1,-1)     # Create a column vector with coefficients for contrast of the first two levels against the last two

c2<-c(1,-1, 0,0)     # Create a column vector with coefficients for contrast within the first two level
c3<-c(0,0,1,-1)      # Create a column vector with coefficients for contrast within the last two level
mat<-cbind(c1,c2,c3)  # create a matrix joining the two vectors of coefficients for contrast 1 and contrast 2
#mat<-matrix(c(1,1,-1,-1,1,-1,0,0,0,0,1,-1),ncol=3)  # Create the contrast directly as matrix for treatment vitb12 considering the order HIGH, LOW, NONE
model1<-aov(y ~ Variety + Block, contrasts = list(Variety=mat), data=BD) # Fit the linear model and orthogonal contrast
summary.aov(model1,split=list(Variety=list("Americane vs Europee"=1,
                                           "Entro Americane"=2,
                                           "Entro Europee"=3)))
```
