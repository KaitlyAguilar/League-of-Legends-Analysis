# League-of-Legends-Analysis
This is a project for DSC80 at UCSD

By Kaitly Aguilar

# Introduction

Our dataset encompasses all professional League of Legends matches held in 2023. Each game is represented by 12 rows, with 10 rows dedicated per player and an additional two rows providing summary statistics for each participating team in the match. In this anlysis we will answering a couple of questions: Is a team more likely to win with a higher kills count or assists count? and  Is the mean number of kills by winning teams is the same as the mean number of kills by non-winning teams?

Individuals engaged in League of Legends gameplay may seek insights into strategies that enhance their chances of winning. Additionally, new players can utilize these findings to prioritize their learning objectives effectively.

__Description of Columns:__

The columns that we usefule in the analysis were:

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
