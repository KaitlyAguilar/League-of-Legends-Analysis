# League-of-Legends-Analysis
This is a project for DSC80 at UCSD

By Kaitly Aguilar

# Introduction

Our dataset encompasses all professional League of Legends matches held in 2023. Each game is represented by 12 rows, with 10 rows dedicated per player and an additional two rows providing summary statistics for each participating team in the match. In this anlysis we will answering a couple of questions: *Is a team more likely to win with a higher avgerage kills count or higher avgerage assists count?* and  *Is the mean number of kills by winning teams is the same as the mean number of kills by non-winning teams?*

Individuals engaged in League of Legends gameplay may seek insights into strategies that enhance their chances of winning. Additionally, new players can utilize these findings to prioritize their learning objectives effectively.

__Description of Columns:__

The columns that were usefule in the analysis were:

* __Kills__ - Total kill count for the team
* __Assists__ - Total assists count for the team
* __Result__ - True if the team won the game, otherwise False
* __Position__ - Position of player or team if row belongs to the team statistics
* __League__ - The leaague the games belong to
* __Damagemitigatedperminute__ - A teams damage mitigaded per minute
* __Side__ - Side the team was one (red or blue)
* __Total_gold__ - Total gold earned in a game                                                  
* __Gamelength__ - The tota; length of a game in seconds

I chose these columns because they provided the rigth information needed for the tests. They provided the results of the games and other factors such as kills, assists, total_gold, etc. Other columns such as position were used to filter through the data, ensuring our dataframe consisted of only the summary statistics for each team.


# Data Cleaning and Exploratory Data Analysis

__Data Cleaning__

To begin cleaning the data, I frist started by grabbing all the columns I needed. These columns included: 'kills', 'assists', 'results', and 'position'. Later on in the analysis I would go back into my data set and retrive other relevant columns. I chose to focus maininly
on the outcome of teams rather than individual player performances as I would be looking for overall kill and assists count per game. As a result, I only extracted rows corresponding to the summary statistics of the two teams, necessitating a search through the 'positions' column. Next, I searched for any misssing values in the data, but none were found. Since I was looking for teams that scored above average kills and assists counts, I transformed the kills and assists data into a series of Boolean values, with 1 indicating that the team achieved above-average kill or assist counts, and 0 indicating otherwise.

| __Result__ | __Kills__ | __Assists__ |
|----------|----------|----------|
| True  | 0  | 1  |
| False | 0  | 0  |
| False | 1  | 1  |
| True  | 1  | 0  |
| True  | 1  | 1  |
|  ...  | ...| ...|

__Univariate Analysis:__

<iframe src="assets/kill-count.html" width=800 height=600 frameBorder=0></iframe>





