# Exploratory Data Analysis of Individual Solver 1 Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of my (Individual Solver 1; IS1) own performance on 3+ years (Oct. 2020 - Jan. 2024) of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS1 solve times across this period, IS1 performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS1 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), properties of clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and IS1 puzzle day-of-week specific past performance prior to a given solve. This EDA led to identification of a set of features correlated to my performance thus far that hold promise as useful inputs to a predictive model of my future performance.

This project would not have been possible without access to two key data sources. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site (though [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data. This includes both my own data and data for the GMS. 

### Global Median Solver (GMS)

Several analyses in ths summary compare my (IS1) performance to that of the GMS over the set of puzzles that I have solved. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver#). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the word "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The probable main reasons for this being that the sample does not contain solvers who fail to complete a given puzzle (itself more likely as puzzles get more difficult later in the week), and that the sample contains only solvers motivated enough by the prospect of improvement to track their own progress. 

The GMS has undeniably improved over time (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (January, 2024). Also clear from the 2-year density plots of raw solve time distributions, performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMST is drawn, however, it's not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked by puzzle issue date, as I did not have access to completion dates. It's safe to assume, and Matt concurs, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS1 performance, however, is tracked by puzzle completion data since I was able to obtain completion timestamps for my own solves via XWStats.  

**Figure 1. Day-of-Week Specific 10-Puzzle Moving Average and Solve Time Distributions (by 2-Year Interval) for GMS**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/61320644-8fe7-4b8d-b46c-b69e5bf4cc60)



## Results
### Individual Solver 1 (IS1) Performance Over Time

IS1 solved N = 1,157 puzzles in the sample period: 230 (19.9%) in 2021, 493 (42.6%) in 2022, and 434 (37.8%) in 2023-2024 (through Jan. 10). IS1's solve profile over time has considerably more volatility than that of the GMS. **Supplmentary Figure 1** shows that this volatility is not likely to be due to coincidental cyclical changes in the difficulty of puzzles, as determined by GMS performance on the same puzzle set. Longer term volatility aside, there was a large amount of improvement in IS1 perfomance on the more difficult later week puzzle days (Thu-Sun), between early Q2 2023 and the end of the sample period. This improvement can be seen in both the top and bottom panels of **Figure 2**. Like the GMS, IS1 also has become more consistent on early week puzzle days (higher, sharper peaks in the most recent density plot), though this doesn't carry through to the later week puzzle days as it does with the GMS.    

**Figure 2. Day-of-Week Specific 10-Puzzle Moving Average and Solve Time Distributions (by 1-Year Interval)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/566ee85d-57e9-45e3-8515-d395df08e84a)
*Median[IQR] solve time (m), per puzzle day, per solve year:* 

*2021- Sun:24.8[22.7-29.0], Mon:6.2[5.7-6.7], Tue:7.6[6.8-8.5], Wed:8.5[7.6-10.7], Thu:13.5[11.2-16.2], Fri:14.1[10.9-18.4], Sat:18.2[12.8-22.0]*

*2022- Sun: 25.2[22.2-28.8], Mon: 6.1[5.7-6.6], Tue: 7.0[6.4-8.1], Wed: 9.1[7.9-10.6], Thu: 13.5[11.5-16.1], Fri: 13.6[11.5-16.8], Sat: 17.4[14.3-22.5]*

*2023+- Sun: 21.4[18.4-27.1], Mon: 5.2[4.8-5.7], Tue: 6.2[5.6-7.0], Wed: 8.4[7.1-10.2], Thu: 12.8[10.8-15.8], Fri: 11.4[9.4-15.3], Sat: 15.3[11.0-17.6]*  




**Supplementary Figure 1. Day-of-Week Specific 10-Puzzle Moving Average for IS1, Adjusted by GMS Performance Over the Same Puzzle Set** 
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/db598abf-f191-4d75-b4ff-eb03b1f1d8f9)
*For each puzzle completed by IS1, the percentage difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see Figure 2) is still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by-chance runs of greater or lesser difficulty per puzzle day.*
