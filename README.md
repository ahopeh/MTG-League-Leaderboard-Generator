# MTG-League-Leaderboard-Generator

# **Gaming League Leaderboard Calculator - User Guide**

This Python script automatically calculates player rankings for your card gaming league based on your custom scoring rules. Here's how to use it:

## **📥 Setup Requirements**
1. **Python 3.6+** installed on your computer
2. **Required Libraries** (install via command prompt):
   ```bash
   pip install pandas numpy openpyxl
   ```

## **📂 Preparing Your Data**
Create an Excel file (`league_scores.xlsx`) with these columns:

### **🔹 Required Columns**
| Column Name               | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| `player_name`             | Player's name                                                               |
| `individual_games_played` | Total # of individual games played                                          |
| `individual_points`       | Sum of all points earned from individual games                              |
| `max_individual_possible` | Maximum points possible based on games played (games × pod size)            |

### **🔸 Per Draft Event Columns**  
*For each draft event (name them `draft_1`, `draft_2`, etc.):*

| Column Pattern            | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| `draft_X`                 | Any value = participated (leave blank if didn't attend)                     |
| `draft_X_rounds`          | Number of rounds (2 or 3)                                                   |
| `draft_X_wins`            | Total wins in the event                                                     |
| `draft_X_losses`          | Total losses in the event                                                   |
| `draft_X_undefeated`      | Number of undefeated rounds (0-3)                                           |
| `draft_X_bye`             | `TRUE` if received a bye round, else `FALSE`                                |
| `draft_X_clean_sweep`     | `TRUE` if went 3-0              |

*Example:*  
![Example Excel Structure](https://i.imgur.com/JQjyWQxl.png)

## **🚀 Running the Script**
1. Save the Python code as `league_scorer.py`
2. Place it in the same folder as your `league_scores.xlsx`
3. Run it:
   ```bash
   python league_scorer.py
   ```

## **📊 Understanding the Output**
The script generates:
1. **Console output** showing the ranked leaderboard
2. **league_leaderboard.xlsx** with detailed breakdowns:

| Column                  | Description                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| `rank`                  | Final position                                                              |
| `player_name`           | Player identifier                                                           |
| `final_score`           | Total score (individual + draft + bonuses - penalties)                      |
| `individual_score`      | Points from individual games                                                |
| `draft_score`           | Points from all draft events                                                |
| `penalty`               | Deduction for missing games (if played <15)                                 |
| `grinder_bonus`         | Bonus = (player's indiv. score / best max indiv. score in league)           |
| `games_played`          | Total individual games played                                               |
| `draft_events_attended` | How many drafts the player joined                                           |
| `max_*_possible`        | Shows theoretical maximum points for reference                              |

## **🛠️ Customization Options**
Edit these constants in the code if needed:
```python
MIN_GAMES = 15                # Minimum required individual games
PENALTY_MULTIPLIER = 3        # Penalty = (15 - games_played) × this
DRAFT_WIN_POINTS = 4          # Points per draft win
UNDEFEATED_ROUND_BONUS = 3    # Bonus for going undefeated in a round
CLEAN_SWEEP_BONUS = 10        # Awarded for going undefeated in a draft event
```

## **💡 Pro Tips**
- The script automatically:
  - Handles any number of draft events
- For large leagues (>50 players), the script may take a few seconds to run
- Empty cells in Excel are treated as "did not participate"

