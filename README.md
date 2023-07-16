---
author: Justice
date: "`r Sys.Date()`"
output: html_document
title: Data Visualization and storytelling
---
[Data analyst audio.webm](https://github.com/Justice-source/Data-visualization-and-story-telling/assets/95739749/495f1f1f-b1a7-471a-b621-ffc958cfeab9)

## Programs used for data visualisation of the Pokemon datasets

I made used of R ,R is a programming language for statistical computing
and graphics supported by the R Core Team and the R Foundation for
Statistical Computing. I made use of R studio for coding for the
hakathon.
I used R studio computer program.
RStudio is an integrated development environment for R.

I used Github for version control.

OBS studio for screen recording and audio recording.

The snipping tool app on Windows 10 for taking screenshots and images.

#### My thought process when working on the pokemon data set.

When analyzing Pokemon data sets, here are the steps I  followed:

1. Understand the data set: I Familiarized myself with the structure and contents of the  Pokemon data set. Checked all the variables and their descriptions to know what information is provided.

2. Data Pre-processing: I cleaned the data set, establishing a new data sets I will be working on, outliers, or any inconsistencies in the data.I Cleaned up the data set to ensure accurate analysis.

3. Exploratory Data Analysis (EDA): I Performed initial exploratory analysis using the skimr package in R to gain insights into the data set. Visualized distributions, correlations, and summary statistics of different attributes present in the  Pokemon data set.  I did create a correlation matrix to Identify interesting trends within the data.

4. Feature engineering: I analysed the strongest Pokemon based on Speed , the Pokemon with the highest attack and defense stats and more.

5. Statistically analyze attributes: I Utilized statistical techniques to understand relationships between attributes. Compute correlation coefficients, perform hypothesis testing, or use scatter plots and correction matrices and data tables to analyze factors that influence certain characteristics, like attack, Speed or defense.

6. Data Visualization:  I Created visualizations such as scatter plots, tables and excel column tables to represent different aspects of the  Pokemon data set. This helps in better understanding and communicating the patterns and relationships within the data.




## I recommend running the codes in the  R markdown (rmd) file in my github repository, there are grouped into  code chunks.

## Libraries used for data visualisation of the Pokemon datasets

library(tidyverse)

library(ggplot2)

library(ggpubr)

library(L1pack)

library(yardstick)

library(dplyr)

library(GGally)

library(DT)

library(waffle)

library(extrafont)

library(showtext)

library(hrbrthemes)

library(echarts4r)

library(echarts4r.assets)

library(knitr)

library(skimr)

library(ggthemes)

library(Sleuth3)

library(scales)

library(devtools) find_rtools()

The package echarts4r.assets is not available on CRAN so you need to
install it from github account by running this command
devtools::install_github("JohnCoene/echarts4r.assets")

# install.packages("devtools")

devtools::install_github("r-lib/conflicted")

Install the packages used for Infographic Charts You can install these
packages by running command install.packages(). The package
echarts4r.assets is not available on CRAN so you need to install it from
github account by running this command
devtools::install_github("JohnCoene/echarts4r.assets")

    waffle
    extrafont
    showtext
    tidyverse
    hrbrthemes
    echarts4r
    echarts4r.assets

## I will be utilizing code chunks.

`{r setup, include=FALSE} knitr::opts_chunk$set(echo = TRUE)`

## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax
for authoring HTML, PDF, and MS Word documents. For more details on
using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document. You can embed an R code chunk like this:

## Including Plots

Sure! To create an Data visualization in R Markdown using a provided
Pokemon CSV file, you can follow these steps:

Step 1: Install Required Packages Install the necessary packages for
data manipulation and visualization. You can use the `tidyverse` package
for this:

``` {r}
install.packages("tidyverse")
```

Step 2: Load the Required Packages Load the `tidyverse` package to
access its functions:

``` {r}
library(tidyverse)
```

Step 3: Read the CSV File Read the CSV file into a data frame using the
`read_csv()` function:

``` {r}
data <- read_csv("pokemon.csv")


# Load data
filter <- c("Grass", "Fire", "Water", "Psychic", "Normal", "Dragon", "Flying", "Dark", "Rock", 
            "Steel", "Ice", "Poison", "Bug", "Electric", "Ground", "Ghost", "Fairy", "Fighting")
df <- read_csv(file.path(dirs$root, dirs$data, csvfile))

#show_col_types = FALSE
```

## skimr

skimr is designed to provide summary statistics about variables in data
frames, tibbles, data tables and vectors. It is opinionated in its
defaults, but easy to modify. In base R, the most similar functions are
summary() for vectors and data frames and fivenum() for numeric vectors.

By design, the main focus of skimr is on data frames; it is intended to
fit well within a data pipeline and relies extensively on tidyverse
vocabulary, which focuses on data frames.

It is very good in summarizing a data set

``` {r}
# Type in your code after this line!
library(skimr)
skim(df)
```

Step 4: Explore the Data Inspect the data to understand its structure
and variables using functions like `head()`, `str()`, or `summary()`:

``` {r}
head(data)
str(data)
summary(data)
```

I will make sure to customize the plots, labels, and titles according to
my dataset and analysis needs.

`{r pressure, echo=FALSE, fig.cap="A caption", out.width = '100%'} knitr::include_graphics("image1.png")`

## Data Pre-processing

Data pre-processing is an important and crucial step in the data
visualization and storytelling process. It refers to the cleaning,
transforming, and integrating of data in order to make it ready for
analysis. The goal of data pre-processing is to improve the quality of
the data and to make it more suitable for the specific data
visualization task.

I am going load the needed packages for this tasks in Rstudio and
proceed.

The original Pokemon data set included 1194 observations with 13
variables including Names, Type1, Type2, Hp, Total, Attack, Defense,
Speed,Sp. Atk and Sp. Def. \[1\]. The data set included a lot of
qualitative data that would not be necessary for this EDA(Exploratory
Data Analysis) so some of the variables will later be removed to enhance
better Data visualization.

``` {r}
# Load packages
library(tidyverse)
library(ggplot2)
library(ggpubr)
library(L1pack)
library(yardstick)
library(dplyr)
library(GGally)
library(DT)
```

``` {r}
# Load Data

data <- read_csv("pokemon.csv")

df <- read_csv(file.path(dirs$root, dirs$data, csvfile))

new_data <- subset(data)

# Make a dataset with our data statistics for each Pokemon
pokemon_data_stats <- new_data[c("Id", "Names", "Type1", "Type2", "HP", "Attack", "Defense", "Sp. Atk", "Sp. Def", "Speed", "Total")]

new_names1 <- c('ID', 'Name', 'type1', 'type2', 'hp', 'attack', 'defense', 'Special Atk', 'Special Def', 'speed', 'Total')
names(pokemon_data_stats) <- new_names1

# Make a dataset with all our relevant numerical data variables
pokemon_datanum_stats <- new_data[c("Id", "HP", "Attack", "Defense", "Sp. Atk", "Sp. Def", "Speed", "Total")]

new_names3 <- c('ID', 'hp', 'attack', 'defense', 'Special Atk', 'Special Def', 'speed', 'Total')

names(pokemon_datanum_stats) <- new_names3
pokemon_datanum_stats[] <- lapply(pokemon_datanum_stats, function(x) 
as.numeric(as.character(x)))
pokemon_datanum_stats <- pokemon_datanum_stats %>% na.omit()
```

`{r pressure, echo=FALSE, fig.cap="A caption", out.width = '100%'} knitr::include_graphics("image.jpg")`

## Data Visualisation

Data Visualization

Now let's look at our pokemon data using EDA (Exploratory Data
Analysis). This is a crucial step in data analysis because learning more
about the data before diving too deep into any topic might help you
discover information that changes how you want to proceed.

