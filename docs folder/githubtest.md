---
output:
  md_document:
    variant: markdown variant
    code_folding: hide
    toc: yes
    toc_depth: 2
    toc_float: yes
  pdf_document:
    toc: yes
    toc_depth: '2'
---

![](images/iceslogo.png)

---

# ICES advice 2018 for hke.27.3a46-8abd

"Hake (*Merluccius merluccius*) in subareas 4, 6, and 7, and in divisions 3.a, 8.a–b, and 8.d, Northern stock
(Greater North Sea, Celtic Seas, and the northern Bay of Biscay)"

<a href="#top">Back to top</a>
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(
	echo = FALSE,
	message = FALSE,
	warning = FALSE
)
```

***

![](images/hake.png) ![](images/map.png)

[Link to latest advice](http://ices.dk/sites/pub/Publication%20Reports/Advice/2017/2017/hke.27.3a46-8abd.pdf)  
[Link to Standard Graphs page](https://standardgraphs.ices.dk/manage/ViewGraphsAndTables.aspx?key=8988)

***

# ICES advice on fishing opportunities
ICES advises that when the MSY approach is applied, catches in 2018 should be no more than **115 335** tonnes.
 <br> 

***

# Stock development over time
The spawning-stock biomass (SSB) has increased significantly since 2006 and is well above historical estimates. Fishing mortality (F) has decreased significantly after 2005, and has been below FMSY since 2012. The recruitment (R) estimate for 2016 is above average
 
 
```{r cars, echo=FALSE, fig.align=, fig.height=5, fig.width=5}
 library(htmlwidgets)
 library(dplyr)
 library(ggplot2)
 library(gridExtra)
 library(dygraphs)
 library(htmltools)
 data <- read.csv("Data/hke/hkedata.csv")
 
 dyBarChart <- function(dygraph) {
  dyPlotter(dygraph = dygraph,
            name = "BarChart",
            path = system.file("examples/plotters/barchart.js",
                               package = "dygraphs"))
}
 
 catches <- data %>% select(Year, catches)
 catches$catches <- catches[, "catches"]/1000
 recruitment<- data %>% select(Year, low_recruitment, recruitment, high_recruitment)
 
 dygraph(catches, main = "Catches") %>% 
   dyRangeSelector()%>%
   dyOptions(colors = RColorBrewer::brewer.pal(3, "Set2"), drawGrid = FALSE,maxNumberWidth = 4)%>%
   dyAxis("y", label = "Catches in 1000 t")%>%
   dyBarChart()
 dygraph(recruitment, main = "Recruitment(age 0)") %>%
   dyRangeSelector()%>%
   # dyOptions(colors = RColorBrewer::brewer.pal(3, "Set2"))%>%
   dyAxis("y", label = "Recruitment in millions")%>%
   dyBarChart()
 

```
 
  
 
```{r, echo = FALSE, fig.height = 5, fig.width = 5, fig.align = "left"}
library(dygraphs)
library(htmlwidgets)
library(dplyr)
library(ggplot2)
library(gridExtra)
library(dygraphs)

dyBarChart <- function(dygraph) {
  dyPlotter(dygraph = dygraph,
            name = "BarChart",
            path = system.file("examples/plotters/barchart.js",
                               package = "dygraphs"))
} 

F <- data %>% select(Year, low_F, F,high_F, FLim, Fpa, FMSY )
 dygraph(F, main = "F") %>% 
  dySeries(c("low_F", "F", "high_F"))%>%
   dyLimit(as.numeric(F[, 5]), color = "red")%>%
   dyRangeSelector()%>%
   dyOptions(colors = RColorBrewer::brewer.pal(3, "Set2"), 
             drawGrid= FALSE,maxNumberWidth = 4)%>%
   dyAxis("y", label = "F(15-80cm)")

SSB <- data %>% select(Year, low_SSB, SSB,high_SSB, Blim, Bpa, MSYBtrigger)
 dygraph(SSB, main = "SSB") %>%
  dySeries(c("low_SSB", "SSB", "high_SSB"))%>%
   dyLimit(as.numeric(F[, 5]), color = "red")%>%
   dyRangeSelector()%>%
   dyOptions(colors = RColorBrewer::brewer.pal(3, "Set2"),
             drawGrid= FALSE,maxNumberWidth = 4)%>%
   dyAxis("y", label = "SSB in 1000 t")

