## Mixed Repeated Measures

```R
rm(list = ls()) # Clean the workspace 
#install.packages("nlme")  # If necesary install the library
library(lsmeans)           # Call the library to the workspace
library(nlme)              # Call the library to the workspace

# Read the data
myfile<-"C:/Users/toledo/Dropbox/UNIPD/Biostatistics Curse  R Spring 2018/curso STAT phD 2018 Mixed Models/data/rep.txt"
mydata<-read.table(file=myfile,stringsAsFactors = TRUE,header = TRUE,sep = "\t")
options(contrasts = c("contr.SAS","contr.poly")) # Change contrast options
mydata$animal<-as.factor(mydata$animal)   # Set as factor
mydata$age<-as.factor(mydata$age)         # Set as factor

# Different covariance Structures
# Model Unstructured
model.un<-gls(bw ~  group + age + group*age, data = mydata,    # Model
              correlation = corSymm(form = ~ 1|group/animal),  # General correlation matrix, unstructure.
              weights = varIdent(form = ~ 1|age))              # Constant variance(s), used to allow different 
                                                               # variances according to the levels of a classification factor.

model.un               # Model fitted
anova(model.un)        # ANOVA
lsmeans(model.un,"group") # LSM
cors<-corMatrix(model.un$modelStruct$corStruct)[[1]]  # Extract the Correlation Matrix
cors                                                  # See the Correlation Matrix
stdev.st<-c(1.000000, 1.546902, 1.730297, 2.234001, 
            2.801870, 2.891596, 3.275352, 3.353758)   # Get the stratum SD
vars<-stdev.st*model.un$sigma^2                       # Multiply the stratum SD by the Error Variance 
covs<-outer(vars,vars,function(x,y)sqrt(x)*sqrt(y))   # Get the Variance & Covariance Matrix
round(cors*covs,3)                                    # Get the R matrix: Covariance estimate for subjects

# Model Compound Symmetry Correlation Structure
model.cs<-gls(bw ~  group + age + group*age, data = mydata,    # Model
              correlation = corCompSymm(form = ~ 1|group/animal)) # Compound Symmetry Correlation Structure
model.cs              # Model fitted
anova(model.cs)       # ANOVA
lsmeans(model.cs,"group") # LSM
cors<-corMatrix(model.cs$modelStruct$corStruct)[[1]]  # Extract the Correlation Matrix
cors                                                  # See the Correlation Matrix
err.var<-model.cs$sigma^2                             # Err.Variance
round(cors*err.var,3)                                 # Get the R matrix: Covariance estimate for subjects

# A model with No Correlation looks like:
diag(1,8,8)*err.var

# Fit the same model with different types of variance and covariance

model.a<-lme(bw ~  group + age + group*age, data = mydata, # Model
             random = ~ 1|group/animal,                    # Random Effect
             weights = varIdent(form = ~ 1|age),           # Constant variance(s)
             correlation = NULL)                           # No correlation

#Doesn't converge
model.b<-lme(bw ~  group + age + group*age, data = mydata, # Model
             random = ~ 1|group/animal,                    # Random Effect
             weights = varIdent(form = ~ 1|age),           # Constant variance(s)
             correlation = corSymm())                      # Compound Symmetry Correlation Structure

model.c<-lme(bw ~  group + age + group*age, data = mydata, # Model
             random = ~ 1|group/animal,                    # Random Effect
             weights = varIdent(form = ~ 1|age),           # Constant variance(s)
             correlation = corAR1())                       # autocorrelation structure of order 1

model.d<-lme(bw ~  group + age + group*age, data = mydata, #  Model
             random = ~ 1|group/animal,                    # Random Effect
             correlation = corCompSymm())                  # Compound Symmetry Correlation Structure

anova(model.a,model.c,model.d)                             # Model Comparisson

```
