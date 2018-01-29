## Contrasts
```R
rm(list = ls())
# Create Dataframe
filedir<-"https://raw.githubusercontent.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/master/data/lambs.csv"
es1<-read.table(file = filedir,stringsAsFactors = TRUE,header = TRUE, sep = ",")

head(es1) #See the Data
table(es1$sex,es1$breed, by=es1$treatment) #Frequency table for factors

fm<-aov(slaughtering_weight ~ sex + breed + treatment, data=es1) # Fit the ANOVA
summary(fm) # ANOVA table

tm<-lm(slaughtering_weight ~ sex + breed + treatment, data=es1) # Fit the linear model
summary(tm) # Linear Model Summary 

# LSM
library(lsmeans)
lsmeans(tm,"sex")          #LSM for sex
lsmeans(tm,"breed")        #LSM for breed
lsmeans(tm,"treatment")    #LSM for treatment

# Contrasts
#tm$contrasts$sex 
#tm$contrasts$breed
#tm$contrasts$treatment
contrasts(es1$sex)         #Grid for contrasts
contrasts(es1$breed)         #Grid for contrasts
contrasts(es1$treatment)         #Grid for contrasts

fm<-aov(slaughtering_weight ~ sex + breed + treatment + age_beginning, data=es1) # Fit the ANOVA
summary(fm) #ANOVA table

tm<-lm(slaughtering_weight ~ sex + breed + treatment + age_beginning, data=es1) # Fit the linear model
summary(tm) # Linear Model Summary 

#contrasts(es1$sex)<-c(1,0)
contrasts(es1$sex)<-contr.SAS          #Change contrast grid 
#contrasts(es1$breed)<-cbind(c(1,0,0), c(0,1,0))
contrasts(es1$breed)<-contr.SAS        #Change contrast grid
#contrasts(es1$treatment)<-cbind(c(1,0,0), c(0,1,0))
contrasts(es1$treatment)<-contr.SAS    ##Change contrast grid

fm1<-aov(slaughtering_weight ~ sex + breed + treatment + age_beginning, data=es1) # Fit the ANOVA
summary(fm1) #Anova table

tm1<-lm(slaughtering_weight ~ sex + breed + treatment + age_beginning, data=es1) # Fit the linear model
summary(tm1) # Linear Model Summary 
Anova(tm1, type = "III") #Anova table with SS III
lsmeans(tm1,"sex")         #LSM for sex
lsmeans(tm1,"breed")       #LSM for breed
lsmeans(tm1,"treatment")   #LSM for treatment


#############################
# Orthogonal Contrasts
```R
#c1<-c(-1,-1,2)
#c2<-c(1,-1, 0)
#mat1<-cbind(c1,c2)
mat1<-matrix(c(-1,-1,2,
                1,-1,0),ncol=2)  # Create the contrast for treatment
mat2<-matrix(c(1,-1,0),ncol = 1) # Create the contrast for breed

#contrasts(es1$treatment)<-mat1
#contrasts(es1$breed)<-mat2
model1<-aov(slaughtering_weight ~ sex + breed + treatment + age_beginning, 
            contrasts = list(treatment=mat1, breed=mat2), data=es1) # Fit the linear model
#ANOVA table with the effects splited for each contrast
summary.aov(model1,split=list(treatment=list("Secco vs Pascolo"=1,"CLA vs noCLA"=2),
                        breed=list("Brogna vs Alpagata"=1)))  
# Polynomial Contrasts#
mat3<-matrix(c(-1,0,1,
               1,-2,1),ncol=2)   #Create the contrast for treatment Linear and Quadratic
#contrasts(es1$treatment)<-mat3
#contrasts(es1$breed)<-contr.SAS
model2<-aov(slaughtering_weight ~ sex + breed + treatment + age_beginning, 
            contrasts=list(treatment=mat3),data=es1) # Fit the linear model
#ANOVA table with the effects splited for the contrast
summary.aov(model2,split=list(treatment=list("Linear"=1,"Quadratic"=2)))

attributes(model2$qr$qr) # See the model grid

#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# NOTE: Another way to obtain the constrast
#library(multcomp)
#contr<-rbind("Linear"=c(-1,0,1),
#             "Quadratic"=c(1,-2,1))
#model3<-glht(fm1,linfct=mcp(treatment=contr))
#summary(model4)
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
######################################
```
