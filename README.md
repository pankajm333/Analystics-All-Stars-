# Cricket Performance Analysis-Dashboard

### Dashboard Link:
## Problem Statement

The objective of this dashboard is to assist cricket team selectors in analyzing player performance data to create the best possible team. The team should be capable of achieving the following performance goals:

- Score at least 200 runs on average per match.
- Defend 150 runs on average per match.

## Measures

| Sno | Measures              | Description / Purpose                              | DAX FORMULA                                           | TABLE                |
|-----|-----------------------|----------------------------------------------------|-------------------------------------------------------|----------------------|
| 1   | Total Runs            | Total runs scored by the batsman                   | Total Runs = SUM(fact_batting_summary[runs])          | fact_batting_summary |
| 2   | Total Innings Batted  | Total innings the batsman batted                   | Total Innings Batted = COUNT(fact_batting_summary[match_id]) | fact_batting_summary |
| 3   | Total Innings Dismissed | Total innings the batsman got out                | Total Innings Dismissed = SUM(fact_batting_summary[out]) | fact_batting_summary |
| 4   | Batting Average       | Average runs scored in an innings                 | Batting Avg = DIVIDE([Total Runs],[Total Innings Dismissed],0) | fact_batting_summary |
| 5   | Total Balls Faced     | Total number of balls faced by the batsman        | Total balls faced = SUM(fact_batting_summary[balls])   | fact_batting_summary |
| 6   | Strike Rate           | Number of runs scored per 100 balls               | Strike rate = DIVIDE([Total Runs],[total balls faced],0)*100 | fact_batting_summary |
| 7   | Batting Position      | Batting position of a player                     | Batting Position = ROUNDUP(AVERAGE(fact_batting_summary[batting_pos]),0) | fact_batting_summary |
| 8   | Boundary %            | Percentage of boundaries scored by the batsman   | Boundary % =  DIVIDE(SUM(fact_batting_summary[Boundary runs]),[Total Runs],0) | fact_batting_summary |
| 9   | Avg. Balls Faced      | Average balls faced by the batter in an innings  | AVERAGE(fact_batting_summary[balls])                   | fact_batting_summary |
| 10  | Wickets               | Total wickets taken by a bowler                  | Wickets = SUM(fact_bowling_summary[wickets])          | fact_bowling_summary |
| 11  | Balls Bowled          | Total balls bowled by the bowler                 | Balls Bowled = SUM(fact_bowling_summary[balls])        | fact_bowling_summary |
| 12  | Runs Conceded         | Total runs conceded by the bowler                | Runs Conceded = SUM(fact_bowling_summary[runs])        | fact_bowling_summary |
| 13  | Bowling Economy       | Average runs conceded in an over                 | Economy = DIVIDE( [Runs Conceded], ([balls Bowled]/6),0) | fact_bowling_summary |
| 14  | Bowling Strike Rate  | Number of balls bowled per wicket                | Bowling Strike Rate = DIVIDE([balls Bowled], [Wickets],0) | fact_bowling_summary |
| 15  | Bowling Average      | Average number of runs conceded per wicket       | Bowling Average = DIVIDE([Runs Conceded],[Wickets],0) | fact_bowling_summary |
| 16  | Total Innings Bowled | Total innings bowled by a bowler                | Total Innings Bowled = DISTINCTCOUNT(fact_bowling_summary[match_id]) | fact_bowling_summary |
| 17  | Dot Ball %           | Percentage of dot balls bowled by a bowler      | Dot ball % = DIVIDE(SUM(fact_bowling_summary[zeros]), SUM(fact_bowling_summary[balls]),0) | fact_bowling_summary |
| 18  | Player Selection     | Indicate if a player is selected or not         | Player Selection = IF(ISFILTERED(dim_player[name]),"1","0") | - |
| 19  | Display Text         | Display text when no player is selected          | Display Text = IF([Player Selection] = "1", "", "Select Player(s) by clicking the player’s name to see their individual or combined strength.") | - |
| 20  | Color Callout Value  | Display value when a player is selected         | Color Callout Value = IF([Player Selection]="0", "#D0CF1D","#1D1D2E") | - |

