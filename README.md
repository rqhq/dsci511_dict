# NBA MVP Dataset - Data Dictionary
## Overview
This documentation provides detailed descriptions of the variables in the NBA MVP dataset. This dataset provides advanced metrics and statistics that require further explanation. These performance metrics are for 33 star-caliber players that have averaged 20+ points per game spanning from 2020-2021 through the 2024-2025 seasons.

 
## Player Identification
| Column | Data Type | Description |
|----------|----------|----------|
| PLAYER_ID   |  Integer  | Unique identifier assigned by the NBA to each player  |
| NAME  | String   | Each player's full name  |

## Sample Information
| Column  | Data Type | Description | Notes |
|----------|----------|----------|----------|
| TOTAL_GAMES   | Integer   | Number of games each player played in | Important to take into consideration how many games the player played for statistical significance in averages. Higher values = more reliable averages.|

## Essential Advanced Metrics
Note: All percentages are in float form i.e. 15% = 0.15
### NET_RATING
| Attribute | Value | 
|----------|----------|
| Data Type   | float   | 
| Description   | Point differential per 100 possessions when the player is on the court  | 
| Formula   | Off. Rating - Def. Rating | 
| Typical Range   | -15.0 to +15.0   |
| Elite Threshold   | +15.0 to +20.0  | 
| Interpretation  | Positive = team outscores opponents with player on court while Negative = team is outscored  |
| Importance | Measures overall impact on team success and accounts for pace differences between teams  |


### TS_PCT (True Shooting Percentage)
| Attribute | Value | 
|----------|----------|
| Data Type   | float   |
| Description   | Scoring efficiency metric that accounts for field goals, 3-pointers, and free throws  |
| Formula   | Points / (2 x (FGA + 0.44 × FTA))  |
| Typical Range  | 45% - 70%   |
| League Average   | 58%   |
| Elite Threshold   | 65%+   |
| Interpretation   | Higher = more efficient scorer. Takes in to account for the value of 3-pointers and free throws unlike basic FG%  |
| Importance   | Most accurate single measure of scoring efficiency and again is better than FG% for comparing players  |

### USG_PCT (Usage Percentage)
| Attribute | Value | 
|----------|----------|
| Data Type   | float   |
| Description   | Percentage of team plays used by the player while on the court |
| Formula   | 100 × ((FGA + 0.44 × FTA + TOV) × (Team Minutes / 5)) / (Minutes × (Team FGA + 0.44 × Team FTA + Team TOV))  |
| Typical Range  | 15% to 35%  |
| League Average   | 20%   |
| Elite Threshold   | 30%+   |
| Interpretation   | Higher = more involved in team's offense. Star players typically have higher usage  |
| Importance   | Great context for other advanced metrics. High usage pct + high efficiency = star player |

### AST_RATIO (Assist Ratio)
| Attribute | Value | 
|----------|----------|
| Data Type   | float   |
| Description   | Percentage of player's possessions that end in an assist |
| Formula   | 100 × Assists / (FGA + 0.44 × FTA + Assists + Turnovers)  |
| Typical Range  | 5.0 to 25.0  |
| Elite Threshold   | 25.0+, 30.0+ for Point Guards as they typically distribute the ball far more than other positions  |
| Interpretation   | Takes into consideration playmaking as shooting is not everything in the NBA, passing is very important as well  |
| Importance   | Measures playmaking ability independent of team pace and valuable for identifying facilitators vs. scorers |

### REB_PCT (Rebound Percentage)
| Attribute | Value | 
|----------|----------|
| Data Type   | float   |
| Description   | Percentage of available rebounds grabbed by the player while on court |
| Formula   | 100 × (Rebounds × Team Minutes) / (Player Minutes × (Team Rebounds + Opponent Rebounds))  |
| Typical Range  | 3% to 20%  |
| Elite Threshold   | 15% for big men (taller players), 8% for guards |
| Interpretation   | Higher = better rebounding capabilities when a rebounding opportunity occurs |
| Importance   | Takes positioning into account for rebounding instead of just total rebounds |

