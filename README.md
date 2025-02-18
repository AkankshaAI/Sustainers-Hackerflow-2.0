#                                                                            AIS- HALT
<p align="centre"><img src="https://github.com/AkankshaAI/Sustainers-Hackerflow-2.0/blob/main/images/logosus.jpg" width="300" > </p>
In this project we will collaborate with [Global Fishing Watch](http://www.globalfishingwatch.org/) to detect fishing activity in the ocean using data from satellite Automatic Identification System [AIS](https://en.wikipedia.org/wiki/Automatic_identification_system) collected from different vessels around the world. The AIS data contains the latitude, longitude, speed and course of the vessels at different times.  
The interactive tool should be able to categorize the AIS inactivity episodes for a single vessel or multiple vessels in a selected region. Further, the data may be classified based on the ship behavior prior to the inactivity, as well as based on various inactivity parameters such as location, time and duration of inactivity.


## Problem Statement

AIS is a useful system that helps to avoid ship collisions and allows managers of fleet management, especially for emergencies e.g. adverse sea conditions. Vessels keep the AIS beacons on in order to stay safe. However, sometimes the vessels do not transmit. The reasons for this may be unknown. As much as the AIS activity data are important, the inactivity data can also be put to use to understand the possible reasons behind such behavior and if needed, respond in the appropriate manner. The interactive tool should be able to categorize the AIS inactivity episodes for a single vessel or multiple vessels in a selected region. Further, the data may be classified based on the ship behavior prior to the inactivity, as well as based on various inactivity parameters such as location, time and duration of inactivity.


## Existing solutions in process
Global Fishing Watch (GFW) is an organization that analyzes data from the Automatic Identification System (AIS), which is collected by satellites and terrestrial receivers, to identify apparent fishing behavior based on the movement of vessels over time.

<img src="https://github.com/AkankshaAI/Sustainers-Hackerflow-2.0/blob/main/images/solu.png" width="600" align="centre" > 


## Our Solution

AIS system was put in place to guarantee the safety of vessels, it provides collision avoidance and allow maritime authorities to track and monitor vessel movements. Each vessel periodically reports information including the vessel’s identity, type, position, course, speed, navigational status and other safety-related information.

<img src="https://github.com/GinaE/Detecting-fishing-activity/blob/master/images/direct_AIS_limitations.png" width="600">  

Vessels fitted with AIS transceivers can be tracked by AIS base stations located along coast lines or, when out of range of terrestrial networks, through a growing number of satellites that are fitted with special AIS receivers and manage to map the position of the vessels [2]. 

<img src="https://github.com/GinaE/Detecting-fishing-activity/blob/master/images/Satellite_AIS.png" width="600"> 

20M of data points are produced per day this way. In this project we will have data that has been already labeled by different experts and using crowd sourcing methods. 

## Results

<img src="https://github.com/AkankshaAI/Sustainers-Hackerflow-2.0/blob/main/images/results.png" width="600"  > 

The data set was kindly made available by David Kroodsma and Timothy Hochberg from [SkyTruth](http://skytruth.org/).


Notes on the data:

The data features include the type of vessel (troller, drifting long lines, fixed gear) and time series of position, speed, and course of each vessel.
The intervals of data acquisition is not constant. There may be gaps when the vessels are not on the satellite’s field of “view”. It takes 90 mins for a low orbit satellite to go around the globe, so we can expect gaps of up to 1 hour. 

When there is good coverage the time intervals still vary from 2 seconds to 2 minutes, due to differences in satellite communications around the world and signal interference.

### References

[1]  http://www.ipsnews.net/2016/09/new-public-website-offers-detailed-view-of-industrial-fishing/
[2]  ExactEarth Technologies, https://en.wikipedia.org/wiki/Automatic_identification_system

## What you can do in this repo

## Repo Structure


- data/labeled - This folder has a sample file: "alex_crowd_sourced_Purse_seines.measures.labels.npz", please copy the rest of the data files from [GFW training data](https://github.com/GlobalFishingWatch/training-data/tree/master/data/labeled) here. 
- images - Images used on the web app

- results: 
	- best_reconstructions: Images of the recostructed tracks superimposed to maps.
	- final_models: Best performing models, you can find the pickle files here on the '.pkl' files, as well as a summary of their performance on the '.txt' files.
	- models_performance.png

- src - The scripts used in the analysis

	- grid_search_multicolumns.py

		Grid search for each model specified on the models_dict dictionary. It takes 3 arguments, run it in the console like this:

		> python grid_search_multicolumns.py model_number model_type gear_type 

		The possible values for the arguments are:

		|   Argument   |						 values 								|
		|--------------|:-------------------------------------------------------------:	|
		| model_number | ['model_1','model_2','model_3','model_4','model_5','model_6'] 	|
		| model_type   | ['RF','GBC']               									|
		| gear_type    | ['longliners','trawlers','purse_seines'] 						|

		For example, to run the grid search on a Random Forest (RF), for model_1 and the longliners, you should write:

		> python grid_search_multicolumns.py model_1 RF longliners 


	- reconstructing_tracks.py
		For a given mmsi (vessel identification number) this script will generate two images of the tracks, one indicationg the actual fishing sites (in green) and another images with the predicted fishing sites (in blue.) 
		The images then will be kept on ../results/best_reconstructions

	- results_analysis.py
		Produces a graph of the F1-scores for the different models and stores it on ../results


## Our Solution Glimpses from Presentation

<img src="https://github.com/AkankshaAI/Sustainers-Hackerflow-2.0/blob/main/images/ss.png" width="600" align="centre" > 

<img src="https://github.com/AkankshaAI/Sustainers-Hackerflow-2.0/blob/main/images/ss1.png" width="600" align="centre" > 
