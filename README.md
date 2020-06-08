# COVID-19
Computational model and statistics regarding the COVID-19 expansion.
## What is this project?
This project is intended to be a **data source for creating models** that track the **COVID-19 expansion** around the world.
You will be able to use mined resources from several websites that allow us to have data regarding hospital beds, 
immigration flows by nationality, population, demography, affection of risk conditions, real-time evolution of the illness,  
and other relevant statistics for many countries.
## About the project
The code is written in a Python3 Jupyter Notebook [_COVID-19.ipynb_](COVID-19.ipynb) that contains all functionality for data mining
and some predictive models.
Along with the _COVID-19.ipynb_ notebook you will find many directories and CSV files containing data associated with the illness or
other public health information for many countries:

* [_MIG.csv_](MIG.csv): Immigration flows between one country to another by years.
* [_HFA.csv_](HFA.csv): Bed occupancy rate by country and by year.
* [_HOSPITAL_BEDS.csv_](HOSPITAL_BEDS.csv): Hospital beds by country and by year.
* [_population_](population): Directory with demography data (by age and sex) of countries in CSV files
* [_who_cm_](who_cm): Directory with data of affection of risk conditions in countries (PDF files)
* [_data_](data): Directory with Total cases, Deaths and Recovered for every country from 2020-01-21

## Functionality 

### Time evolution of a country

By calling the function ```timeEvolution(<country>)``` you will obtain a Pandas DataFrame with confirmed cases, deaths,  
and recovered for any country.

You can also plot confirmed cases, deaths or recovered by calling the function 

``` graphProgression(<Country_DataFrame>,<parameter>) ```

For example 

``` graphProgression(timeEvolution("Spain"),"Confirmed") ```

![Spain's confirmed cases in time](https://github.com/DanielGuzmanOlivares/COVID-19/blob/master/imgs/Spain_evolution.png?raw=true)

### Real-time evolution

You can call the function ```realTimeEvolution()``` to get a Pandas DataFrame with the current numbers for each country
this is done by mining the web https://www.worldometers.info/coronavirus/ .

### Demography 

The function ```getDemography(<Country>)``` will return a demography table for each country in the form of a pandas DataFrame.
This data can also be plotted by calling the function ```plotDemography(<Country>)```.
For example:
```plotDemography(country_info)```

![United States Demography](https://github.com/DanielGuzmanOlivares/COVID-19/blob/master/imgs/United_States_demography.png?raw=true)

### Immigration flow

It is possible to get the immigration flow by country of every country with a call to the function ```immigrationTo(<Country>)```.
This data are mined from OECD and is the data provided is the latest official data provided to the organization by countries.

### Hospital beds

It might be useful to know how many hospital beds a country has, this can be obtained by calling the ```bedsCountry(<country>)```
function.

### Preexisting conditions

The function getFRCountry(<country>) shows the percentage of fatal cases affected by preexisting medical conditions.
It is also possible to obtain general statistics in fatal cases such as:
* Age -> ```fatalityRate(0) ```
* Sex -> ```fatalityRate(1) ```
* Preexisiting conditions -> ```fatalityRate(2) ```

__Important note:__ due to the difference in naming a country (United States, USA, United States of America ...) in
                    mining resources, we created adaptative dictionaries that translate them to common indexing, if a call
                    to some of the previous functions raises a KeyError, it is probably because of an error in that indexing,
                    we are working on it.
  
### Models

The project provides an example model (based on a sigmoid function) for modeling the growth of total cases in time for any country.
However, we encourage users to create models of their own using the provided tools! 

We provide the following tools for helping in model creation, fitting, and testing:

* ```fit(func,x_data,y_data)``` -> wrapper for the fit_curve function of Scipy library
* ```fromFirstCase(country_df,param)``` -> returns trimmed country data frame from first appearance of parameter (i.e. first case,first death..)
* ```prediction(country,param,days,model,fromNow=False)```-> prediction of <days> days with a model
* ```plotPrediction(x_data,y_data,df)```-> plots prediction and original data
* ```countryR2(country,param,model)``` -> R2 statistic of the prediction model for a country
* ```modelR2(param,model)```-> gives the mean of the R2 statistic applied to each country

### Risk map
You can print a risk choropleth folium map that measures the risk of suffering a health system collapse in a given number of
days based on a logistic growth model and current capacity of the sanitary system of each country.
Risk is represented by a real number in [-inf,0], the lesser the risk the smaller the number.

![Risk map](https://github.com/DanielGuzmanOlivares/COVID-19/blob/master/imgs/Risk_map.png?raw=true)

## Coming soon!

* Economy metrics -> how will the COVID-19 affect your country's economy?
* The risk associated with usual immigration flows from one country to another

## Proposing models and data mining

We believe that there is no such thing as a great project without external collaboration. Do you have any proposals for data mining
or want to provide a new model? Please do not hesitate to contact us (needless to say, all credit will be given to the authors).

Gloria del Valle Cano: glorelvalle@gmail.com

Daniel Guzmán Olivares: dguzolivares@gmail.com