I will be working with Box plots, In descriptive statistics, a box plot
is a method for graphically demonstrating the locality, spread and
skewness groups of numerical data through their quartiles.

## Boxplot

Box plots are a great way to look at one variable of a data set because
it gives you a quick way to see its mean, minimum, maximum, and
upper/lower quartiles. I created 9 box plots side by side to examine one
variable (attack or defense) across another variable (Speed).

``` {r}
# Generate Attack Box Plot
attack_box_plot <- ggplot(aes(group=Speed,x= Speed, y=Attack, color=Speed),data=data) + geom_boxplot() + labs(x= "Speed (1-9)", y="Attack", title = "Attack Stats by Speed")

# Generate Defense Box Plot
defense_box_plot <- ggplot(aes(group=Speed,x= Speed, y=Defense, color=Speed),data=data) + geom_boxplot() + labs(x= "Speed (1-9)", y="Defense", title = "Defense Stats by Speed")

# Arrange Box Plots Side-by-Side
ggarrange(attack_box_plot, defense_box_plot, ncol = 2)
```

## 

It seems like the general mix of Pokemon in each speed column(attack and
defense) is relative. In the Box plot analyzing attack against speed,
Most Pokemons seem to have a higher attack level when utilizing their
attacks with increased speed. Whereas In the Box plot analyzing defense
against speed, Most Pokemons seem to have a higher defense level when
utilizing their defenses with reduced speed. Although defense potential
can differ depending on the pokemon and its type, most tend to have a
higher value for defense with speeds not greater than 100.