### PIE (Player Impact Estimate)
| Attribute | Value | 
|----------|----------|
| Data Type   | float   |
| Description   | NBA's catch-all metric estimating a player's overall contribution to game outcomes |
| Formula   | (PTS + FGM + FTM - FGA - FTA + DREB + 0.5×OREB + AST + STL + 0.5×BLK - PF - TOV) / Game Totals  |
| Typical Range  | 5% to 25%  |
| League Average  | Roughly 10%  |
| Elite Threshold   | 18%+ |
| Interpretation   | Represents percentage of game events attributable to player thus higher = greater impact |
| Importance   | A simple single-number summary that can be used for quick player comparisons |

### TM_TOV_PCT (Turnover Ratio)
| Attribute | Value | 
|----------|----------|
| Data Type   | float   |
| Description   | Percentage of player's possessions that end in a turnover |
| Formula   | 100 × Turnovers / (FGA + 0.44 × FTA + Turnovers)  |
| Typical Range  | 5.0 to 20.0  |
| League Average  | Roughly 12.0  |
| Elite Threshold   | Below 10.0 |
| Interpretation   | In this case, Lower = better. This indicates ability to secure the ball |
| Importance   | Critical in considering player's ball-handling ability. Higher-usage players usually have a higher turnover percentage due to the pure volume of involvement  |

## Calculated Metrics
### MVP Score
| Attribute | Value | 
|----------|----------|
| Data Type   | float   |
| Description   | Composite score weighting multiple advanced metrics to estimate MVP-caliber performance |
| Formula   | (NET_RATING × 0.30) + (TS_PCT × 0.20) + (USG_PCT × 0.15) + (AST_RATIO × 0.10) + (REB_PCT × 0.10) + (PIE × 0.10) - (TM_TOV_PCT × 0.05)  |
| Typical Range  | Varies by dataset  |
| Interpretation   | Higher = more MVP-like statistical profile |
| Importance   | Aggregates multiple dimensions of performance into single comparable value for league's top performers |

### Understanding Weight Justification
| Metric | Weight | Reason |
|----------|----------|----------|
| NET_RATING   | 30%   | Strongest indicator for winning impact   |
| TS_PCT   | 20%   | For stars, scoring efficiency is crucial   |
| USG_PCT   | 15%   | MVPs are usually won for offensive impact   |
| AST_RATIO   | 10%   | Playmaking adds value beyond scoring   |
| REB_PCT   | 10%   | Rebounding leads to more team success and more possessions    |
| PIE   | 10%   | Overall impact validation   |
| TM_TOV_PCT   | 5%   | Importance of turning the ball over  |


## Data Quality Indicators
| Filter | Threshold | Reason |
|----------|----------|----------|
| MVP Eligibility  | 65+ games   | This is an official requirement by the NBA. 65 games must be played to be considered for the end of season awards   |
| Statistically Signifcant   | 30+ games   | The law of large numbers: averages stabilize around n = 30 games. This is important for player averages in general but not for MVP eligibility  as it does not reach the requirement |
| Minutes Per Game   | 30+ MPG| Star players usually play a minimum of 30 minutes per game assuming no injury concerns |
| Minimum Points Per Game  | 20+ PPG| Only 1 MVP in the last 40+ years has scored less than 20 PPG and that was an era where the pace of games was slower with better defense. Modern NBA has more scoring and higher pace of play |


## Basketball Terminology Glossary
| Term | Definition | 
|----------|----------|
| Possession   | An offensive opportunity resulting in a shot, foul, or turnover  |
| Pace   | Speed at which a team plays. This is the number of possessions a team has per 48 minutes (full game) | 
| Offensive Rating  | Points scored per 100 possessions   | 
| Defensive Rating   | Points allowed per 100 possessions   | 
| FGA  | Field Goals Attempted   | 
| FTA  | Free Throws Attempted  | 
| TOV   | Turnovers  | 

### Known Limitations
- Missing Context: Injuries, trades, quality of teammates, coaching firings/hirings
- Limited Defensive Metrics Tracked: The defensive stats that are tracked are the basic boxscore metrics
- Opponent Strength: Schedule difficulty is not taken into account
- Team Playstyle: Some teams have higher paces while others play more possession-based basketball (slower)

