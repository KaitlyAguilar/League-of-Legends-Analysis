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

<iframe src="assests/kill-count.html" width=800 height=600 frameBorder=0></iframe>

The pie chart above shows the percentage of games won by teams that earned an above average kill count and the percentage of games won by teams the earned a below average kill count.

__Bivariate Analysis:__

<iframe src="assests/High-vs-Low.html" width=800 height=600 frameBorder=0></iframe>

The graph above shows the percentage win rate for teams that scored above avgerage kill counts and the percentage win rate for teams that scored above average assists counts.

__Pivot Table:__

| Result | False | True |
|----------|----------|----------|
|   teamname   |      |      |
|   100 Thieves   |   3.0   |   20.0   |
|   100 Thieves Challengers	   |   2.0   |   19.0   |
|   19esports   |   2.0   |   15.0   |
|   3BL Esports	   |   6.0   |   13.0   |
|   5 Ronin	   |   1.0   |   1.0   |
|   ...   |   ...   |   ...   |

The pivot table above shows whether a team won or lost corresponding to their above average assists count. For example, the first row shows that the team 100 Thieves scores above average assists in three games but lost, while scoring 20 above average assists in the rest of their games and winning those.


# Assessment of Missingness

__NMAR Analysis__

Yes, I believe that there are multiple columns that are classified as Not Missing At Random (NMAR). There are four columns that were found to be NMAR in the dataset. These include ban1, ban2, ban3, and ban4 which all indicate the character that has been banned from a certain player. Therefore, when there are missing values in any of these columns, you can conclude that there was no banned character for that specific player. 

__Missingness Dependency__


# Hypothesis Testing

*We will be analyzing a different question than the previous one*

__Null hypothesis__: The mean number of kills by winning teams is the same as the mean number of kills by non-winning teams

__Alternative hypothesis__: The mean number of kills by winning teams is greater than the mean number of kills by non-winning teams

__Test stat__:  Difference in Means
* I chose the difference in means because we are using quantitative data and we have direction in our hypothesis.

__p-value__: 0.0
* I did 1000 simulations

__Significance level__: 0.05
* I chose this significance level because it it standard

__Conclusion__: We reject the null hypothesis. Meaning the number of mean kills by winning teams is no the same as the mean number of kills by non-winning teams.

Since we reject the null hypothesis, this means that there is a difference in the number of kills between winning teams and non-winning teams. I believe that number of kills a team earns has influence on the outcome of the match.

<iframe src="assests/kill-count.html" width=800 height=600 frameBorder=0></iframe>

# Framing the question

I am trying to predict whether a team won or lost, therefore this type of prediction problem is classification. Since there are only options we are trying to predict, my classifier will be performing binary classification. The variable we are choosing to predict is the result column which contains whether a team lost or won a game. The metric I chose to evaluate my model was accuracy. Accuracy is a suitable metric because the two classes we are predicting are approximately balanced since for every True(win) there is a False(Lost).

# Baseline Model

In order to predict whether a team will win or lose a game, we are going to start grabbing features that we believe to be influential to the outcome. The features that were chosen for the baseline model(RandomForestClassifier) were:  ‘kills’, ‘side’ and ‘totalgold’. The ‘result’ column is what we are trying to predict therefore it will not be used in our baseline model, but will be used to help train the model. Why were these features chosen? : 

* ‘Kills’ - Kills provide gold and experience advantages, this allows team members to level up their champions giving them a better chance at winning. The kills feature is a quantitative feature.
* ‘Side’ - There is a possibility one side (red or blue) may provide a team an advantage. The side column was hot one encoded in order to make the categorical values quantitative 
* ‘Totalgold’ - Similar to the ‘Kills’ column, earning more gold can level up champions giving players advantages. The Totalgold feature is a quantitative feature.

__Encoding__:
There was only one column that I encoded and that was the 'side' column. I encoded the column so it would make two columns where one had 1's for trues and 0's for falses. This would label the teams as either being on the blue side of the map or the red side.

# Final Model

In order to better the model I engineered a few features.
Added Features:
* Gamelength(used to make new features) - I used game length to find the number of kills per second a team had to better predict the outcome for a team. Helps produce other columns such as kill_per_s.
* kill_per_s - Calculates the average kills per second a team gets. This shows on avgerage how good a teams skill increasing the likelihood of a team winning.
* Totalgold (Avg) - The total goal column was binarized by the avg amount of gold that was earned throughout the entire dataset. Is a good indicater of players who may have been able to level up their champions giving them advantages.
* Assists (Avg) - The assits was binarized by the avg amount of assits that were earned throughout the entire dataset. This is good as assists also generate more gold giving allowing players to level up their champion.

# Fairness Analysis
