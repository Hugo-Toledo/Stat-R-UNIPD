# :clipboard: Applied-Statistics-R-UNIPD

The overall course goal is to give the participants knowledge on statistical methods and data analysis, with particular emphasis on the application techniques using R software.

Professors:

* Alessio Cecchinato, :e-mail: alessio.cecchinato@unipd.it
* Roberto Mantovani, :e-mail: roberto.mantovani@unipd.it
* Cristina Sartori, :e-mail: cristina.sartori@unipd.it
* Hugo Toledo, :e-mail: hugooswaldo.toledoalvarado@phd.unipd.it or h.toledo.a@gmail.com

Class meets: 
   * February 6, 7 & 8 from 9:00am to 12:00pm, at Aula 12 Pentagono.
   * Tuesday 20, aula 2 - prima stecca, 9 - 12 pm - - Mantovani
   * Tuesday 20, aula 2  - prima stecca, 14 -17:30 - - Cristina
   * Thursday 22, aula 1 - 2nda stecca, 11 - 13:30 - - Cristina
	* Thursday 22, aula 2 - 2nda stecca, 14:30 - 18:00 - - Cristina

1. please bring your own laptop with R software already installed.
2. please verify that you have one internet connection ('eduroam' or others) working properly.
3. please download the slides from this webpage

You can install R directly from https://www.r-project.org/, also you can install RStudio (https://www.rstudio.com/) to have a nice interface. 
If you are a complete beginner with **R**, I recommend reading this brief [**introduction**.](books/Torfs_Brauer-Short-R-Intro.pdf)
For the course you need the following packages:
```R
install.packages("car")
install.packages("multcomp")
install.packages("lsmeans")
install.packages("lme4") # For mixed models course
```

## :notebook: Slides

1. [**Cecchinato ANOVA**](slides/applied_statistics_R_2018.pdf)

2.1 [**Mantovani Exp. Designs**](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/slides/Analysis%20of%20Variance.pdf)

2.2 [**Mantovani Experimental Plans**](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/slides/Experimental%20plans.pdf)

3.1 [**Cristina Mixed Models**](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/slides/Mixed_models_PhD_2018_parts_I_%26_II.pdf)
3.2 [**Cristina Mixed Models**](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/slides/Mixed_models_PhD_2018_parts_III_%26_IV.pdf)

## :bicyclist: Exercises

* [Soils](exercises/ex_soils.md) 
   * [PDF with solutions](exercises/Excercise_Soils.pdf)

## :computer: R scripts

If you want to use the scripts, please select, copy and paste the script in R. Otherwise you can download the PDF with the solutions. 
1. [Descriptive Statistics and Normality](scripts/normal.md)
    * [PDF with solutions](scripts/1.0_Normality.pdf)
2. [One-Way ANOVA](scripts/anova1.md)
    * [PDF with solutions](scripts/2.0_ANOVA.pdf)
3. [Complete Randomized Block Design](scripts/anova2.md)
    * [PDF with solutions](scripts/3.0_ANOVA_rcbd.pdf)
4. [Two-Way ANOVA](scripts/anova3.md)
    * [PDF with solutions](scripts/4.0_Two_Way_ANOVA.pdf)
5. [Contrasts](scripts/anova4.md)
    * [PDF with solutions](scripts/5.0_ANOVA_Contrasts.pdf)
6. [Completely Randomized Design with a Covariate](scripts/anova5.md)
    * [PDF with solutions](scripts/6.0_ANOVA_CRD_Covariate.pdf)
------
7. [Random Block Design](scripts/rbd.md)

8. [Latin Square](scripts/latinsquare.md)
	
9. [Nested](scripts/nested.md)
    * [PDF with solutions](scripts/1.0_Nested.pdf)	
10. [Split Plot](scripts/splitplot.md)
    * [PDF with solutions](scripts/2.0_SplitPlot.pdf)

	[For Loop](scripts/forloop.md)
------

11. [Mixed Models 1](scripts/mix1.md)
    * [PDF with solutions](scripts/1.0_Mixed.pdf)
12. [Mixed Models RBD]()
    * [PDF with solutions](scripts/2.0_Mixed_rbd.pdf)
13. [Mixed Models Nested]()
    * [PDF with solutions](scripts/3.0_Mixed_Nest.pdf)
14. [Mixed Models Repeated Measures]()
    * [PDF with solutions](scripts/4.0_Mixed_Rep.pdf)

## :page_with_curl: Datasets 

To save a file to your pc, click it to view the contents within the GitHub, then in the top right, **right click** the **Raw** button, then **save as...**   :floppy_disk: 

 * [Cows](data/latte-12-02_en.txt)
 * [Foods](data/foods.txt)
 * [Pigs](data/pigs.txt)
 * [Vitamins](data/vits.txt)
 * [Lambs](data/lambs.csv)
 * [Gain](data/gain.txt)
 
 ------
 
 * [RBD](data/rbd.txt)
 * [Latin Square](data/LatinSquare.txt)
 
 ------
 
 * [Mixed Models 1](data/cows.txt)
 * [Mixed Models RBD](data/yield_rbd.txt)
 * [Mixed Models Nested](data/latte-12-02_en.txt)
 * [Mixed Models Repeated Measures](data/rep.txt)
 
 
## :books: Textbooks and Suplemental Readings

* [Elementary Statistics](books/Larson_and_Farber_Elementary_Statistics_Picturing_the_World_5th_ed.pdf)
* [Short-Refcard](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/books/Short-refcard.pdf)
* [R in Action: Book](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/books/R%20IN%20ACTION_%20Data%20analysis%20and%20graphics%20with%20R%20-%20Robert%20I.%20Kabacoff.pdf)
* [The R Book: Book](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/books/The%20R%20Book%20.pdf)
* [LSMeans in R](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/books/LSMeans%20R.pdf)
* [Formula Notation in R](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/books/formulanotation.pdf)
* [Mixed Models in R](https://github.com/Hugo-Toledo/Applied-Statistics-R-UNIPD/blob/master/books/lme4_R.pdf)

## :globe_with_meridians: Usefull Links

* https://www.rdocumentation.org/
* https://www.statmethods.net/index.html
* https://stackoverflow.com
* https://stats.idre.ucla.edu/r/
