# Overview of the disease risk model

The model consist of several entangled sections :

<br>
<p align="center">
  <img src="https://github.com/ACCR-VBD/Presentation---Swiss-global-change-day/assets/63344790/5d770b36-a17b-4480-9000-7836701aba05" width=500>
  <br>
  <em>Schematic representation of the different modules involved in the disease risk model</em>
</p>

### Climate input
The climate input is the DAILY-GRID CH2018 Dataset developed by MeteoSwiss. It consist of 68 regional climate models from the EURO-CORDEX ensemble, statisticaly downscaled by quantile mapping to a 2 $\times$ 2 km grid over Switzerland from 1981 to 2099. 31 model correspond to the Representative Concentration Pathway (RCP) 8.5, 25 to RCP4.5, and 12 to RCP2.6. Each of those 68 models provides daily precipitation and maximum, mean and minimum temperature estimates ([CH2018, MeteoSwiss](https://www.nccs.admin.ch/nccs/en/home/the-nccs/priority-themes/ch2018-climate-scenarios.html)). All the spatial data input and output will be aligned with this 2 $\times$ 2 km grid.


### Demographic projection input
The demographic projection inputs consists of two models : 

-   A 1-km downscaling of a global scenario-based spatial projections for each of the five Shared Socio-economic Pathways (SSP) at 10-years interval from 2010 to 2100, obtained by downscaling national-level projections of urban and rural population change corresponding to each scenario to 1/8° using a gravity-type model parameterized to reflect the spatial patterns of change prescribed by each SSP ([Gao et al., 2017](https://opensky.ucar.edu/islandora/object/technotes:553))

-   1-km global spatial projections at 5-year intervals from 2020 to 2100, obtained by building a random forest model based notably on the WorldPop, Global Urban Land Use Change Product and country-level SSPs population projections datasets. ([Wang et al., 2022](https://www.nature.com/articles/s41597-022-01675-x))

### Land-use projection input

### Mosquito population model

The mosquito population model will primarily be based on a compartmental model of the different life stages of relevant mosquito, with parameters defining the dynamics of the compartment. Here is a diagram from ([Metelmann et al., 2019](https://royalsocietypublishing.org/doi/10.1098/rsif.2018.0761)) illustrating this concept :

<p align="center">
  <img src="https://github.com/ACCR-VBD/Presentation---Swiss-global-change-day/assets/63344790/9f1dcf31-c9d3-4a22-9009-d66fc36b8ba1" width=600>
</p>

Each mosquito species has specific climate- and human demography dependent parameters for the 

### Disease risk model

# Current state of the project

