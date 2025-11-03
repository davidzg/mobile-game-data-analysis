# mobile-game-data-analysis
Game progression analysis of a mobile game
## Introduction
In this project I am performing an Exploratory data analysis from a mobile game.
The questions to answer with this project are:
1. How engaging are the levels? are they fun and challenging?
2. Which levles would need a rebalance to offer a better user experience


### About the game
"Jungle Vine Runner" is a fictional game where players control a character that swings on vines and collects bananas and other special collectibles. The game is divided in consecutive levels, and each one has its own Goal and restrictions. This project only will analyse the first 50 levels.

### About the data
#### Source data
- The data used for this project are the game logs for one day.
- The data has been annonymised.
#### meatadata
The "levels.csv" file contains each level's configuration, like the goal and restrictions that applay for the specific level. This file is the point of comparison to estimate how well the players has played an specific attempt. Here is the structure of this data:

|Column |Description    |
|-----|----|
|lvl|Level number|
|goal_type|There three types of goal: Collect bananas,reach a distance, or collect special collectibles|
|goal_value|The goal value to meet|
|limit_type|There are two types of restriction: Time restriction, Swings restriction|
|limit_value|The restricition value to meet|
|target_goal|Collecting objects will increase the scoring. Players must meet the specific scoreing in order to win the level.|

The "logs.csv" file stores logs about each attempt to complete a level.
The log data contains information that is not of interest for this project, and is cleaned or discarded during the EDA process. The prepared and cleaned data is stored in the "logs.csv" and is structured as follow:

|Column |Description    |
|-----|----|
|device_id|Unique id to identify the user|
|date_time| log date and time|
|level_number|Level number played (1-50)|
|end_reason|win ('win') or fail ('time' or 'swings')|
|lives_left|lives left by the end of the attempt|
|n_bananas|numbers of bananas collected by the end of the attempt|
|n_distance|distance advanced by the end of the attempt|
|n_specialcollectibles|number of special collectibles collected by the end of the attempt|
|n_swings|number of swings left over by the end of the attempt|
|pathtrace|A set of coordinates that traces the path the character has travelled during the attempt|
|stars|number of stars earned in this attempt|
|swings_left|number of swings left over by the end of the attempt|
|time_used|duration of the attempt|
|total_duration|duration of the attempt|
|score|final score|
## Analysis
There are two notebooks. The first one takes the raw logs files and transforms it into a more maneagable dataset with the columns of interest for this project. In this process there is also some data cleaning and formatting.
The second notebook takes as input the compacted data and performs the analysis by filtering, grouping and shaping the data, to finally generate some visualizations to help to understand the data and extract the insights.

## Results

In the following chart, the red line represent the 100% completness.

![Alt text](./visualizations/completeness_by_level_and_goal.png)

<!-- ![Alt text](./visualizations/output.png) -->

We can define an engaging level as one where the median (green line of each boxplot) of completeness is close to 100% (red line). Meaning the level difficulty feels right, challenging but achievable. 
It is also important to keep the IQR (inter-quartile range) of the boxplot intersecting the red line.

### insights
- With the definitions in mind, the obvious observation is that early levels feel engaging and sometimes easy (levels 1,2, 11, 12), this is intended to have this difficulty as it represent the FTUE (first time user experience) content.
- Level 15 has a wide boxplot, indicating the variety of player skills. the IQR is above the 100% completeness, indicating that this level is too easy, and potentially boring to users.
    - The same conclusion could be said about levels 12, 17 and 21.
- There are also levels that are too challenging as their IQR is below 100%, these levels 
- levels where the goal is to collect special colletibles are generally on the difficult side.
- Levels where the goal is to collect bananas become harder asfter level 20.

### Recomendations
- Rebalance the levels where the goal is to collect special collectibles to make them easier, this can be done by adding more collectibles to the map.
- Level 15 can be made more challenging, as it is still part of the FTUE it is recommended to keep it on the Easy difficulty still.