Next, I used box plots again to examine how Attack and Defense variables
changed across Type1(Primary) types.

``` {r}
# Box plot of Attack Stats by Primary Type
ggplot(data=pokemon_data_stats, mapping=aes( x=attack, color=type1))+geom_boxplot()+coord_flip()+labs(title="Boxplots of Attack Statistics by Primary Type1")

# Box plot of Defense Stats by Primary Type
ggplot(data=pokemon_data_stats, mapping=aes( x=defense, color=type1))+geom_boxplot()+coord_flip()+labs(title="Boxplots of Defense Statistics by Type1")
```

In our box plots showing Attack and Defense stats by Type1 statistics,
we can see that Rock,bug and Steel types have the highest defense
usually while Electric and Normal have the lowest defenses.

Fire, Dragon and Ground types generally have the highest attack, while
Fairy and Psychic types have lower defenses. This may be because Fairy
and Psychic types usually have high Special Defense instead.

## Scatter plot

Scatter plots are the graphs that present the relationship between two
variables in a data-set. It represents data points on a two-dimensional
plane or on a Cartesian system. The independent variable or attribute is
plotted on the X-axis, while the dependent variable is plotted on the
Y-axis.

Next, a scatter plot matrix can show regression lines for how each of
the base stats relate to each other. This provides a more in depth p
view of the correlations between the data stats.

``` {r}
# Make a Scatter plot Matrix with Regression Lines for Data Stats
pairs(pokemon_data_stats[,5:11], panel=panel.smooth, col='light green',main="Scatterplot Matrix with Regression Lines for Data Stats")
```

I don't recommend the scatter plot matrix, once you know the focus of
your data analysis because it is hard to get any conclusive data
visualization when looking at so many variables simultaneously.

Our scatter plot matrix shows us that data stats for Pokemon generally
have a slight positive relationship with each other. This suggests that
Pokemon with a high data stat in one area usually has high data stats in
other areas. This kind of scatter plot matrix can be useful for getting
a very clear view of our data as a whole, but it doesn't offer clear
evidence in our Pokemon data set.

Then, I created another dashboard with a series of scatter plots,
density graphs, and a correlation matrix showing the differences between
the Total stats and the other Pokemon numerical stats such as hp,
attack, defense, Special Atk, Special Def and speed.

Total stats of a pokemon seems to correlate alot with other pokemon
numerical stats as our results were TRUE.

``` {r}
pokemon_datanum_logical_Total <- pokemon_datanum_stats
pokemon_datanum_logical_Total$Total <- as.logical(pokemon_datanum_logical_Total$Total)
ggpairs(pokemon_datanum_logical_Total, columns = 2:8, ggplot2::aes(color=Total), title = "Scatterplot, Density Graph, and Correlation Coefficient Matrix
        colored by Total Status")
```

The density graphs indicate that the Total stats of a Pokemon is more as
a combination of attack, Special Atk, and defense when observed. The
correlation coefficient matrix shows that most of the stats are highly
correlated with each other.