# p<- ggplot(data, aes(x = Year, y= F)) + geom_line(position = "stack")
#  p <- p + theme_bw()
#  c<- ggplotly(p)
#  q <- ggplot(data, aes(x = Year, y= SSB)) + geom_line(position = "stack")
#  q <- q + theme_bw()
#  d<- ggplotly(q)
#  subplot(c,d)

#Need to figure out how to order them, and make them all show up 
 
```

**Figure 1**  Hake in subareas 4, 6, and 7, and in divisions 3.a, 8.a–b, and 8.d, Northern stock. Summary of the stock assessment.Recruitment, F, and SSB plots show 95% confidence intervals (shaded area). Assumed recruitment values are unshaded.
<br>

 ***  

# Stock and explotation status

<br>
**State of the stock and fishery relative to reference points**
![](images/MSY_1.png)

<br> 

***  

# Catch scenarios

<br>
**Table 2** Hake in subareas 4, 6, and 7, and in divisions 3.a, 8.a–b, and 8.d, Northern stock. The basis for the catch scenarios. All weights are in tonnes.
<br>
```{r catchoptionsbasis, echo=FALSE}
library(knitr)
library(readr)
library(kableExtra)
dt <- read.csv("Data/hke/hkecatchoptionsbasis.csv",header = T, row.names = 1)
# dt <- dt [,-1] 
kable(dt, "html")%>%kable_styling(position = "center", full_width = T, font_size = 12)%>%
  row_spec(0, bold = T, color = "black", background = "lightgrey", align = "c")%>%
  column_spec(1, width = "15em")%>%
  column_spec(4, width = "60em")%>%
  column_spec(3, width = "10em")
```

<br>

***

**Table 3** Hake in subareas 4, 6, and 7, and in divisions 3.a, 8.a–b, and 8.d, Northern stock. Annual catch options. All weights are in tonnes

<button class="btn btn-primary" data-toggle="collapse" data-target="#BlockName"> Show/Download Table </button>  
<div id="BlockName" class="collapse"> 
```{r catchoptions, echo=FALSE}
library(knitr)
library(readr)
library(kableExtra)
dt <- read.csv("Data/hke/hkecatchoptions.csv", header = T, row.names = 1)
# dt <- dt [,-1]
dt <- dt[complete.cases(dt),]
 kable(dt, "html") %>% kable_styling(position = "center")%>%
   row_spec(0, bold = T, color = "black", background = "lightgrey")%>%
   column_spec(1, width = "60em")%>%
   group_rows("ICES advice basis",1,1) %>%
   group_rows("Other options",2,9)
```

```{r}
library(magrittr)
 readLines("Data/hke/hkecatchoptions.csv") %>% 
   paste0(collapse="\n") %>% 
   openssl::base64_encode() -> encoded
```

[Download CSV](`r sprintf('data:text/csv;base64,%s', encoded)`)
</div>
<br>



```{r, out.width = "600px"}
knitr::include_graphics("images/hkescenariosplot.png")

