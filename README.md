# Exploratory Data Analysis of Individual Solver 1 Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of my (Individual Solver 1; IS1) own performance on 3+ years (Oct. 2020 - Jan. 2024) of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS1 solve times across this period, IS1 performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS1 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), properties of clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and IS1 puzzle day-of-week specific past performance prior to a given solve. This EDA led to identification of a set of features correlated to my performance thus far that hold promise as useful inputs to a predictive model of my future performance.

This project would not have been possible without access to two key data sources. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site (though [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data. This includes both my own data and data for the GMS. 

### Global Median Solver (GMS)

Several analyses in ths summary compare my (IS1) performance to that of the GMS over the set of puzzles that I have solved. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver#). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the word "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The probable main reasons for this being that the sample does not contain solvers who fail to complete a given puzzle (itself more likely as puzzles get more difficult later in the week), and that the sample contains only solvers motivated enough by the prospect of improvement to track their own progress. 

The GMS has undeniably improved over time (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (January, 2024). Also clear from the 2-year density plots of raw solve time distributions, performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMST is drawn, however, it's not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked by puzzle issue date, as I did not have access to completion dates. It's safe to assume, and Matt concurs, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS1 performance, however, is tracked by puzzle completion data since I was able to obtain completion timestamps for my own solves via XWStats.  

**Figure 1. GMS Solve Time 10-Puzzle Moving Averages and Distributions by Puzzle Day (2-Year Issue Date Interval)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/c8408fd1-e509-42ba-a812-c7f0857b9c43)




## Results
### Individual Solver 1 (IS1) Performance Over Time

IS1 solved N = 1,160 puzzles in the sample period: 230 (19.8%) in 2021, 493 (42.5%) in 2022, and 437 (37.7%) in 2023-2024 (through Jan. 12, 2024). IS1's 10-puzzle moving averages for each puzzle day (**Figure 2**; top panel) had considerably more volatility than those of the GMS. **Supplmentary Figure 1** shows that this volatility is not likely to be due to coincidental cyclical changes in the difficulty of puzzles, as determined by GMS performance on the same puzzle set. Longer term volatility aside, there was a large amount of improvement in IS1 perfomance on the later week (more difficult) puzzle days (Thu-Sun), between early Q2 2023 and the end of the sample period. This improvement can be seen in both the top and bottom panels of **Fig. 2**, as well as in per-solve year violin plots with swarm plot overlay (**Figure 3**). Like the GMS, IS1 also became more consistent on early week puzzle days (higher, sharper peaks in the most recent density plot; **Fig. 2** bottom panels), though this trend didn't carry through to the later week puzzle days as it did for the GMS.    

**Figure 2. 10-Puzzle Solve Time Moving Averages and Distributions by Puzzle Day (1-Year Solve Date Intervals)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/d86506e4-a537-4592-a762-3d0d98a8ddcb)



**Figure 3. Violin Plots With Swarm Plot Overlay by Puzzle Day (1-Year Solve Date Intervals)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/cb07aba5-babe-4412-8b75-51782b3ee65a)
*<h5>Violin plots show both the range (vertical extent) as well as distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve year. Black lines demarcate the quartiles. The swarm plot overlays show individual puzzle raw solve times.* 
*<h5>Median[IQR] solve time (m), per puzzle day, per solve year:*<br>
*2021:    Sun: 24.8[22.7-29.0], Mon: 6.2[5.7-6.7], Tue: 7.6[6.8-8.5], Wed: 8.5[7.6-10.7], Thu: 13.5[11.2-16.2], Fri: 14.1[10.9-18.4], Sat: 18.2[12.8-22.0]*<br>
*2022:    Sun: 25.2[22.2-28.8], Mon: 6.1[5.7-6.6], Tue: 7.0[6.4-8.1], Wed: 9.1[7.9-10.6], Thu: 13.5[11.5-16.1], Fri: 13.6[11.5-16.8], Sat: 17.4[14.3-22.5]*<br>
*2023-24: Sun: 21.4[18.4-27.1], Mon: 5.2[4.8-5.7], Tue: 6.2[5.6-7.0], Wed: 8.4[7.1-10.2], Thu: 12.8[10.6-15.8], Fri: 11.4[9.3-15.0], Sat: 15.2[10.8-17.6]*<br>


### Individual Solver 1 (IS1) Performance Vs Global Median Solver (GMS) 

