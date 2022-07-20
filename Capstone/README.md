## Contents:
- [Problem Statement](#Problem-Statement)
- [Data](#Data)
- [Notebook Descriptions](#Notebook-Descriptions)
- [Modeling and Preprocessing](#Modeling-and-Preprocessing)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)
- [Executive Summary](#Executive-Summary)
- [References](#References) 

---

## Problem Statement

Through analyzing this dataset for Search and Rescue missions, what are the key factors that indicate the timeframe to locate and rescue victims both in wilderness and non-wilderness environments? 

This data analysis and subsequent classification models reveal the key factors that either increase or reduce the timeframe of a SAR mission. These analyses are meant to aid SAR teams/organizations in their efforts to minimize mission timeframes, educate individuals on SAR processes and how they can improve their chances of being located/rescued, and conclusively show certain states with higher frequency of SAR incidents have shorter timeframes for mission success.    

---

## Data
This data was collected from the [Mountain Rescue Association](https://mra.org). The original dataset can be found [Here](https://experience.arcgis.com/experience/5a9928653c6c45ca94ae29c8ce90cf91/page/Open-Data/)


## Data Dictionary

|Feature|Description|
|--:|:--|
|**time_bin**|**Target:**  0-11 hours, 11-32 hours, 32 hours-7 days|
|**number_volunteers**|Number of volunteers (continuous variable) involved in SAR mission|
|**number_subjects**|Number of subjects involved in SAR mission (limited to up to 10 subjects)|
|**area_type**|**Type of area:** wilderness, urban_rural, unknown, water, interface (urban/rural/wilderness)|
|**total_aircrafts**|Number of different types of aircrafts involved: helicopter, fixed-wing, UAV|
|**children**|OHE feature where children (1-15 years old) involved|
|**seniors**|OHE feature where seniors (65+) involved|
|**mental**|OHE feature where any subject has a mental factor or rating other than normal|
|**winter**|OHE feature for incidents occuring in winter months or snow conditions|
|**daylight**|OHE feature where mission initiated in daylight hours (7am - 8pm)|
|**state**|Dummified feature for each state out of 19 states|

---

## Notebook Descriptions

|Notebooks|Description|
|:--|:--|
|**[01_EDA.ipynb](https://github.com/deemerwsp/FINAL_CAPSTONE/blob/main/Capstone/Code/01_EDA.ipynb)**|Exploratory Data Analysis and Feature Engineering|
|**[02_Preprocessing.ipynb](https://github.com/deemerwsp/FINAL_CAPSTONE/blob/main/Capstone/Code/02_Preprocessing.ipynb)**|Preprocessing: dummifying, scaling, train test split|
|**[03_Logistic_Regression.ipynb](https://github.com/deemerwsp/FINAL_CAPSTONE/blob/main/Capstone/Code/03_Logistic_Regression%20.ipynb)**|Modeled Logistic Regression algorithm on processed data|
|**[04_Random_Forest.ipynb](https://github.com/deemerwsp/FINAL_CAPSTONE/blob/main/Capstone/Code/04_Random_Forest.ipynb)**|Model Random Forest algorithm on processed data|
|**[05_Presentation_Visualizations.ipynb](https://github.com/deemerwsp/FINAL_CAPSTONE/blob/main/Capstone/Code/05_Presentation_Visualizations.ipynb)**|Created visualizations for technical and non technical reports|

## Modeling and Preprocessing

**Data Cleaning:** The data was subsetted to only include incidents that were true and ***typical*** Search and Rescue missions. The cleaned dataset included 10,000+ datapoints. All datapoints include atleast one live victim. The dataset was limited to incidents occuring after 2013 when SAR teams began regulary inputing data into this database. Only datapoints with a timeframe under 7 days were included. The dataset was limited to datapoints including a maximum of 10 subjects. Outliers for each feature were dropped from the dataset. Null values were imputed manually by comparing other relatable features e.g. Area Type imputed as "wilderness" where other similar features included "wilderness".

**Preprocessing:** Several engineered features were one-hot-encoded. Other categorical variables were dummified. Continuous variables were scaled using Standard Scaler. The processed data was split into train and test sets. 

**Modeling:** Hyperperameters for both classification models were gridsearched. Resulting parameters were tested with Cross Validation. Test sets were used to make predictions and metrics were included to show accuracy, precision, and recall for both classification models. 

---


## Conclusions and Recommendations

The Logistic Regression model offers more human interpretabillity and thus is the recommended production model. SAR teams can benefit most from this algorithm in understanding what contributes to reducing the timeframe for completing a SAR mission. This model is 57% accurate in predicting the target class, 22% more accurate than the baseline model of 35% probability by predicting the majority class - 32 hours to 7 days. 

The Random Forest model is 58% accurate in predicting the target - timeframe. The top most important feature for the Random Forest model it the number of volunteers involved in the SAR mission. This feature was also important for the Logistic Regression model. The number of volunteers increase over time as the search for victims continues. Based on this fact, I would recommend SAR teams incorporate a grass-roots effort to sign up volunteers willing to participate in SAR efforts and maintain a system to activate these volunteers as soon as possible. This would allow these volunteers to participate sooner and reduce the timeframe for SAR mission success. 

The Logistic Regression model determined the state in which a SAR mission occurs to be the best indicator of target class. Both California and Colorado comprised of more than 60% of this dataset. Their average mission total hours are 16 and 20 hours respectively. This is considerably lower than half of all included states. Utah, Oregon, and New Mexico together comprise of 10% of this dataset. All had average total hours to mission success above 30 hours. Both California and Colorado having higher frequency of incidents and lower average total hours indicate that these states out perform SAR missions in other states. I recommend conducting a study on these SAR teams and organizations. Are these states benefiting from government funding and support systems? My second recommendation is to create an organization that would allow SAR teams accross the country to collaborate and share their knowledge and methods. 

Evidently aircrafts are most often deployed when missions exceed 32 hours. These essential aircrafts do reduce the timeframe for SAR mission success. Few incidents involved the use of UAVs. This technology is rapidly advancing and has potential to benefit SAR missions. The Coast Guard employ search patterns when a sailor is reported overboard. These search patterns are designed to aquate for ocean currents and time of event. UAVs could be programmed in a similar fashion to conduct search patterns over land areas. They also can incorporate infrared cameras for night searches. If UAVs are small and highly maneuverable, they can make contact with victims on-site and communicate with them. I highly recommend researching how to incoporate UAVs into SAR efforts. 

GPS transponders have become increasingly popular and affordable over the past 10 years. These devices are truly indispensable. Only 1% of this dataset included incidents where victims used GPS transponders. The average total hours for these incidents was 12 hours. These devices allow users to send SOS messages that directly call emergency responders. 75% if the datapoints in this dataset occured in a "wilderness" evironment, where SAR efforts are the most difficult. I recommend educating these adventure seekers about these devices. 

My final recommendation is to lobby congress for a federal program aimed towards mitigating risks for civilians enjoying our country's National Parks and Wilderness areas. The federal Forest Service oversees all National Parks and Wilderness areas. Most trails have points of information (e.g. trail heads) where maps and details about wildlife are displayed. I recommend creating pamphlets on SAR "what-to-do" and preparedness be provided at these information outlets. This would be the most efficient method of distributing information to individuals entering these high-risk, wilderness environments.  


## Executive Summary

Search and Rescue is a public service that has become increasingly necessary as more civilians enjoy our beautiful national parks and wilderness areas each year. There are inherent risks when people endeavor any adventure into the outdoors. These SAR missions are the safety net that mitigate those risks and save lives. As the number of civilians venturing out into these risk proned environments increases, the necessity of these professional SAR teams increases. 

For the most part, these SAR teams are not funded by the government and are comprised of non-paid volunteers. Members of these SAR teams are highly skilled and predominantly philanthropic. These SAR teams are becoming overwhelmed and financially unsubstainable. Certain states like California and Colorado have higher frequencies of SAR missions and understand the importance of this public service. 

Wilderness Environments have the largest average total hours for SAR missions and require the most attention. 

**Summary of Recommendations:**
1. SAR teams build volunteer reserves able to immediately be called into action. 
2. Study California and Colorado SAR teams/organizations and their government funding/programs
3. Create a federal association for SAR teams and organizations across the country to share knowledge and methods 
4. Research UAV's ability to aid SAR missions
5. Promote aqcuiring GPS transponders for anyone going into National Parks and Wilderness areas
6. Lobby Government to provide SAR information pamphlets at ports of information in our National Parks and Wilderness areas

---

## References

[America’s busiest search-and-rescue system at risk of collapse, study finds](https://www.outsidebusinessjournal.com/issues/a-new-study-finds-americas-busiest-search-and-rescue-system-is-at-risk-of-collapse/)

### Presentations

[Non-technical](https://github.com/deemerwsp/FINAL_CAPSTONE/blob/main/Capstone/SAR%20Non%20Technical%20Presentation.pdf)
[Technical](https://github.com/deemerwsp/FINAL_CAPSTONE/blob/main/Capstone/SAR%20Technical%20Presentation.pdf)
