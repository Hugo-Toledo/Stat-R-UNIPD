## For loop

```R
rm(list = ls())      # Clean the workspace
# Read Data
myfile<-"../Dropbox/UNIPD/Biostatistics Curse  R Spring 2018/curso STAT PhD 2018 ExpDesign/data/nested2.txt" 
mydata<-read.table(file = myfile,sep = "\t",header = TRUE,stringsAsFactors = TRUE)
mydata$Boar<-as.factor(mydata$Boar) # Set the variable as factor
str(mydata)                         # See the structure of my data

#### Linear Model in a for loop
# To store the results directly in a file use:
sink("../Dropbox/UNIPD/Biostatistics Curse  R Spring 2018/curso STAT PhD 2018 ExpDesign/data/results.txt",append = FALSE)
# For loop to do the analysis for several variables
for (i in 4:5){    # For the 4 and 5 column  
   y <- mydata[,i] # Select the column i
   print(paste0("Results for ",colnames(mydata)[i]))  # Print the number of the variable
   print("######################################")    # 
   mymodel<-aov(y ~ mydata$Boar + Error(mydata$Sow))    # Fit the ANOVA model
   print(summary(mymodel))                            # See the results
   print("######################################")
}
sink() # Return the result to the R console
```