The next series of figures explicitly compare IS1 solve performance over time versus that of the GMS on the identical set of puzzles. **Figure 4** shows per-puzzle day scatterplots of raw GMSTs (x-axis) versus IS1 solve times (y-axis), broken down by pre (lighter dots) and post-2023 (darker dots) IS1 solve dates. Points falling on the dashed diagonal line represent identical raw solve times for IS1 and GMST on a given puzzle, points above and below this line represent "wins" for the GMS and IS1, respectively. Win %s for IS1 were high across puzzle days pre-2023, but increased for the majority of puzzle days in 2023-2024. The lowest IS1 win % for both time periods was for Monday puzzles, which aligns with my own sense that the more pure mechanical speed comes into play, the more of a relative disadvantage I'm at versus other skilled solvers (though my Mon win rate and mean solve time advantage both did improve substantially in 2023/2024, so there may be hope for me yet). Regression lines show that there is a relatively high degree of correlation in solve times between IS1 and GMST (see the next figure for a recent solver form-normalized take on this), with more of a downward shift away from the dashed diagonal indicating a greater magnitude of performance advantage for IS1 over the GMS. 

**Figure 4. Scatterplots of IS1 vs GMS Solve Performance by Puzzle Day and Solve Period**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/39bcee3f-5315-41f0-b9b3-aa271953d021)
*<h5> Win Percentage for IS1 vs GMS, by IS1 solve period:*<br>
*pre-2023: Sun: 96.9, Mon: 64.2, Tue: 89.1, Wed: 88.2, Thu: 91.3, Fri: 90.1, Sat: 89.6*<br>
*2023-24:  Sun: 91.2, Mon: 83.1, Tue: 83.9, Wed: 94.6, Thu: 88.7, Fri: 93.8, Sat: 95.0*<br>

*<h5> Mean(stdev) Solve Time Difference (m) for IS1 vs GMS, by IS1 solve period (negative denotes faster for IS1):*<br>
*pre-2023:   Sun: -9.9(6.5), Mon: -.32(1.2), Tue: -1.8(1.7), Wed: -2.7(2.5), Thu: -5.2(4.1), Fri: -5.7(4.5), Sat: -7.3(6.0)*<br>
*2023-24:    Sun: -9.9(6.2), Mon: -.76(0.9), Tue: -1.8(1.6), Wed: -3.2(2.2), Thu: -5.7(4.2), Fri: -6.4(3.5), Sat: -8.2(5.4)*<br>
###
Along with absolute performance, the degree to which the same puzzles were *relatively* difficult for IS1 and the GMS on a per-puzzle basis can be addressed. To this end, each solve time for IS1 and GMS was calculated as a % difference from the solver's respective day-specific 10-puzzle moving averages. These 'recent form-normalized' solve times for IS1 and the GMS were then plotted against each other on a per-puzzle day and per-solve period basis (**Figure 5**). Points falling in the lower left (LL; "relatively easy for both solvers") and upper right (UR; "relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. Overall correlations for relative difficulty were moderately or strongly positive, with greater strength for most puzzle days in the more recent period. By far the most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (LL), with the second most common outcome being "relatively hard for both solvers" (UR). One reason for the asymmetry between these two quadrants is that it's relatively rare for the solver (either the GMST or individual solver) to solve a new puzzle more slowly than their 10-puzzle moving average, because of relentless improvement in underlying skill. Nonetheless, there are still a substantial number of puzzles in the quadrants other than LL. Starting in the next section, the focus is on analyses isolating the relationship of factors independent of baseline solver aptitiude (ie, "why are there points in those three quadrants?".

**Figure 5. IS1 vs GMS Solve Times as Percentage Difference from 10-Puzzle Moving Average by Puzzle Day and Solve Period**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/181b1f80-a790-4702-846a-f3177a27687a)
*<h5> IS1-GMS Quadrant Percentage by IS1 solve period: Lower Left(LL)/Upper Right(UR)/Upper Left(UL)/Lower Right(LR)*<br>
*LL: Relatively Easy for Both IS1 & GMS/ UR: Hard for IS1 & GMS/ UL: Easy for GMS-Hard for IS1/ LR: Easy for IS1-Hard for GMS*<br> 
*pre-2023: Sun: 45.7/21.3/22.3/10.6, Mon: 47.1/16.7/26.5/9.8, Tue: 53.8/17.0/19.8/9.4, Wed: 44.8/17.1/26.7/11.4, Thu: 54.5/21.8/16.8/6.9, Fri: 53.6/18.6/20.6/7.2,<br> Sat: 50.5/18.4/17.5/13.6*<br>
*2023-24:  Sun: 47.7/20.9/20.9/10.4, Mon: 51.8/10.7/23.2/14.3, Tue: 53.6/21.4/19.6/5.4, Wed: 48.2/30.4/12.5/8.9, Thu: 51.6/16.1/19.4/12.9, Fri: 55.7/23.0/19.7/1.6,<br> Sat: 44.6/37.5/14.3/3.6*<br>