```

<br>
```{r echo = FALSE, fig.height = 4, fig.width = 6, fig.align = "left"}
library(ggplot2)
library(plotly)
 catchoptions <- read.csv("Data/hke/hkescenariosplot.csv")
 labels <- catchoptions$Basis
 labels <- as.character(labels)
 mypalette<-ggthemes::tableau_color_pal('tableau20')
 
  p1 <- plot_ly(catchoptions, x = ~F, y = ~SSB, type = 'scatter', showlegend = T) %>% 
    
    # , color = ~Basis, colors=mypalette, height=375
    layout(hovermode="TRUE", showlegend = TRUE,
           # xaxis = list(title = 'F', range= c(min(ssb3$Year), max(ssb3$Year)+1)),
           # yaxis = list (title = 'SSB', range = c(0, max(ssb3$value, na.rm = T)*1.05)),
           shapes = list(
             list(type = "rect", fillcolor = "green", opacity = 0.2, 
                  line = list(color = "green", opacity=0.2), 
                  x0 = -0.3, x1 = 0.62, xref = "x",
                  y0 = 0, y1 = 450000, yref = "y"), 
             #      xref = "Year", y0 = Bpa, y1 = max(ssb$value, na.rm=TRUE)*1.05, yref = "value"),
             list(type = "rect", fillcolor = "orange", opacity = 0.2, 
                  line = list(color = "orange", opacity=0.2), 
                  x0 = 0.62, x1 = 0.87, y0 = 0, y1 = 450000), 
                  # xref = "Year", y0 = Blim, y1 = Bpa, yref = "value"),
             list(type = "rect", fillcolor = "red", opacity = 0.2, 
                  line = list(color = "red", opacity=0.2), 
                  x0 = 0.87, x1 = 3, y0 = 0, y1 = 450000))) 
                  # xref = "Year", y0 = 0, y1 = Blim, yref = "value")))
  p1$elementId <- NULL
  p1
 
 
 
 
 
 p1 <- ggplot(catchoptions, aes(F)) + theme_bw() +
    # geom_rect(xmin = -Inf, ymin = -Inf, xmax = 0.62, ymax = Inf,
    #           fill = "lightgreen", alpha=0.50)+theme_bw()+
    # # geom_rect(xmin = 0.280, ymin = -Inf, xmax = 0.282, ymax = Inf,
    # #           fill = "gold", alpha=0.50)+theme_bw()+
    # geom_rect(xmin = 0.62, ymin = -Inf, xmax = 0.87, ymax = Inf,
    #           fill = "coral")+theme_bw()+
    # geom_rect(xmin = 0.87, ymin = -Inf, xmax = Inf, ymax = Inf,
    #           fill = "brown1")+theme_bw()+
    geom_hline(yintercept=45000, linetype="dashed", color = "yellowgreen")+
    geom_hline(yintercept=32000, linetype="dashed", color = "yellow4")+
    geom_vline(xintercept = 0.28,linetype = "dotted",
               color = "violet", size = 0.5)+
    geom_vline(xintercept = 0.62, linetype="dotted",
               color = "violetred", size=0.5)+
    geom_vline(xintercept = 0.87, linetype="dotted",
               color = "violetred1", size=0.5)+
    # geom_col(aes(y = Catch), width = 0.15)+
    geom_point(aes(y = Catch),size = 2, colour= "orangered") +
    geom_line(aes(y = Catch),size = 0.5, colour= "orangered")+
    geom_point(aes(y=SSB), size = 2, colour= "lightskyblue")+
    geom_line(aes(y = SSB),size = 0.5, colour= "lightskyblue")+
    scale_y_continuous("tonnes",sec.axis = sec_axis(~., name = "SSB"))+
    # scale_x_continuous(breaks = catchoptions$F)+
    xlab("Fish mortality")+
    ylab("Catches and SSB in tonnes")
 
  p2 <- p1 + theme(axis.text.x = element_text(face="bold", color="Black",
                             size=10, angle=45))+
    theme(legend.text = element_text(colour="blue", size = 16, face = "bold"))
  # p3<- p2+ guide_colorbar(title = "Spawning Stock Biomass", label= TRUE,barheight = )
 # p3<- p2 + geom_hline(yintercept=45000, linetype="dashed", color = "red")+
 #   geom_hline(yintercept=32000, linetype="dashed", color = "black")+
 #   geom_vline(xintercept = 0.28,
 #                 color = "yellow", size=3)+
 #   geom_vline(xintercept = 0.62, linetype="dotted",
 #                   color = "blue", size=0.5)+
 #   geom_vline(xintercept = 0.87, linetype="dotted",
 #                 color = "blue", size=0.5)



 ggplotly(p2, width = 600, height = 300)
