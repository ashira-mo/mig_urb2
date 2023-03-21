# mig_urb2

Replication material for Demographic Research 2023 journal article:
	"Migration’s contribution to the urban transition: Direct census estimates from Africa and Asia"
	Phillipe Bocquier, Ashira Menashe-Oren & Wanli Nie

This file explains the different steps taken, and needed to replicate the results of the paper, including:
	 where to get the data, and what variables are needed 
	 how to generate in and out migration rates,
	 modelling of the migration rates.
The zipped folder includes 19 programs (R files or Stata do files) and an excel file of migration rates.

1. Data
Census samples from IPUMS International are readily available at:
https://international.ipums.org/international/

The downloaded data for each census should include variables of:
	individual identifier
	person weights	
	age
	sex
	education
	place of residence (rural/urban)
	region of current residence
	variables related to migration - either previous place of residence and years in current location, place of residence 1 year ago or 5 years ago
	
Note: the census data is saved as "country_year", where country is based on ISO alpha-2 code. 

2. Generating migration rates

a) To compute in and out migration rates between the rural and urban sectors from the census data, it is first required to clean the raw data.
   In particular, each region within the country needs to be defined as rural/urban according to a 50% threshold. 
	-> The "decision on urban threshold_adjusted wup and weighted" R file documents how the 50% threshold was chosen (see also Appendix A1).
   The R files named "calibrate rates_" go through the censuses and define regions as rural/urban, in some cases relying on external data sources.
   The calibration also ensures age and education variables are coded coherently and consistently, and identifies those we consider migrants.

b) After preparing the data, to extract the migration rates, the Stata files named 1-year/3-year/5-year, in/out, africa/asia are run.
	-> To check if the number of migrations and person years at risk corresponds to the raw data, and that the cleaning did not distort the data,
	 it is possible to use the R programme "check golden rules africa/asia" 
	-> The excel file "Africa Asia migration rates" is the output of these programs - migration rates pre-modelling.

3. Modelling internal migration

The analysis of migration and urbanisation is based on a set of Poisson models, using the computed migration estimates in the census, 
as well as the proportion urban per country-year taken from the World Urbanisation Prospects (WUP) 2018. 
The WUP data is available as excel file ("WUP2018-F02-Proportion_Urban.xls"), at: https://population.un.org/wup/download/
The Stata do file "models" documents the modelling strategy.