*IS1-GMS Correlation (Pearson r) of 10-puzzle moving average-adjusted solve difficulty by IS1 solve period:<br>
*pre-2023: Sun: .47, Mon: .38, Tue: .48, Wed: .56, Thu: .53, Fri: .50, Sat: .44*<br>
*2023-24:  Sun: .56, Mon: .38 , Tue: .51 , Wed: .70, Thu: .57, Fri: .63, Sat: .79*<br>

### IS1 Performance By Puzzle Constructor(s)

The high proportion of puzzles by repeat individual constructors or specific constructor teams solved by IS1 (72%) afforded the opportunity to evaluate which constructors IS1 tended to struggle against and which they tended to do relatively well against. A "mean constructor difficulty" measure (mean % difference from 10-puzzle moving average), normalized both for puzzle day and IS1 baseline solve performance, was computed. **Figure 6** shows heatmapping of IS1 performance against the n=71 constructor(s) contributing >=4 puzzles over the sample period. While only 13% of constructor(s) contributed this many puzzles, this group contributed 39% of all puzzles solved. **Fig. 6** also shows this metric for the GMS on the same set of puzzles for the sake of qualitative comparison. Warmer colors (-%) indicate that the solver solves relatively fast against a given constructor when controlling for day-of-week difficulty and recent solver form; cooler colors (+%) indicate the opposite. "Hot" of "cold" constructors for IS1 tended to also be relatively fast or slow, respectively, for GMS as well. However, there was clearly a substantial degree of discordance in terms of specific order and some constructors (e.g., Brad Wiegmann, Byron Walden, Will Nediger) stand out as being "hot" for one solver but "cold" for the other.

Along with mean normalized performance against given constructor(s) shown in **Fig. 6**, a correlational analysis in the direction of assessing the potential predictive value of past performance against constructor(s) on future performance was performed. **Figure 7** shows the correlation between past performance against a given constructor(s) (x-axis) and performance on the next individual puzzle by that constructor(s) (y-axis). This analysis was restricted to only the n=169 puzzles by the constructor(s) included in **Fig. 6** solved *after* >=3 previous puzzles by the same constructor(s) (based on puzzle completion date for IS1, but issue date for GMS). There was a very modest positive correlation for IS1, but a substantially stronger one for GMS. It may make sense for the 'typical' solver to have a more reliable relationship with specific constructor(s) than an indvidual solver, though predictive modeling will say a lot more on this topic. Increasing the threshold of previous puzzles per constructor(s) to even one more puzzle does substantially increase the correlation for IS1 (not shown), so the weakness of this 'predictive' effect for IS1 may be due to a lower than optimal sample size.   

**Figure 6. Heatmapping of IS1 and GMS Performance Against Individual Constructor(s)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/e13a305d-99e6-4632-ae9a-c51ace3f6ab1)





**Figure 7. Scatterplots of IS1 and GMS Past Performance Against Individual Constructor(s) Versus 'Next' Individual Puzzle Performance Against the Same Constructor(s)**  
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/baf16c1f-df1d-4d34-861a-5038a10ab3b0)
*<h5>The past performance measure on the x-axis was normalized to control for variable puzzle day mix for prior puzzles by given constructor(s). The individual solve time measure on the y-axis was normalized to control for 'recent' puzzle day-specific IS1 (left panel) or GMS (right panel) performance. <br>Pearson correlation coefficient (r): IS1: .11, GMS: .40*

### IS1 Performance by Completion Time of Day

Many external variables are likely to have an impact on individual solver performance, for the large majority of which data collection is, at best, impractical. Examples include data relevant to how tired, stressed, influenced by substances, or distracted by other sensory stimuli the solver was while working on a puzzle. One external variable that we *are* fortunate to have data on (thanks, once again, to Matt at XWord Stats) is time of day at puzzle completion. **Figure 8** shows IS1's solve peformance by hour of day, overall (black) and by puzzle day (by color). To control for day-specific puzzle difficulty, solve times are expressed as % difference from day-specific 10-puzzle moving averages. IS1 completed most puzzles during the sample period either early in the morning (7-8 AM) or in the evening soon after their release (6 PM ET the evening before for Sun and Mon puzzles; 10 PM ET the evening before for Tue-Sat puzzles). There are no clear trends overall or in specific puzzle days, however for the more difficult puzzle days the small number of fastest solves relative to baseline were in the 10 PM (22:00) hour. Interpretation of this result is difficult because puzzle *start* times are not available. Thus, it can't be distinguished with te available data whether IS1 is a better performer at night or simply finishes easier puzzles before bedtime and leaves harder ones for morning completion.   

