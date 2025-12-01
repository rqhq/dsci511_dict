# NBA MVP Dataset - Data Dictionary
## Overview
This documentation provides detailed descriptions of the variables in the NBA MVP dataset. this dataset provides advanced metrics and statistics that require further explanation. These performance metrics are for 33 star-caliber players that have averaged 20+ points per game spanning from 2021-2022 through the 2024-2025 seasons.

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
### NET_RATING
| Attribute | Value | 
|----------|----------|
| Data Type   | Float   | 
| Description   | Point differential per 100 possessions when the player is on the court  | 
| Formula   | Off. Rating - Def. Rating | 
| Typical Range   | -15.0 to +15.0   |
| Elite Threshold   | +15.0 to +20.0  | 
| Interpretation  | Positive = team outscores opponents with player on court while Negative = team is outscored  |
| Importance | Measures overall impact on team success and accounts for pace differences between teams  |