## I visualized Attack vs. Defense in our Pokemon data using a scatter plot.

``` {r}
library(tidyverse)
library(ggplot2)
library(Sleuth3)
library(scales)

pokemon_datanum_logical_Total <- new_data
pokemon_datanum_logical_Total$Total <- as.logical(pokemon_datanum_logical_Total$Total)
pokemon_datanum_logical_Total <- pokemon_datanum_logical_Total %>% 

  arrange(-Attack, -Defense) %>%

 ggplot2::aes(x = Attack, y = Defense,  color=data)

data = new_data

#display the names of all objects in environment
ls()

#check if data exists
exists('data')

 #slice(1:100)  %>%


library(ggthemes)
new_data %>%
group_by(Attack,Defense) %>% #calculate the mean Score of Attack and Defense 
summarize(average_Score = mean(HP, na.rm = TRUE), n= n()) 

ggplot(data= new_data, aes(x = Attack, y = Defense)) +
  geom_point(color = "grey", size = 3, color= data, alpha = 0.6) +

  labs(title = "My Scatter Plot", x = "X-axis Label", y = "Y-axis Label") +

  geom_text(aes(x = Attack, 
                y = Defense, label = Names), 
            check_overlap = TRUE, 
            col = "grey50",
            hjust = 0, 
            alpha = 0.8) +
  
  
  ggtitle(label='Pokemon attack and defense Scatterplot') +
  scale_size_continuous(guide="none")+
  scale_y_log10("defense (%) (log scale)")+
  scale_x_log10("attack (%) (log scale)")+
  scale_color_brewer(palette = 5, type = "qual") +
  theme_classic()
  scale_x_continuous( trans= 'log10')




```

Our Pokemon attack and defense scatter plot demonstrates that the two
variables usually go together and Pokemons high in defense are also high
in attack on an average.

## Notable outliers are shuckle and magikarp.

`{r pressure, echo=FALSE, fig.cap="A caption", out.width = '100%'} knitr::include_graphics("shuckle.jpg") knitr::include_graphics("magikarp.jpg")`
`{r pressure, echo=FALSE, fig.cap="A caption", out.width = '100%'} knitr::include_graphics("shuckle.jpg")`

Shuckle is a Bug/Rock-type Pokemon introduced in Generation II. It is
known for having the highest Defense and Special Defense stats of any
Pokemon. Shuckle is low in attack stats but exceeds greatly in its
defense stats.

`{r pressure, echo=FALSE, fig.cap="A caption", out.width = '100%'} knitr::include_graphics("magikarp.jpg")`

Magikarp is a Water type Pokémon introduced in Generation 1. Magikarp is
known for being one of the weakest Pokemon, with poor stats. it has a
high defense stat but low attack stat.

## The highest outlier in both attack and defense stats is Steelix Mega Steelix

`{r pressure, echo=FALSE, fig.cap="A caption", out.width = '100%'} knitr::include_graphics("steelix.jpg")`

Steelix is a Steel/Ground type Pokémon introduced in Generation 2.
Steelix has very high attack and defense stats as observed in the
scatter plot.

## Other outliers include Blissey and Chansey

`{r pressure, echo=FALSE, fig.cap="A caption", out.width = '100%'} knitr::include_graphics("blissey.jpg") knitr::include_graphics("chansey.jpg")`
Blissey and chansey.

\`\`\`{r pressure, echo=FALSE, fig.cap="A caption", out.width = '100%'}
knitr::include_graphics("blissey.jpg")


    Blissey is a Normal type Pokemon introduced in Generation 2.
    Blissey is characterized as having very low attack and defense stats.



    ```{r pressure, echo=FALSE, fig.cap="A caption", out.width = '100%'}
    knitr::include_graphics("chansey.jpg")

Chansey is a Normal type Pokemon introduced in Generation 1. Chansey is
characterized as having very low attack and defense stats.

## Doing a preliminary EDA of the data allows you as a data analyst to approach your data more effectively.

Do Pokemon become stronger or weaker when they have higher speeds or
not?

If we only look at Attack and Defense, it seems from the box plots of
Attack and Defense by Speed We found out that Speed plays a major role
in attack and defense. Attack seems more dependent on Speed than defense
seems to be.

