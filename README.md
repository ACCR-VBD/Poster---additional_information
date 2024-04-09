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

Each species has specific climate- and human demography dependent parameters determining the ... life stages. Those parameters are based on either laboratory experiment, such as the temperature-dependant mortality, or expert knowledge, such as the overwintering pattern.

We get ... adult mosquito population over the 2 $\times$ 2 km grid. However, such model mostly uses variable explicitly linked to the life cycle. Some variables such as land-use and elevation, which are known to significantly impact the species distribution, are difficult to implement in this framework.

Neithertheless, the modelisation of the mosquito life stages yields gridded estimates of egg abundance. The most straightforward and scalable method for monitoring mosquito populations is precisely the recording of egg layed in traps. When available, this data allows us to construct a statistical model which would correct for bias in the egg estimates and straightforwardly implement relevant variable. Combining the two methodology allows us to project refined egg abundance estimates over Switzerland, which allows to improve the gridded adult population estimates.

<p align="center">
  <img src="https://github.com/ACCR-VBD/Presentation---Swiss-global-change-day/assets/63344790/26271975-738a-4aae-8754-fbd02487144b" width=400>
  <br>
  <em>Classical ovitrap. This device is designed as a typical breeding site for the studied species. <br> Once installed on the field, the number of mosquito eggs is usually recorded every two weeks</em>
</p>

### Disease risk model

As the mosquito population model yields an estimate of the number of mosquitoes likely to bite humans, and by adding human demographic projection, we are able to model the transmission dynamic of specific mosquito-borne diseases using the framework of epidemiological models, which divides each gridded population into different compartment depending on their infection status.

<p align="center">
  <img src="https://github.com/ACCR-VBD/Presentation---Swiss-global-change-day/assets/63344790/694ca8a9-d849-434e-8cc8-88f29959b9df" width=600>
  <br>
  <em></em>
</p>

A ... of such epidemiological model is the basic reproduction number $R_0$, which corresponds to the average number of secondary infection caused by a single infection in a fully susceptible population

# Current state of the project

