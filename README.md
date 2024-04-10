# Overview of the disease risk model

The overall objective of our research project is to develop a model that utilizes RCP-SSP scenarios as input to generate a probabilistic risk assessment of Dengue, Zika, and Chikungunya outbreaks driven by Aedes albopictus and Aedes aegypti. We aim to provide up to 2060 a daily estimate of outbreak potential, mapped on a 4 km² grid across     Switzerland.

We plan to implement a framework consisting of several entangled sections :

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

### Mosquito population model

The mosquito population model will primarily be based on a compartmental model of the different life stages of relevant mosquito, with parameters defining the dynamics of the compartment. Here is a diagram from ([Metelmann et al., 2019](https://royalsocietypublishing.org/doi/10.1098/rsif.2018.0761)) illustrating this concept for Aedes albopictus :

<p align="center">
  <img src="https://github.com/ACCR-VBD/Presentation---Swiss-global-change-day/assets/63344790/9f1dcf31-c9d3-4a22-9009-d66fc36b8ba1" width=800>
</p>

Each mosquito species has specific climate- and human demography dependent parameters determining the dynamics of the mosquito life cycle. Those parameters are based on either laboratory experiment, such as the temperature-dependant mortality, or expert knowledge, such as the overwintering pattern.

Using this approach, we are able to estimate the abundance of female adult mosquito in each cell of the 2 $\times$ 2 km grid. However, such model can only use variables explicitly linked to the mosquito life cycle. Some variables such as land-use patterns and elevation, which are known to significantly impact the species distribution, are difficult to implement in this framework.

Neithertheless, the modelisation of the mosquito life stages also yields estimates of egg abundance. The most common and scalable method for monitoring mosquito populations is precisely the recording of the number of eggs layed in traps. When available, this data allows to construct a statistical model which would correct for bias in the egg estimates and straightforwardly implement relevant variable. Combining the two methodology allows us to project refined egg abundance estimates over Switzerland, which therefore improves the gridded adult population estimates.

<p align="center">
  <img src="https://github.com/ACCR-VBD/Presentation---Swiss-global-change-day/assets/63344790/26271975-738a-4aae-8754-fbd02487144b" width=400>
  <br>
  <em>Classical ovitrap. This device is designed as a typical breeding site for the studied species. <br> Once installed on the field, the number of mosquito eggs is usually recorded every two weeks.</em>
</p>

### Disease risk model

As the mosquito population model yields an estimate of the number of mosquitoes likely to bite humans, and by adding human demographic projection, we are able to model the transmission dynamic of specific mosquito-borne diseases using the framework of epidemiological models, which divides each gridded population into compartments corresponding to different epidemiological status.

<p align="center">
  <img src="https://github.com/ACCR-VBD/Presentation---Swiss-global-change-day/assets/63344790/694ca8a9-d849-434e-8cc8-88f29959b9df" width=600>
  <br>
  <em>Ross-macdonald transmission model of mosquito-borne diseases</em>
</p>

A crucial metric based on such epidemiological model is the basic reproduction number $R_0$, which corresponds to the average number of secondary infection caused by a single infection event in a fully susceptible population. This value has interesting thresholding properties:

- If \($R_0$ > 1\), each infected individual, on average, infects more than one other person, leading to the potential for an epidemic.
- If \($R_0$ < 1\), the disease will eventually die out as each infected individual, on average, infects less than one other person.

This metric is computed through an equation based on several parameters of the epidemiological compartmental model, as in the following formula from the Ross-macdonald model :

<p align="center">
  <img src="https://latex.codecogs.com/svg.latex?\Large&space;R_0=\frac{M}{N}\times\frac{a^2bc}{\mu{r}}e^{-\mu\times\text{EIP}}">
</p>

Where:
- \(M\) is the number of female adult mosquitoes,
- \(N\) is the number of human,
- \(a\) is the daily biting rate per mosquito,
- \(b\) is the probability of disease transmission from an infectious mosquito to a susceptible human per bite,
- \(c\) is the probability of disease transmission from an infectious human to a susceptible mosquito per bite,
- \($\mu$\) is the mortality rate of mosquitoes,
- \(r\) is the recovery rate of humans.
- \(EIP\) is the incubation period during which an infected mosquito becomes infectious.

Many parameters of this equation are sensitive to temperature. To account for this effect, we can estimate the temperature dependence by fitting functional forms to reported controlled laboratory experiments measuring the parameter for different temperatures :

<p align="center">
  <img src="https://github.com/ACCR-VBD/Presentation---Swiss-global-change-day/assets/63344790/465c9e79-aa53-4a29-ad57-fade566d1770", width =500>
</p>

Using a bayesian framework allows to straightforwardly propagate the uncertainity of the parameters thermal dependency to the $R_0$ estimate, yielding a function relating the temperature with a confidence interval of $R_0$ :

<p align="center">
  <img src="https://github.com/ACCR-VBD/Presentation---Swiss-global-change-day/assets/63344790/99d9994d-4635-442a-96ef-bd1288152fae", width =400>
  <br> 
  <em>Temperature dependance of the basic reproduction number for <br> Aedes Aegypti mosquitoes transmitting dengue, estimated with arbitrary population values</em>
</p>

Finally, by combining the mean temperature, the estimated number of female mosquitoes and the estimated size of human population, we can use this framework to model a probabilistic risk of mosquito-borne disease outbreaks in each cell of the 2 $\times$ 2 km grid and for each pair of mosquito species and disease studied.