## Calculated Columns

| Sno. | Calculated Column Name | Description / Purpose | DAX formula | Table |
|------|------------------------|-----------------------|-------------|-------|
| 1    | boundary runs          | Total runs scored by hitting fours and sixes | boundary runs = fact_batting_summary[fours]*4 + fact_batting_summary[sixes]*6 | fact_batting_summary |
| 2    | Boundary runs bowling  | Total runs conceded in boundaries by bowlers | Boundary runs = fact_bowling_summary[fours]*4 +fact_bowling_summary[Sixes]*6 | fact_bowling_summary |
| 3    | Custom Batting Order   | Assign batting order to potential final 11   | SWITCH( TRUE(), dim_player[name] = "Jos Butt

ler",1, dim_player[name] = "Rilee Rossouw",2, dim_player[name] = "Alex Hales",2, dim_player[name] = "Virat Kohli",3, dim_player[name] = "Suryakumar Yadav" ,4, dim_player[name] = "Glenn Phillips" ,5, dim_player[name] = "Marcus Stoinis" ,6, dim_player[name] = "Glenn Maxwell" ,6, dim_player[name] = "Sikandar Raza" ,7, dim_player[name] = "Rashid Khan" ,8, dim_player[name] = "Shadab Khan" ,8, dim_player[name] = "Sam Curran" ,9, dim_player[name] = "Shaheen Shah Afridi" ,10, dim_player[name] = "Anrich Nortje" ,11 ) | dim_player |

## Key Considerations for Dashboard Design

### Color Selection
- Choose primary and/or secondary colors based on the corporate identity or industry.
- Use theme colors for various dashboard elements such as page background, container background, borders, text, etc.

### Font Selection
- Choose fonts based on the identity/industry/subject.
- Determine the size for KPI values, title text, value texts, and paragraph texts.

### Positioning
- Place elements in horizontal/vertical positions in multiples of 8 or 4.
- Maintain proper distances between elements to avoid congestion.
- Stick to aspect ratios to keep visuals appealing.

### Dashboard Creation Steps

1. **Load Data**: Load data into Power BI Desktop from a CSV file.
2. **Data Quality Check**: Use Power Query Editor to check column distribution, quality, and profile.
3. **Error Handling**: Handle errors and empty values in columns.
4. **Report Design**: 
    - Use themes for consistency.
    - Add visual filters (slicers) for Class, Customer Type, Gate Location, and Type of Travel.
    - Create visuals for average delay, customer ratings, and other key metrics.
5. **Text and Image Addition**: Add text boxes with company name and tagline. Insert company logo and other relevant images.
6. **Calculated Columns and Measures**:
    - Create calculated columns and measures for additional insights.
7. **Publish to Power BI Service**: Publish the report to Power BI Service.

## Insights

- **Batting Performance Insights:**
  - Average Runs: The average runs scored by our batsmen is [average runs].
  - Batting Average: The average batting average of our team is [average batting average].
  - Boundary Percentage: [Percentage]% of our team's runs come from boundaries.
  - Strike Rate: Our team has a strike rate of [strike rate].

- **Bowling Performance Insights:**
  - Economy Rate: The average economy rate of our bowlers is [economy rate].
  - Average Bowling Strike Rate: Our bowlers have an average strike rate of [bowling strike rate].
  - Bowling Average: The average bowling average of our team is [bowling average].
  - Dot Ball Percentage: Our bowlers achieve a dot ball percentage of [dot ball percentage].

### Snapshot of Dashboard (Power BI Service)

![dashboard_snapshot](https://github.com/pankajm333/Analystics-All-Stars-/assets/111896613/a3cfa9ac-cf0e-4a87-b542-c93ef9500670)

### Report Snapshot (Power BI DESKTOP)

![report_snapshot](https://github.com/pankajm333/Analystics-All-Stars-/assets/111896613/08f5b416-78fa-4b2c-8c3a-391e85d6d0e1)

ThankYou.
