# Exploratory Data Analysis of Individual Solver 1 Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of my (Individual Solver 1; IS1) own performance on 3+ years (Oct. 2020 - Jan. 2024) of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS1 solve times across this period, IS1 performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS1 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), properties of clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and IS1 puzzle day-of-week specific past performance prior to a given solve. This EDA led to identification of a set of features correlated to my performance thus far that hold promise as useful inputs to a predictive model of my future performance.

This project would not have been possible without access to two key data sources. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site (though [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data. This includes both my own data and data for the GMS. 

### Global Median Solver (GMS)

Several analyses in ths summary compare my (IS1) performance to that of the GMS over the set of puzzles that I have solved. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver#). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the word "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The probable main reasons for this being that the sample does not contain solvers who fail to complete a given puzzle (itself more likely as puzzles get more difficult later in the week), and that the sample contains only solvers motivated enough by the prospect of improvement to track their own progress. 

The GMS has undeniably improved over time (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (January, 2024). Also clear from the 2-year density plots of raw solve time distributions, performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMST is drawn, however, it's not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked by puzzle issue date, as I did not have access to completion dates. It's safe to assume, and Matt concurs, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS1 performance, however, is tracked by puzzle completion data since I was able to obtain completion timestamps for my own solves via XWStats.  

**Figure 1. GMS Solve Time 10-Puzzle Moving Averages and Distributions by Puzzle Day (2-Year Issue Date Interval)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/22848cd8-d80d-45da-a5e3-2313d28e2df5)




## Results
### Individual Solver 1 (IS1) Performance Over Time

IS1 solved N = 1,159 puzzles in the sample period: 230 (19.8%) in 2021, 493 (42.5%) in 2022, and 436 (37.6%) in 2023-2024 (through Jan. 12, 2024). IS1's 10-puzzle moving averages for each puzzle day (**Figure 2**; top panel) had considerably more volatility than those of the GMS. **Supplmentary Figure 1** shows that this volatility is not likely to be due to coincidental cyclical changes in the difficulty of puzzles, as determined by GMS performance on the same puzzle set. Longer term volatility aside, there was a large amount of improvement in IS1 perfomance on the later week (more difficult) puzzle days (Thu-Sun), between early Q2 2023 and the end of the sample period. This improvement can be seen in both the top and bottom panels of **Fig. 2**, as well as in per-solve year violin plots with swarm plot overlay (**Figure 3**). Like the GMS, IS1 also became more consistent on early week puzzle days (higher, sharper peaks in the most recent density plot; **Fig. 2** bottom panels), though this trend didn't carry through to the later week puzzle days as it did for the GMS.    

**Figure 2. 10-Puzzle Solve Time Moving Averages and Distributions by Puzzle Day (1-Year Solve Date Intervals)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/e442b107-a7d9-4060-b61a-c5f5beec0431)


**Figure 3. Violin Plots With Swarm Plot Overlay by Puzzle Day (1-Year Solve Date Intervals)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/d8bc6531-14d0-4837-9be7-480f1b33574c)
*<h5>Violin plots show both the range (vertical extent) as well as distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve year. Black lines demarcate the quartiles. The swarm plot overlays show individual puzzle raw solve times.* 
*<h5>Median[IQR] solve time (m), per puzzle day, per solve year:*<br>
*2021:    Sun: 24.8[22.7-29.0], Mon: 6.2[5.7-6.7], Tue: 7.6[6.8-8.5], Wed: 8.5[7.6-10.7], Thu: 13.5[11.2-16.2], Fri: 14.1[10.9-18.4], Sat: 18.2[12.8-22.0]*<br>
*2022:    Sun: 25.2[22.2-28.8], Mon: 6.1[5.7-6.6], Tue: 7.0[6.4-8.1], Wed: 9.1[7.9-10.6], Thu: 13.5[11.5-16.1], Fri: 13.6[11.5-16.8], Sat: 17.4[14.3-22.5]*<br>
*2023-24: Sun: 21.4[18.4-27.1], Mon: 5.2[4.8-5.7], Tue: 6.2[5.6-7.0], Wed: 8.4[7.1-10.2], Thu: 12.8[10.6-15.8], Fri: 11.4[9.3-15.0], Sat: 15.3[11.0-17.6]*<br>


### Individual Solver 1 (IS1) Performance Vs Global Median Solver (GMS) 

The next series of figures explicitly compare IS1 solve performance over time versus that of the GMS on the identical set of puzzles. **Figure 4** shows per-puzzle day scatterplots of raw GMSTs (x-axis) versus IS1 solve times (y-axis), broken down by pre (lighter dots) and post-2023 (darker dots) IS1 solve dates. Points falling on the dashed diagonal line represent identical raw solve times for IS1 and GMST on a given puzzle, points above and below this line represent "wins" for the GMS and IS1, respectively. Win %s for IS1 were high across puzzle days pre-2023, but increased for the majority of puzzle days in 2023-2024. The lowest IS1 win % for both time periods was for Monday puzzles, which aligns with my own sense that the more pure mechanical speed comes into play, the more of a relative disadvantage I'm at versus other skilled solvers (though my Mon win rate and mean solve time advantage both did improve substantially in 2023/2024, so there may be hope for me yet). Regression lines show that there is a relatively high degree of correlation in solve times between IS1 and GMST (see the next figure for a recent solver form-normalized take on this), with more of a downward shift away from the dashed diagonal indicating a greater magnitude of performance advantage for IS1 over the GMS. 