**Figure 8. Scatterplots of IS1 Solve Times as Percentage Difference from 10-Puzzle Moving Average by Hour of Completion**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/95021a86-690b-439f-aae3-222e2d540495)


### Correlations of GMS Performance on Individual Puzzles to Puzzle-Specific Features and Past Performance

Numerous potentially interesting features pertaining to puzzle grids, clues, and answers were obtained from XWord Info across the sample period. Features showing strong correlation to IS1 solve performance become strong candidates as input features for predictive modeling, in current forms and/or when combined in novel ways with other existing features. **Figure 9** shows correlation heatmapping separately for 15x15 puzzles (Mon-Sat) and 21x21 puzzles (Sun) for a subset of all measured features with distributions amenable to linear regression and correlation analysis. Numerous features not selected for this analysis might still be useful in predictive modeling but either have non-continuous distributions (e.g., 0 or 1 for puzzles with normal vs non-standard symmetry) or pertain to a feature that is largely specific to only one or several puzzle days (e.g. Rebuses, Circles, Shaded Squares; see **Supplementary Figures 2-4**). The Pearson correlation coefficient (r) captures linear correlation strength between a given feature and solve times (top row and leftmost column of correlation matrix; red indicates a strong positive correlation and green a strong negative correlation). See **Supplementary Figure 5** for breakdown by individual puzzle days for the 15x15 puzzles. As can also be seen in these correlation matrices, a number of grid, clue and answer-related features correlated strongly with each other. For example, 'Mean Answer Length' and 'Freshness Factor' showed a strong negative correlation. This relationship makes intuitive sense because 'Freshness Factor' is a measure of aggregate answer rarity for a given puzzle, and longer answers have a higher likelihood of being uncommon than shorter ones. 

The rightmost column/bottom row per matrix shows the correlation between IS1 solve times for individual puzzles and a puzzle day-specific, time decay-weighted version of the 10-*prior* (to a given puzzle) puzzle moving average. For both 15x15 puzzles and 21x21 puzzles, this (positive) correlation was stronger than any other measured feature correlation to IS1 solve time. This finding generates a prediction that recent (relative to a puzzle date to be predicted) solver form per puzzle day will be more predictive of performance on a novel puzzle than will be any grid or answer (or clue) feature.         

**Figure 10** through **Figure 21** are companion figures to the correlation heatmapping, and show across all 15x15 puzzle days (black) and by-puzzle-day (colored) scatter plots of features of interest vs raw solve times at the level of individual puzzles (with trend lines indicating aggregate correlation strength). A feature distribution density plot (FDP), per feature, shows puzzle day-specific trends in its distribution. A number of features with strong correlations to IS1 solve time can be seen here to covary with puzzle day. Subsequent predictive modeling outputs will quantify the relative importance of each of these features to puzzle difficulty.

**Figure 9. Correlation Heatmapping of IS1 Individual Puzzle Performance vs Grid, Clue, Answer and Past Performance Features**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/4d71482e-580f-43c1-b370-53c916484ce4)


#### Scatterplots for Individual Features vs IS1 Solve Times, with Associated Feature Distribution Density Plots (FDPs)


#### *Grid Features*

**Figure 8. Number of Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver/assets/90933302/b3f0b390-92db-4605-aaec-d84d022d475c)
*<h5>For 15x15 puzzles, there was a strong negative correlation (r= -0.56) between GMST and '# Answers'. More answers typically meant shorter answers (see correlation matrices above), and shorter answers tended to be be more common/easier answers (see 'Average Answer Length' and 'Freshness Factor' analyses below). The correlation strength, and even the directionality thereof, varied across puzzle days. However, the FDP for this feature shows that the toughest puzzle days (Fri and Sat) tended to have the fewest answers (and the Sat trend mirrored the overall 15x15 trend).*



##
**Supplementary Figure 1. IS1 10-Puzzle Solve Time Moving Averages, Adjusted by GMS Performance, by Puzzle Day** 
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/12d757eb-8280-45b5-aca8-fc90e091d2ce)
*<h5>For each puzzle completed by IS1, the percentage difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2**) was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by-chance runs of greater or lesser difficulty per-puzzle day.*

**<h4>Supplementary Figure 5. Correlation Heatmapping of IS1 Individual Puzzle Performance vs Grid, Answer and Past-Performance Features By Puzzle Day (15x15 Puzzle Days)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/7a824723-c36b-49b2-ab80-ffae1e9a2888)


