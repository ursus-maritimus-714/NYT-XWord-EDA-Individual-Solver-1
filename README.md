# Exploratory Data Analysis of Individual Solver 1 Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of my (Individual Solver 1; IS1) own performance on 3+ years (Oct. 2020 - Jan. 2024) of the [New York Times (NYT) crossword puzzle] (https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS1 solve times across this period, IS1 performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS1 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), properties of clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and IS1 puzzle day-of-week specific past performance prior to a given solve. This EDA led to identification of a set of features correlated to my performance thus far that hold promise as useful inputs to a predictive model of my future performance.

This project would not have been possible without access to two key data sources. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site (though [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data. This includes both my own data and data for the GMS. 

### Global Median Solver (GMS)

Several analyses in ths summary compare my (IS1) performance to that of the GMS over the set of puzzles that I have solved. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver#). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the word "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The probable main reasons for this being that the sample does not contain solvers who fail to complete a given puzzle (itself more likely as puzzles get more difficult later in the week), and that the sample contains only solvers motivated enough by the prospect of improvement to track their own progress. 

The GMS has undeniably improved over time (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (January, 2024). Also clear from the 2-year density plots of raw solve time distributions, performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMST is drawn, however, it's not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked by puzzle issue date, as I did not have access to completion dates. It's safe to assume, and Matt concurs, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS1 performance, however, is tracked by puzzle completion data since I was able to obtain completion timestamps for my own solves via XWStats.  

**Figure 1. Day-of-Week Specific 10-Puzzle Moving Average and Solve Time Distributions (by 2-Year Interval) of GMSTs**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/61320644-8fe7-4b8d-b46c-b69e5bf4cc60)



## Results
### Individual Solver 1 (IS1) Performance Over Time

