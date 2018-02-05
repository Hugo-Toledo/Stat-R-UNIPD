```r
# Reads data directly from WEB 
filedir<-"https://raw.githubusercontent.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/master/data/latte-12-02_en.txt"
cows<-read.table(file = filedir,stringsAsFactors = FALSE,header = TRUE, sep = "\t")

######################################
#  Descriptive Statistics and Normality Test

milk<-cows$milk      # Select the variable 
summary(milk)        # Basic statistics
sd(milk)             # Standard Deviation function
range(milk)          # Range function
shapiro.test(milk)   # Shapiro - Wilk normality test
# install.packages("car") ?
car::leveneTest(milk ~ as.factor(breed), data=cows) #Levene’s test

# Density plot with normal distribution curve 
plot(density(milk), col=4, main="Milk")
curve(dnorm(x, mean = mean(milk), sd = sd(milk)), add = T, col=3)

# Histogram  with normal distribution curve
hist(milk, breaks = 10, freq = FALSE)
curve(dnorm(x, mean = mean(milk), sd = sd(milk)), add = T, col=3)

# Q-Q Plot
qqnorm(cows$milk)
qqline(cows$milk)

#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#NOTE: the library psych has a function 
#to describe data including  test for kurtosis and skew

#install.packages("psych")
#library(psych)
#describe(milk,skew = TRUE,ranges = TRUE,quant = c(0.1,0.99))
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

```
