---
title       : Body Mass Index, Body Fat Percentage and Ideal Weight
subtitle    : 
author      : Alvaro Botella
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

Defined overweight and obesity as an excess of body fat, the measure most used for diagnose them is the Body Mass Index (BMI). But, this measure underestimates the prevalence of overweight and obesity. It has been suggested that the Body Fat Percentage (BFP) is most util indicator to estimate the overweight and obesity, and thereby, prevent the health risk associated.

This application calculate the BMI (weight and height based) and the estimated BFP (BMI, gender and age based), and plotting each in a nutritional category graphic.

The BMI nutritional category has been obtained from [WHO-Europe nutritional page web](http://www.euro.who.int/en/health-topics/disease-prevention/nutrition/a-healthy-lifestyle/body-mass-index-bmi).And the formula for calculate BFP and the cutoff for BFP, and other related consults: [Gomez-Ambrosi, J.,et. al.](http://www.nature.com/ijo/journal/v36/n2/full/ijo2011100a.html)

--- .class #id 

## ui.R File (sidebar panel)

We need height and weight to calculate BMI ( \(BMI=\frac{weight}{height^2}\) ). And BMI, age and gender to calculate BFP

We collect these data using the folowing widgets:
- Numeric input (age and height). 


```r
numericInput("age", label = "Type your age in years",value = 0)
```

- Select box (gender). 


```r
selectInput("sex", label = "Select your gender", choices = list("Male" = 0, "Female" = 1), selected = 1)
```

- slider (weight) 

```r
sliderInput("weight", label = "Select your weight in Kg.", min = 30, max = 120, value = 65)
```

--- .class #id

## ui.R File (main panel)

We display the results subdivided the user interface into two sections (tabset mode). A section contain the intructions, an another the results. The instructions section is made inserting a markdown file. We show the code below.


```r
mainPanel(
        tabsetPanel(
                tabPanel ("Instructions", 
                                includeMarkdown("text.md")),                    
                tabPanel ("Results",
                        textOutput("text1"),              
                        plotOutput ("PlotBMI"),
                        br(),
                        br(),
                        textOutput ("text2"),  
                        plotOutput ("PlotBFP"))
                )
        )
```

--- .class #id

## Results, an example

The complete code is in [github](http://github.com/Abotella5/shareshinycode/tree/master/appShiny). We show the BMI and BFP text format, and a plot example here:


```
## [1] "Your BMI is: 24.5"
```

```
## [1] "Your BFP is: 24.2111775"
```

---

## The plot


```r
barplot(as.matrix(table(dat$categoryMal)), col= c("lightyellow", "lightgreen", "lightsalmon", "lightcoral"), beside = FALSE, axes = FALSE, 
   main="Your Nutritional Status by BFP (MALES)", ylab = "BFP")
 axis(side = 2, at = c(0, 100, 200, 300, 400, 500),labels = c("0", "10", "20", "30", "40", "50"))
 text (x=0.7, y=25, "Underweight"); text (x=0.7, y=130, "Normal weight")
 text (x=0.7, y=225, "Overweight"); text (x=0.7, y=335, "Obesity")
abline (h=BFP*10, col="red", lwd=2)
```

![plot of chunk unnamed-chunk-6](assets/fig/unnamed-chunk-6.png) 