#little turn to avoid double values adding in the bars
catchoptions <- catchoptions[!duplicated(catchoptions[,c('F')]),]
labels <- catchoptions$Basis
labels <- as.character(labels)

 p1 <- ggplot(catchoptions, aes(F))+
    # geom_rect(xmin = -Inf, ymin = -Inf, xmax = 0.62, ymax = Inf,
    #           fill = "lightgreen", alpha=0.50)+theme_bw()+
    # # geom_rect(xmin = 0.280, ymin = -Inf, xmax = 0.282, ymax = Inf,
    # #           fill = "gold", alpha=0.50)+theme_bw()+
    # geom_rect(xmin = 0.62, ymin = -Inf, xmax = 0.87, ymax = Inf,
    #           fill = "coral")+theme_bw()+
    # geom_rect(xmin = 0.87, ymin = -Inf, xmax = Inf, ymax = Inf,
    #           fill = "brown1")+theme_bw()+
    geom_hline(yintercept=45000, linetype="dashed", color = "red")+
    geom_hline(yintercept=32000, linetype="dashed", color = "black")+
    geom_vline(xintercept = 0.28,
               color = "yellow", size=3)+
    geom_vline(xintercept = 0.62, linetype="dotted",
               color = "blue", size=0.5)+
    geom_vline(xintercept = 0.87, linetype="dotted",
               color = "blue", size=0.5)+
   #this is wrong, it is adding twice the same value
    geom_col(aes(y = Catch), width = 0.15)+
    # geom_point(aes(y = Catch),size = 2, colour= "Red") +
    # geom_line(aes(y = Catch),size = 0.5, colour= "Red")+
    geom_point(aes(y=SSB), size = 2, colour= "Blue")+
    geom_line(aes(y = SSB),size = 0.5, colour= "Blue")+
    scale_y_continuous("tonnes",sec.axis = sec_axis(~., name = "SSB"))+
    scale_x_continuous(breaks = catchoptions$F, labels = labels)+
    xlab("Catch scenarios for 2018")+
    ylab("tonnes")
  p2 <- p1 + theme(axis.text.x = element_text(face="bold", color="Black",
                             size=10, angle=45))+
    theme(legend.text = element_text(colour="blue", size = 16, face = "bold"))
  # p3<- p2+ guide_colorbar(title = "Spawning Stock Biomass", label= TRUE,barheight = )
 # p3<- p2 + geom_hline(yintercept=45000, linetype="dashed", color = "red")+
 #   geom_hline(yintercept=32000, linetype="dashed", color = "black")+
 #   geom_vline(xintercept = 0.28,
 #                 color = "yellow", size=3)+
 #   geom_vline(xintercept = 0.62, linetype="dotted",
 #                   color = "blue", size=0.5)+
 #   geom_vline(xintercept = 0.87, linetype="dotted",
 #                 color = "blue", size=0.5)



 ggplotly(p2, width = 600, height = 300)
```

<br>

# Basis of the advice  
***
<br>
**Table 4** Hake in subareas 4, 6, and 7, and in divisions 3.a, 8.a–b, and 8.d, Northern stock. The basis of the advice.
```{r advicebasis, echo=FALSE}
library(knitr)
library(readr)
library(kableExtra)
dt <- read.csv("Data/hke/hkeadvicebasis.csv", header = FALSE)
dt <- dt [,-1] 
kable(dt, "html")%>%kable_styling(position = "center")%>%
  column_spec(1, bold = T, color = "black", background = "lightgrey")

```

<br>

#Quality of the assessment  
***
<br>
The uncertainty in the assessment is relatively high, with large changes in biomass estimates in consecutive years. The model confidence intervals are an underestimate of uncertainty because they are narrower than interannual changes in estimates in consecutive years.
There is a lack of tuning data for the earlier years of the assessment, for some areas outside of subareas 7 and 8, and for the larger individuals in the population. Given the expansion of the stock into northern areas (ICES, 2017b), there is a potential that not all catches are reported for this stock. Biological sampling from these areas is also limited.
The data compilation of this stock is very complicated because it is exploited by several countries and the assessment model configuration is complex. In turn, the assessment model is very sensitive to the data and the settings used. Hence, it is extremely important for the quality of the assessment to have the complete data for all the countries on time and in the right format.

# Reference Points  
***
<br>
Herring in Subarea 4 and divisions 3.a and 7.d, autumn spawners. Reference points, values, and their technical basis.
```{r referencepoints, echo=FALSE}
library(knitr)
library(readr)
library(kableExtra)
dt <- read.csv("Data/hke/hkereferencepoints.csv")
dt <- dt [,-1] 
kable(dt, "html")%>%kable_styling(position = "center")%>%
  row_spec(0, bold = T, color = "black", background = "lightgrey")

```
<br>

# Basis of the assessment  
***
<br>
Herring in Subarea 4 and divisions 3.a and 7.d, autumn spawners. Basis of the assessment and advice
```{r advicebla, echo=FALSE}
library(knitr)
library(readr)
library(kableExtra)
dt <- read.csv("Data/hke/hkeassessmentbasis.csv")
dt <- dt [,-1] 
kable(dt, "html")%>%kable_styling(position = "center")%>%
  row_spec(0, bold = T, color = "black", background = "lightgrey")

```

# Historical trends

```{r, echo=FALSE}
library(googleVis)
# kobe <- read_csv("kobe_data_2.csv")
# herring <- kobe %>% filter(StockCode =="her.27.3a47d")
# vis<- gvisMotionChart(herring, idvar = "StockCode", timevar = "Year", xvar = "SSB.MSYBtrigger",
#   yvar = "F.Fmsy", colorvar = "EcoRegion", sizevar = "", date.format = "%Y/%m/%d",
#   options = list())
# vis
```