**Figure 4. Scatterplots of IS1 vs GMS Solve Performance by Puzzle Day and Solve Period**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/89f94136-ac21-4a84-baf7-bae6fc2673a1)
*<h5> Win Percentage for IS1 vs GMS, by IS1 solve period:*<br>
*pre-2023: Sun: 96.9, Mon: 64.2, Tue: 89.1, Wed: 88.2, Thu: 91.3, Fri: 90.1, Sat: 89.6*<br>
*2023-24:  Sun: 91.2, Mon: 83.1, Tue: 83.9, Wed: 94.6, Thu: 88.7, Fri: 93.8, Sat: 95.0*<br>

*<h5> Mean(stdev) Solve Time Difference (m) for IS1 vs GMS, by IS1 solve period (negative denotes faster for IS1):*<br>
*pre-2023:   Sun: -9.9(6.5), Mon: -.32(1.2), Tue: -1.8(1.7), Wed: -2.7(2.5), Thu: -5.2(4.1), Fri: -5.7(4.5), Sat: -7.3(6.0)*<br>
*2023-24:    Sun: -9.9(6.2), Mon: -.76(0.9), Tue: -1.8(1.6), Wed: -3.2(2.2), Thu: -5.7(4.2), Fri: -6.4(3.5), Sat: -8.2(5.4)*<br>
###
Along with absolute performance, the degree to which the same puzzles were *relatively* difficult for IS1 and the GMS on a per-puzzle basis can be addressed. To this end, each solve time for IS1 and GMS was calculated as a % difference from the solver's respective day-specific 10-puzzle moving averages. These 'recent form-normalized' solve times for IS1 and the GMS were then plotted against each other on a per-puzzle day and per-solve period basis (**Figure 5**). Points falling in the lower left (LL; "relatively easy for both solvers") and upper right (UR; "relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. Overall correlations for relative difficulty were moderately or strongly positive, with greater strength for most puzzle days in the more recent period. By far the most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (LL), with the second most common outcome being "relatively hard for both solvers" (UR). One reason for the asymmetry between these two quadrants is that it's relatively rare for the solver (either the GMST or individual solver) to solve a new puzzle more slowly than their 10-puzzle moving average, because of relentless improvement in underlying skill. Nonetheless, there are still a substantial number of puzzles in the quadrants other than LL. Starting in the next section, the focus is on analyses isolating the relationship of factors independent of baseline solver aptitiude (ie, "why are there points in those three quadrants?".

**Figure 5. IS1 vs GMS Raw Solve Times as Percentage of 10-Puzzle Moving Average by Puzzle Day and Solve Period**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/f7d91dbc-da37-4b07-b194-bb19c088aac2)
*<h5> IS1-GMS Quadrant Percentage by IS1 solve period: Lower Left(LL)/Upper Right(UR)/Upper Left(UL)/Lower Right(LR)*<br>
*LL: Relatively Easy for Both IS1 & GMS/ UR: Hard for IS1 & GMS/ UL: Easy for GMS-Hard for IS1/ LR: Easy for IS1-Hard for GMS*<br> 
*pre-2023: Sun: 45.7/21.3/22.3/10.6, Mon: 47.1/16.7/26.5/9.8, Tue: 53.8/17.0/19.8/9.4, Wed: 44.8/17.1/26.7/11.4, Thu: 54.5/21.8/16.8/6.9, Fri: 53.6/18.6/20.6/7.2,<br> Sat: 50.5/18.4/17.5/13.6*<br>
*2023-24:  Sun: 47.7/20.9/20.9/10.4, Mon: 51.8/10.7/23.2/14.3, Tue: 53.6/21.4/19.6/5.4, Wed: 48.2/30.4/12.5/8.9, Thu: 51.6/16.1/19.4/12.9, Fri: 55.7/23.0/19.7/1.6,<br> Sat: 44.6/37.5/14.3/3.6*<br>

*IS1-GMS Correlation (Pearson r) of 10-puzzle moving average-adjusted solve difficulty by IS1 solve period:<br>
*pre-2023: Sun: .47, Mon: .38, Tue: .48, Wed: .56, Thu: .53, Fri: .50, Sat: .44*<br>
*2023-24:  Sun: .56, Mon: .38 , Tue: .51 , Wed: .70, Thu: .57, Fri: .63, Sat: .79*<br>



##
**Supplementary Figure 1. IS1 10-Puzzle Solve Time Moving Averages, Adjusted by GMS Performance, by Puzzle Day** 
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/a2257f76-ba3d-4b3b-bf10-c845ab29bdb3)
*<h5>For each puzzle completed by IS1, the percentage difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see Fig. 2) was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by-chance runs of greater or lesser difficulty per-puzzle day.*

