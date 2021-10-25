
<div><img src="img1.png" alt="t20 Image"></div>


# ICC Men's T20 World Cup 2021

<p> Though football is one of the most popular games in the world but when it comes to cricket, ICC's tournaments are not far behind.
It doesn't matter, if you are a cricket fan or not, you must have encountered some cricket-based ads, blog links, and whatnot. So many promotional advertising messages and emails must have made you realize, how religiously people follow cricket and like to discuss it. In this blog, We would discuss this year's Cricket World Cup, various participating teams, their statistics, and past performances. We will be concluding our discussion by methodically predicting finalists, semi-finalists, and top teams in the qualifier round.</p>

### Why prediction?

<p> Humans have always been curious about the future. Knowing what would happen in near future beforehand is no less than a superpower. Presently, researchers and scientists are using historical data to observe patterns to forecast/predict upcoming events so our lives can be easier. In statistics, the words prediction, forecasting, and estimation are identical and can be used interchangeably. "Prediction" more naively can be described as a well-informed guess or opinion. Therefore, in this article, we will use the magical power of historical data to predict the winners of the tournament before they actually win.</p>

### Where to begin?

Before we procure our superpower to predict, We have to acquire the magical power of historical data first. There is a lot of cricket data available on the internet through different sources but most of them are outdated. For our problem, we would require the latest data to make our predictions precise. The following links are some of the most credible sources for cricketing data.

For T-20 data : [ESPN_CricketInfo](https://stats.espncricinfo.com/ci/engine/stats/index.html?class=3;template=results;type=aggregate;view=results)

For IPL data : [HowStat](http://www.howstat.com/cricket/Statistics/IPL/MatchList.asp)

This source (espncricinfo) has all the ICC T20 match records along with full scorecards. I have used  **Beautifulsoup** , A python library for scraping data from a static webpage. If you are curious about how to do it, You can [click here](DataScraping_espn.ipynb) to check the source code.
Now we have acquired our magical power of historical data, our next step would be to explore this power so we can use it for good.

### Exploring magical power "Data"

We have 1374 T20 match records from 17th-Feb-2005 till 18th-Oct-2021. We will be using only those matches which resulted in a "win" for either team, removing " n/r or tied ".

Let's consider the  most hyped "India vs Pakistan" upcoming match and analyze it


![indvpak!](indvpak.jpeg?style=centerme "Head to Head")

The above figure shows the head to head win percentages for both the team. It is evident that india has performed well between the two.

<br />
<br />

**Now we will compare their batting, and see who dominated the batting department**

<br />

![indvpak_30+!](indvpak_30+.jpeg "Players scored 30+")

More number of players scored 30+ runs and led pakistan to victory in third match.
Apparently, only one player scored 30+ in following matches from pakistan greecing the wheels for india's win.

<br />

![indvpak_run_rate!](indvpak_run_rate.jpeg "team run rate per match")

Scoring at better run rates than pakistan in most matches evince win for india.

<br />
<br />

**Lets explore the bowling aspect of both teams**

<br />

![indvpak_team_extra!](indvpak_team_extra.jpeg "Team extras")

Initially, indian bowling had rewarded pakistan with few extras which seem to be imporved in latter matches.
Lets have a glance over the bowling economy to get a clear distinction between the two teams.
<br />

![indvpak_bowl_econ!](indvpak_bowl_econ.jpeg "Bowling economy")

Above infographic evince an economical bowling of indian team. 

Although indian batting and bowling looks impressive on the graphs, opponent stats looks promising too.

### Procuring superpower "The prediction model"

Without further ado, lets initiate with the due process of building a prediction model. The data we hold not just has coarse but granular features too. Coarse features help menoeuvre vanilla probabilistic model whereas we can employ coarse, granular and few derived features for advanced statistical algorithms like **Logistic Regression**.    

<br />

**Vanilla model**

Vanilla model is nothing but very basic non-complex model. This approach uses past match records of the two competing teams and calculate probabilities of win and lose. In case both the teams never had a face off earlier or both are equally likely to win, then either team with better ICC rankings will be predicted as winner.   
curious how to do it? [click here](vanilla_model.ipynb) to see the code.

The motivation behind this approach is to utilize past head to head contested battles between the teams. Below are phase1 predictions of the model

![indvpak_bowl_econ!](phase1_vanilla_model.PNG "Phase1 prediction")

<br />

**Logistic Regression**

Since logistic regression is a supervised learning algorithm, therefore feature 'winner' be our target column. Logistic regression takes independent variables as input and results log(Odds) that later converted into P(1/X) i.e. probability that given observation belongs to class 1. We can use different probability threshold for classification between classes, default is 0.5. The advantage of logistic approach over vanilla approach is logistic takes team batting, bolwing, and drived attributes as input and weigh them appropriately.

The column "winner" has 1, 2 as values representing "Team1" and "Team2". (Note: 0 & 1, 1 & -1 can also represent team1 and team2 numerically)    

We can derive few variables using existing variables. Deriving new features require good understanding of data and can really help to improve model performance. Following list shows derived variables with "t1" and "t2" as prefix.

> 't1_matches_played', 't1_matches_won','t1_matches_lost', 't1_win_per', 't1_odds_of_win', 't1_win_prob','t1_past10_win_per', 't1_past10_lose_per', 't2_matches_played', 't2_matches_won', 't2_matches_lost', 't2_win_per', 't2_odds_of_win','t2_win_prob', 't2_past10_win_per', 't2_past10_lose_per'

Further process to build and train logistic regression model is mentioned [here](logistic_model.ipynb).   
**Note: I have also used IPL data along with T20 because the format of the game and methodology to derive team1, team2 attributes are same.**

Following is the AUC_ROC score for the logistic regression model after training. Better the AUC_ROC score, better the capability of model to differentiate between two classes.

![auc_roc!](auc_roc.jpeg "Logistic Regression AUC_ROC")

you can [click here](logistic_model.ipynb) to see the logistic model code and [here](log_super_12.csv) to see super 12 predictions.
Now we are ready with superpower of prediction. Lets use it for further prediction.

### Using the Superpower

#### Vanilla model prediction for super 12 matches

![vanilla!](vanilla.JPG "vanilla prediction phase 2")

Semi Finalists 
* Group 1
  1. Australia
  2. West Indies
  
* Group 2 
  1. India
  2. Pakistan

Finalists 

India vs Pakistan

![vanilla_final!](vanilla_final.JPG "vanilla prediction finalists")

Winner 

India

![vanilla_winner!](vanilla_winner.JPG "vanilla prediction winner")


#### Logistic regression model prediction for super 12 matches

![log_reg!](log_reg.JPG "log_reg phase 2")

Semi Finalists
* Group 1
  1. South Africa
  2. England

* Group 2
  1. Pakistan
  2. India

Finalists 

India vs Pakistan

![log_final!](log_final.JPG "vanilla prediction finalists")

Winner 

Pakistan

![log_winner!](log_winner.JPG "vanilla prediction winner")

**Note : I have used ICC ranking to resolve the ambiguity between the teams to select top 2 from each group in super 12**