``` {r}
library(tidyverse)
library(ggthemes)
new_data %>%
  
group_by(Attack,Defense) %>% #calculate the mean Score of Attack and Defense 
summarize(average_Score = mean(HP, na.rm = TRUE), n= n()) 

new_data %>%
group_by(Attack,Defense,Total) %>% #calculate the Total mean Score of Attack, Defense and Total
summarize(total_mean_Score = mean(HP, na.rm = TRUE), n= n()) 


```

I think we can conclude that Pokemon did become stronger by attacks
based on higher speeds and some did become weak by attacks due to
reduced speeds. Now by defense based on higher speeds there were
variability but most of the pokemon did exhibit higher defense stats
with relation to speed and exhibited variable results with reduced
speeds.

## What types of Pokemon generally have higher attack or defense stats?

We can answer this question similarly, by grouping our dataset by Type1
and calculating the mean Attack and Defense stats of each type.

``` {r}
  data %>%
  group_by(Type1) %>%
  summarise_at(c("Attack", "Defense"), mean, na.rm = TRUE) %>%
  arrange(desc(Attack)) %>% 
  
  
```

Fighting types exhibiting the higher attack and defense stats according
to our data visualization. We can see that Fighting, Dragon and Ground
generally have the highest Attack and Defense stats, while Bug, Ghost,
and Fairy types have the lowest.

## What types of Pokemon generally have SP. Atk or SP. Def stats?

Something to keep in mind is that there are also Special Attack and
Special Defense types however, and these stats are particularly high in
Psychic and Dragon types which explains discrepancy in data
visualisation with attack and defense stats when cross analysed with
special attack and special defense stats.

``` {r}
data %>%
  group_by(Type1) %>%
  summarise_at(c("Sp. Atk", "Sp. Def"), mean, na.rm = TRUE) %>%
  arrange(desc(`Sp. Atk`)) %>% 
  
```

Pokemon types with special attack and defense abilities goes to psychic
types. Psychic, Dragon and Electric types are the highest in terms of
special attacks and defense stats. Where as Pokemon with the lowest
stats for special attack and special defense were Fighting, Bug and
Ground.

## Does Speed have any correlation with hp, attack, or defense stats?

We can check this by constructing a correlation matrix that shows how
much Speed is correlated with HP, Attack, and Defense in the dataset.

``` {r}
library(tidyverse)
library(ggthemes)
 
# compute the correlation of each feature with Speed
cor_df <- pokemon_datanum_stats
  pokemon_datanum_stats %>%    select_if(is.numeric) %>%
  cor() %>%
  as.data.frame() %>%
  select(speed_Corr = speed) %>%
  arrange(desc(abs(speed_Corr))) %>%
  rownames_to_column(var = "variable")
cor_df
```

We can see that while speed does have some correlation with Total. I
believe that 0.7 as a good threshold for what is a strong enough
correlation to be significant and legitimate to consider correlation.
Then according to the visualized data, I would not say that speed is
really correlated with any numeric variables in the Pokemon data set
except special attack attack and total.

## Summary

This AngelHack Monthly Code Challenge was interesting to me and was a
great opportunity to apply my coding skill on R as well as
EDA(Exploratory Data Analysis) techniques to Pokemon data. I am
currently a student in a computer Engineering and working towards
getting a Data Analyst certification.

I used EDA and correlation matrix, scatter plots and box plots
techniques in this project, in addition to packages like yardstick,
ggplot2,ggpubr ,tidyverse, L1pack, DT, dplyr and GGally used for data
visualizations.

To an avid Pokemon player, these visualizations could be used when
building a team to see which types of Pokemon have what attack and
defense profile, or deciding which game to play if you want generally
stronger or weaker Pokemon. I hope this data visualization were helpful
in helping you better understand the patterns and trends within the data
in R. My primary goal of this was to present the pokemon data sets in an
easily understandable and visually appealing way.

## Data set used:

https://www.kaggle.com/datasets/rohanpatil63/pokemon-dataset
"# Data-visualization-and-story-telling" 
