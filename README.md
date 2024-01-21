# Exploratory Data Analysis of Individual Solver 1 (IS1) Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of my own (Individual Solver 1; IS1) performance on all puzzles issued during a 3+ year (Oct. 2020 - Jan. 2024) sample of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS1 solve times across this period, IS1 performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS1 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), properties of clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and IS1 puzzle day-of-week-specific past performance prior to a given solve. This EDA led to identification of a set of features that hold promise as useful inputs to a predictive model of IS1 future performance.

Without access to two specific data sources this project would not have been possible. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site (though [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data (for both IS1 and the GMS).

Similar analyses to those reported here for IS1 were also carried out for another individual's (IS2) data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2?tab=readme-ov-file#readme).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS1 performance to that of the GMS over the same set of puzzles. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the term "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved over the complete set of puzzles (N=2,211) issued between January 1, 2018 and January 20, 2024 (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it's not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS1 performance, in contrast, is tracked by puzzle completion data since I *was* able to obtain completion timestamps for my own solves with Matt's assistance.  

**Figure 1. GMS Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/4d0b0f9c-75da-4a95-bf6b-0f833a8f67fc)
*<h5>GMS Final (wk of Jan. 15, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 29.9, Mon: 5.7, Tue: 7.8, Wed: 12.0, Thu: 15.6, Fri: 17.8, Sat: 21.0*<br>



## Results
### Individual Solver 1 (IS1) Performance Over Time

IS1 solved N = 1,167 puzzles in the sample period: 230 (19.7%) in 2021, 493 (42.2%) in 2022, and 444 (38.0%) in 2023/24 (through Jan. 13, 2024). The total solve time for IS1 was 10.7 days (2021: 2.2 days; 2022: 4.6 days; 2023/24: 3.9 days). The total solve time for the GMS over this same set of puzzles was 14.7 days.     

IS1's per-puzzle day 10-puzzle moving averages across the sample period are shown in **Figure 2** (top panel). Over the full solve period, IS1 had considerably more solve time volatility than did the GMS. **Supplementary Figure 1** shows that the volatility of IS1's per-puzzle day solve times was *not* likely due to chance stretches of puzzles with higher or lower than usual median difficulty (as determined by GMS performance on the same puzzle set). Longer term volatility aside, there was a large amount of improvement in IS1 performance on the more difficult later week puzzle days (Thu-Sun) between early Q2 2023 and the end of the sample period. This improvement can be seen in both the top and bottom panels of **Fig. 2**. Like the GMS, IS1 also became more consistent on early week puzzle days (higher, sharper peaks in the most recent density plot; **Fig. 2** bottom panels), though this trend didn't carry through to the later week puzzle days to the extent that it did for the GMS.    

**Figure 2. Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/929272ef-d918-404e-a3d8-953a0500892c)
*<h5>IS1 Final (wk of Jan. 15, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 18.4, Mon: 4.6, Tue: 6.0, Wed: 7.5, Thu: 10.8, Fri: 10.6, Sat: 11.6*<br>

###
**Figure 3** shows IS1's solve time performance trajectory in violin plots with swarm plot overlays, broken out by 1-year solve date intervals. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve interval. Black lines on the violin plots demarcate solve time quartiles per puzzle day. Swarm plot overlays per puzzle day show individual puzzle raw solve times.  

**Figure 3. Solve Time Overview by Puzzle Day: Violin Plots With Swarm Plot Overlay**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/a6cd1216-0185-4e68-898f-c97bf26a2c2a)
*<h5>* 
*<h5>Median[IQR] solve time (m), per puzzle day, per solve year:*<br>
*2021:    Sun: 24.8[22.7-29.0], Mon: 6.2[5.7-6.7], Tue: 7.6[6.8-8.5], Wed: 8.5[7.6-10.7], Thu: 13.5[11.2-16.2], Fri: 14.1[10.9-18.4], Sat: 18.2[12.8-22.0]*<br>
*2022:    Sun: 25.2[22.2-28.8], Mon: 6.1[5.7-6.6], Tue: 7.0[6.4-8.1], Wed: 9.1[7.9-10.6], Thu: 13.5[11.5-16.1], Fri: 13.6[11.5-16.8], Sat: 17.4[14.3-22.5]*<br>
*2023/24: Sun: 20.9[18.5-27.1], Mon: 5.2[4.8-5.7], Tue: 6.2[5.6-7.0], Wed: 8.4[7.2-10.1], Thu: 12.8[10.6-15.8], Fri: 11.4[9.4-14.8], Sat: 15.1[10.9-17.5]*<br>


### Individual Solver 1 (IS1) Performance Vs Global Median Solver (GMS) 

The next series of figures directly compare IS1 solve performance to that of the GMS over the same puzzle set. For these analyses, IS1 solves were broken into two solve intervals: pre-2023 (n=723; 62.2% of total solves); 2023/24: n=440; 37.8%). Per puzzle day, in the figures relevant to these analyses, pre-2023 solves are represented by lighter-colored points and regression lines and 2023/24 solves by darker-colored ones. 

**Figure 4** shows per-puzzle day scatterplots of raw GMSTs (x-axis) versus IS1 solve times (y-axis). Points falling on the dashed diagonal line represent identical raw solve times for IS1 and GMST on a given puzzle, points above and below this line represent "wins" for the GMS and IS1, respectively. Win % across all puzzle days was high pre-2023 (86.7%), but increased even further in the 2023/24 interval (90.5%). In terms of individual puzzle days, IS1's highest win % in the pre-2023 interval was for Sunday (96.9%), but was Saturday (95.2%) in the 2023/24 interval. The lowest IS1 win % for both time periods was for Monday puzzles, which aligns with my own sense that the more pure mechanical speed comes into play, the more of a relative disadvantage I am at versus the majority of skilled solvers (though my Mon win rate and mean solve time advantage both did improve substantially in 2023/24, from 63.5% to 83.9%). The per puzzle day regression lines show that there was a relatively high degree of correlation in raw solve times between IS1 and GMST (range across puzzle days and solve intervals: .29-.78). The downward shifts in regression lines away from the dashed diagonal, and the increased magnitude thereof for the more recent solve interval, indicate a greater magnitude of raw performance advantage for IS1 over the GMS. 

**Figure 4. IS1 vs GMS: Comparison of Raw Solve Performance by Puzzle Day and Solve Interval**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/e9e716d8-15dd-4abf-881b-3a4efab65061)
*<h5> Win Percentage for IS1 vs GMS, by IS1 solve interval:*<br>
*pre-2023: Sun: 96.9, Mon: 63.5, Tue: 88.9, Wed: 88.0, Thu: 91.2, Fri: 90.0, Sat: 89.5*<br>
*2023/24:  Sun: 91.4, Mon: 83.9, Tue: 84.7, Wed: 94.9, Thu: 89.2, Fri: 94.0, Sat: 95.2*<br>

*<h5> Mean(SD) Solve Time Difference (m) for IS1 vs GMS, by IS1 solve period (negative denotes faster for IS1):*<br>
*pre-2023:   Sun: -9.8(6.6), Mon: -.32(1.2), Tue: -1.8(1.7), Wed: -2.7(2.5), Thu: -5.2(4.1), Fri: -5.7(4.6), Sat: -7.3(6.0)*<br>
*2023/24:    Sun: -10.0(6.2), Mon: -.76(.87), Tue: -1.8(1.6), Wed: -3.2(2.2), Thu: -5.6(4.1), Fri: -6.4(3.5), Sat: -8.1(5.3)*<br>
###
Along with comparison of raw solve performance between IS1 and GMS, the degree to which the same puzzles were *relatively* difficult for the two solvers was addressed. Per solver (IS1 or GMS) each raw solve time was taken as a % difference from the decay-time weighted average of the *previous* 10 puzzles solved on the same puzzle day ('Recent Performance Baseline'; RPB). These RBP-adjusted solve times were then plotted against each other on a per puzzle day and per solve period basis (**Figure 5**). Points falling in the lower left ("relatively easy for both solvers") and upper right ("relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. The most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (pre-2023: 41.3%; 2023/24: 39.5%), and the second most common was "relatively hard for both solvers" (pre-2023: 25.2%; 2023/24: 28.4%). It's not surprising that "easy" concordance was more common than "hard" concordance, since solvers constantly improved/outperformed their RBP. A considerable minority (>30%) of puzzles, however, were either relatively easy for IS1 and relatively hard for GMS or vice versa (lower right and upper left quadrants, respectively). This suggests that environmental and puzzle-specific variables may affect different solvers in different ways. Starting in the next section, the focus will be on summarizing the effects of some of these variables on IS1 (and GMS) performance.  

**Figure 5. IS2 vs GMS: Comparison of Baseline-Adjusted Solve Performance by Puzzle Day and Solve Interval**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/e305a08e-d6d9-4339-b9a3-8fb856830e74)
*<h5> IS1-GMS Quadrant Percentage by IS1 solve period: Lower Left(LL)/Upper Right(UR)/Upper Left(UL)/Lower Right(LR)*<br>
*LL: Relatively Easy for Both IS1 & GMS/ UR: Hard for IS1 & GMS/ UL: Easy for GMS-Hard for IS1/ LR: Easy for IS1-Hard for GMS*<br> 
*pre-2023: All: 41.3/25.2/15.5/18.0, Sun: 41.1/31.6/12.6/14.7, Mon: 38.2/22.5/20.6/18.6, Tue: 43.9/25.2/12.1/18.7, Wed: 41.1/25.20/16.8/16.8, Thu: 44.6/27.7/11.9/15.8,<br> Fri: 42.4/21.2/18.2/18.2, Sat: 37.5/23.1/16.3/23.1*<br>
*2023/24:  All: 39.5/28.4/14.3/17.7, Sun: 34.3/28.6/18.6/18.6, Mon: 38.7/22.6/14.5/24.2, Tue: 42.4/22.0/17.0/18.6, Wed: 39.7/34.5/12.1/13.8, Thu: 39.1/20.3/17.2/23.4,<br> Fri: 45.5/31.9/12.1/10.6,  Sat: 37.7/39.3/8.2/14.8*<br>

*<h5>Overall, correlations between baseline-normalized IS1 and GMS solve times were moderately-to-strongly positive, with greater strength for most puzzle days in the more recent solve interval.*<br>
*IS1-GMS Correlation (Pearson r) of 10-puzzle moving average-adjusted solve difficulty by IS1 solve interval:*<br>
*pre-2023: All: .47, Sun: .46, Mon: .37, Tue: .43, Wed: .55, Thu: .55, Fri: .47, Sat: .43*<br>
*2023/24:  All: .61, Sun: .55, Mon: .44, Tue: .43, Wed: .64, Thu: .57, Fri: .64, Sat: .74*<br>

### IS1 Performance By Puzzle Constructor(s)

A high proportion of puzzles solved by IS2 (72%) were authored by either repeat individual constructors or specific constructor teams (both referred to as "constructor" from here forward). This afforded the opportunity to evaluate which constructors IS2 tended, in a relative sense, to struggle or do well against. A "mean constructor difficulty" measure (mean % difference from 10-puzzle moving average), normalized both for puzzle day and IS1 baseline solve performance, was computed. **Figure 6** shows heatmapping of IS1 performance against the n=73 constructor(s) contributing >=4 puzzles over the sample period. While only 13% of constructor(s) contributed this many puzzles, this group contributed 39% of all puzzles solved. **Fig. 6** also shows this metric for the GMS on the same set of puzzles for the sake of qualitative comparison. Warmer colors (-%) indicate that the solver solved relatively fast against a given constructor when controlling for day-of-week difficulty and recent solver form (with calculation of mean RPB per constructor; see section above **Fig. 5**); cooler colors (+%) indicate the opposite. "Hot" or "cold" constructors for IS1 tended to also be relatively fast or slow, respectively, for GMS as well. However, there was clearly a substantial degree of discordance in terms of specific order and some constructors (e.g., Peter A. Collins, Brad Wiegmann, Will Nediger, David Tuffs) stood out as being "hot" for one solver but "cold" for the other.

**Figure 6. Heatmapping of IS1 and GMS Performance Against Individual Constructor**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/855c34c0-bb34-4ffe-9223-5e6d437d2f5b)

The next correlational analysis was aimed at assessing the potential predictive value of IS1's past performance against specific constructors on their future performance against the same constructor. **Figure 7** shows this correlation between IS1 past performance against a given constructor (x-axis) and performance on the next individual puzzle by that constructor that was solved (y-axis). This analysis was restricted to only the n=234 puzzles by the constructor(s) included in **Fig. 6** that were solved *after* >=3 previous puzzles by the same constructor (based on puzzle completion date for IS1, but issue date for GMS). There was a weak-to-moderate positive correlation for IS1, but a substantially stronger one for GMS. It may make sense for the 'typical' solver to have a more reliable relationship with specific constructor(s) than an individual solver, though predictive modeling will say a lot more on this topic. 

**Figure 7. IS1 and GMS: Past Performance Against Individual Constructors as "Prediction" of Next Puzzle Performance Against the Same Constructor**  
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/12abdfec-2c60-4c33-a6cd-691c4a63af85)
*<h5>The past performance measure on the x-axis was normalized to control for variable puzzle day mix for prior puzzles by a given constructor. The individual solve time measure on the y-axis was normalized to control for 'recent' puzzle day-specific IS1 (left panel) or GMS (right panel) performance. <br>Pearson correlation coefficient (r): IS1: .11, GMS: .33*

### IS1 Performance by Completion Time of Day

Many external variables are likely to have an impact on individual solver performance, for the large majority of which data collection would be very difficult. Examples include data relevant to how tired, stressed, influenced by substances, or distracted by other sensory stimuli the solver was while working on a given puzzle. One external variable that we *are* fortunate to have data on (thanks, once again, to Matt at XWord Stats) is time of day at puzzle completion. **Figure 8** shows IS1's solve performance by hour of day, overall (black) and by puzzle day (by color). To control for day-specific puzzle difficulty, solve times are expressed as % difference from day-specific 10-puzzle moving averages. IS1 completed most puzzles during the sample period either early in the morning (7-8 AM; 35% of all solves) or in the evening between 6-10 PM (52% of all solves). The most notable trend in IS1's data in terms of time of completion was that a disproportionate number of "extremely fast" solves relative to day-specific baseline (>=50% faster than 10-day moving average) took place in the 10 PM hour. This included 8/77 (10%) of solves in the 10 PM hour, but only 19/1086 (1.7%) solves at all other hours. Nonetheless, interpretation of this result is still difficult because puzzle *start* times were not available. Thus, it can't be distinguished with the available data whether IS1 was a better performer at night or simply finished easier puzzles before bedtime and left harder ones for morning completion. To this end, nearly all of the extremely fast 10 PM solves were for new Friday or Saturday puzzles released the evening before at exactly 10 PM. An additional caveat is that all solve times were recorded with respect to the US Eastern Time Zone, and there is no indication for puzzles completed in other time zones.        

**Figure 8. Baseline-Adjusted Solve Times by Hour of Completion**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/aebdacd2-c356-41f3-b8b5-da72519ff979)
*<h5>Times are all US Eastern Time Zone, adjusted for Daylight Savings Time as necessary.*

### Correlation of IS1 Solve Performance on Individual Puzzles to Recent Puzzle Day-Specific Past Performance

In the next section, I look at the relationship between a number of puzzle grid, clue and answer-related features and IS1 solve performance on individual puzzles. As a benchmark for evaluating those relationships, I evaluated correlation strength between IS1's performance on a given puzzle and recent past performance on puzzles from the same puzzle day. To quantify recent past performance, a puzzle day-specific, time-decay weighted average of solve performance on the *prior* ten puzzles completed ('IS1 Recent Performance') was computed and correlated to the raw solve time on the next puzzle solved for that puzzle day ('IS1 Next Individual Puzzle Performance'). **Figure 9** shows scatterplots of these "predictions" of the next solve time.   

### Correlations of IS1 Performance on Individual Puzzles to Puzzle-Specific Features and Past Performance

Numerous potentially interesting features pertaining to puzzle grids, clues, and answers were obtained from XWord Info across the sample period. Features showing strong correlation to IS1 solve performance become strong candidates as input features for predictive modeling, in current forms and/or when combined in novel ways with other existing features. **Figure 9** shows correlation heatmapping separately for 15x15 puzzles (Mon-Sat) and 21x21 puzzles (Sun) for a subset of all measured features with distributions amenable to linear regression and correlation analysis. Numerous features not selected for this analysis might still be useful in predictive modeling but either had non-continuous distributions (e.g., 0 or 1 for puzzles with normal vs non-standard symmetry) or pertain to a feature that is largely specific to only one or several puzzle days (e.g. Rebuses, Circles, Shaded Squares; see **Supplementary Figures 2-4**). The Pearson correlation coefficient (r) captures linear correlation strength between a given feature and solve times (top row and leftmost column of correlation matrix; red indicates a strong positive correlation and green a strong negative correlation). See **Supplementary Figure 5** for breakdown for IS1 by individual puzzle days for the 15x15 puzzles. As can also be seen in these correlation matrices, a number of grid, clue and answer-related features correlated strongly with each other. For example, 'Average Answer Length' and 'Freshness Factor' showed a strong negative correlation. This relationship makes intuitive sense because 'Freshness Factor' is a measure of aggregate answer rarity for a given puzzle, and longer answers have a higher likelihood of being uncommon than shorter ones. 

The rightmost column/bottom row per matrix shows the correlation between IS1 solve times for individual puzzles and a puzzle day-specific, time decay-weighted version of the 10-*prior* (to a given puzzle) puzzle moving average. For both 15x15 puzzles and 21x21 puzzles, this (positive) correlation was stronger than any other measured feature correlation to IS1 solve time. This finding generates a prediction that recent (relative to a puzzle date to be predicted) solver form per puzzle day will be more predictive of performance on a novel puzzle than will be any individual grid, clue or answer feature.         

**Figure 9. Correlation Heatmapping of IS1 Raw Solve Times vs Grid, Clue, Answer and Past Performance Features**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/f2094338-2ce7-474b-ab2e-fc0fb1ce5549)
*<h5>Correlation heatmaps derived from N=997 15x15 (left panel) and N=166 21x21 (right panel) puzzles solved by IS1.*

###
**Figure 10** through **Figure 21** are companion figures to the correlation heatmapping shown in **Fig. 9**. These figures show, across all 15x15 puzzle days (black) and by-puzzle-day (colored), scatterplots of select features of interest vs IS1 raw solve times at the level of individual puzzles. A feature distribution density plot (FDP) shows puzzle day-specific trends in the distribution of each plotted feature. 

Though most features had at least a moderate correlation strength with IS1 solve times across all 15x15 puzzles, at the by-puzzle-day level these correlations were typically stronger for the more difficult puzzle days (Sat, in particular). It is very likely that the wider ranges of feature values in later week puzzle days (compare per day widths in the FDPs or x-axis extents in the scatterplots) is related to this finding. There may be threshold values per feature below/above which the feature's effect is not significant in comparison with the effects of solver aptitude (see discussion above about **Fig. 9**, and also see **Fig. 21**). Early week puzzles may also simply not be difficult enough overall for certain features to have discernable impacts on solve times. This is especially true with respect to grid features, as they will always necessarily interact with the difficulty of the content of the clue and/or answer contained within.   

Each figure caption for **Figs. 10-21** compares the correlation strength for a given feature for IS1 with that for the global median solver (GMS) over the same set of puzzles. While GMS correlations were uniformly directionally the same as for IS1, they were also uniformly *stronger* than those for IS1. My hunch is that this was related to the more variable per day baseline sole performance of IS1 relative to the GMS (**see Figs. 1 and 2**). Proving or disproving this hunch will require running the correlations (per solver) against times adjusted for each day-specific 10-puzzle moving average (stay tuned...).       

#### Scatterplots for Individual Features vs IS1 Solve Times, with Associated Feature Distribution Density Plots (FDPs)


#### *Grid Features*

**Figure 10. Number of Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/79ee6691-6208-47c6-b6a2-a0f0be09c725)
*<h5>Individual Solver 1 (IS1) solve times and '# Answers' had a moderately strong negative correlation on 15x15 puzzles (r= -.48).<br>
Global Median Solver (GMS) correlation strength on the same set of 15x15 puzzles was considerably stronger (r = -.61).<br>*

*More answers typically meant shorter answers (see correlation matrices above), and shorter answers tended to be more common/easier answers (see 'Average Answer Length' and 'Freshness Factor' analyses below). Aligned with this relationship, the FDP for this feature shows that the toughest puzzle days (Fri and Sat) tended to have the fewest answers. The strong *positive* correlation seen for Monday (also seen for IS2 and GMS), as well as a weaker positive correlation seen for other early-week puzzle days, may be the excepton that proves the rule here. This finding suggests that, below a particular per-clue/answer difficulty threshold, merely having to read more clues to solve the puzzle penalizes the solver more than the solver is rewarded for avoiding longer (but still easy relatively early-in the-week) answers.*

**<h4>Figure 11. Number of Open Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/88b3efa7-a8c5-4760-b883-d3747100feb3)
*<h5>IS1 solve times and '# Open Squares' had a moderately strong positive correlation on 15x15 puzzles (r= .48).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .60).<br>*

*'# Open Squares' is a proprietary measure from XWord Info that counts all white squares that are *not* bordered by black squares. '# Open Squares' was strongly positively correlated to 'Average Answer Length' (see matrices above), so it makes sense that a greater '# Open Squares' was also positively correlated with solve times. The FDP shows that the most difficult puzzle days (Fri and Sat) had a rightward shift in '# Open Squares' relative to the easier 15x15 puzzle days. A large amount of the overall 15x15 correlation for IS1 appears to be accounted for by these more difficult puzzles with large numbers (>~80) of open squares.* 

**<h4>Figure 12. Number of Black Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/09a95693-96f2-408a-9694-36cdd44646fe)
*<h5>IS1 solve times and '# Black Squares' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.31).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of moderate correlation (r = -.40).<br>*

*This relationship was essentially the opposite (albeit a weaker form) of that between solve times and '# Open Squares' (more black squares = shorter answers = easier answers). For IS1, this correlation was consistently apparent across all puzzle days, though with variable strength. The correlation was relatively strong for both Friday and Saturday, which are strongly shifted to the left of the other 15x15 puzzle days in the FDP.*

**<h4>Figure 13. Average Answer Length**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/ae617a78-c410-43e8-8dc8-f9c386a328ac)
*<h5>IS1 solve times and 'Average Answer Length' had a moderately strong positive correlation on 15x15 puzzles (r= .57).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .71).<br>*

*This finding was consistent with other grid feature relationships to IS1 solve times, which makes sense since longer answers meant more multiword and relatively-rare answers (see correlation matrices above and **Figs. 17-19**). This correlation was apparent within most of the individual puzzle days, and was stronger for later week days, as was typical for grid features. As with '# Answers', several early-week puzzle days (particularly Mon) stood out among in showing the reverse correlation sign. Given that these two features are themselves strongly negatively correlated (see **Fig. 10**), it makes sense that early-week puzzle days would again serve as the exception that proves the rule. Longer answers that are still easy may increase solver speed in the aggregate by reducing the amount of clues consumed needed for a solve, without a counterbalancing 'difficulty penalty' that might occur with longer answers on later puzzle days.* 

**<h4>Figure 14. Number of Cheater Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/30078574-067e-476c-bad5-84e0a1038874)
*<h5>IS1 solve times and '# Cheater Squares' had a weak positive correlation on 15x15 puzzles (r= .19).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .23).<br>*

*Cheater Squares are black squares than can be removed without affecting the overall word count of the grid. These squares make construction easier (hence their name), and it can be seen in the FDP that large numbers of them (say, >10) almost always appeared on the difficult puzzle days. Within most puzzle days, it's clear that puzzles with larger numbers of these squares tended to be easier for IS1 (also true for IS2 and the GMS). So the seeming paradox between the overall 15x15 trend and the individual puzzle day trends is likely related to the competing effects on solve times of an increase in '# Cheater Squares' allowing trickier constructions, but also simultaneously reducing '# Answers' and 'Average Answer Length'. Incidentally, the reason cheater squares were only rarely seen in odd numbers is the NYT general requirement for grid symmetry.*


#### *Answer and Clue Content Features*
**<h4>Figure 15. Number of Fill-in-the-Blank Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/fbf543f0-8ecf-4d30-8fa9-9b5903d24d77)
*<h5>IS1 solve times and '# Fill-in-the-Blank Answers' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.24).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.27).<br>*

*Taken together, the FDP and scatterplots indicate that most of the strength of this correlation was due to the easiest puzzles (note the rightward FDP peak shift for Mon, even relative to Tue) employing a heavy dose of FITB answers. It's also noteworthy that the most difficult puzzle days (Thu and Fri) clearly made less use of FITB answers than the other puzzle days. It will be interesting to see how important this feature is in the modeling phase to prediction of early week solve times, specifically.*

**<h4>Figure 16. Scrabble Average**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/0f17fc1c-6b0d-4ca9-9a43-1e64dda563c0)
*<h5>IS1 solve times and 'Scrabble Average' had a weak-to-nonexistent negative correlation on 15x15 puzzles (r= -.04).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.06).<br>*

*'Scrabble Average' is another proprietary XWord Info measure, in which each letter in the answer grid is assigned its equivalent value in Scrabble. Since tile values in Scrabble increase with rarity of letter frequency in English texts, it would make sense that a higher value for this feature would be associated with *answers* of greater rarity. If anything, the opposite was true in practice here. Furthermore, as can be seen in the next series of figures, there are direct measures of answer rarity that *do* have strong positive correlations to solve times. So this one is a candidate to either be left out of predictive modeling entirely or to be combined with other answer rarity/difficulty measures to generate a useful predictive feature.*

**<h4>Figure 17. Number of Scrabble Illegal Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/936199e6-5b78-4a07-8e2d-110135b6bccd)
*<h5>IS1 solve times and '# Scrabble Illegal' had a weak positive correlation on 15x15 puzzles (r= .15).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .19).<br>*

*'# Scrabble Illegal' answers is a proprietary measure of XWord Info that gets at answer rarity more directly than does 'Scrabble Average' (though not as directly as the measures in **Figs. 18 and 19**). Interestingly, this (modest) positive correlation was seen both across all 15x15 puzzles and within each puzzle day (save for Fri). Also interesting is that, apart from a Monday relative leftward shift in the FDP, the distributions for the other 15x15 puzzle days were highly overlapping. I had assumed that the days with more open squares and longer average answers would also have substantially more answers that are not standard English vocabulary words. This finding suggests that more non-standard vocabulary *alone* may not signify or predict puzzle difficulty.*  

**<h4>Figure 18. Number of Unique Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/fc9f538b-c281-4c32-bafe-3eba927621f3)
*<h5>IS1 solve times and '# Unique Answers' had a weak-to-moderate positive correlation on 15x15 puzzles (r= .35).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of moderate correlation (r = .42).<br>*

*<h5>A unique answer is defined here as one that does not appear in any other NYT crossword puzzle in either the Shortz or pre-Shortz eras (either before or after the puzzle release date). This is perhaps an overly stringent criterion to define answer rarity (see **Fig. 19** for a graded approach to defining answer rarity). Nonetheless, the positive correlation was clearly apparent when considering all 15x15 puzzles together and also especially within the most challenging puzzle day (Sat). It is also clear in the FDP that '# Unique Answers' tended to increase as puzzle day difficulty increased.*

**<h4>Figure 19. Freshness Factor**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/c0c7282e-d4b8-4e86-939a-65166fec1b3c)
*<h5>IS1 solve times and 'Freshness Factor' had a strong positive correlation on 15x15 puzzles (r= .58).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .72).<br>*

*<h5>'Freshness Factor' is yet another proprietary XWord Info measure that assesses the aggregate relative novelty of all answers in a given crossword puzzle as compared to those in all other crossword puzzles in the NYT archive. The much stronger correlation to IS1 solve times as compared to that for '# Unique Answers' suggests that there's much to be gained by taking a graded, as opposed to all-or-none, approach in assessing answer rarity.  More so than any other grid, clue or puzzle feature, 15x15 puzzle days peaked in this measure (seen in the FDP) in close concordance with the peaks in the per day sequence for solve times (see **Fig. 2**). This finding generates a prediction that, apart from recent puzzle day-specific solver performance prior to a given solve (see **Figure 21**), 'Freshness Factor' will be the most useful feature evaluated in this analysis for predictive modeling of solve performance.*

**<h4>Figure 20. Number of Wordplay Clues**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/ce0ce028-45a0-43b2-bd9b-52721bc688b1)
*<h5>IS1 solve times and '# Wordplay Clues' had a moderate positive correlation on 15x15 puzzles (r= .39).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .49).<br>*

*<h5>'# Wordplay' clues is an admittedly somewhat subjective measure that I have manually evaluated and calculated clue-by-clue across the entire puzzle sample completed by IS1. The FDP for this feature has some interesting properties, including the clear result that later week (Thu, Fri, Sat) puzzles indeed have a larger allocation of 'trickier' clues than early week puzzles. But also of interest is the distinct bimodality for Monday puzzles. Coupled to the positive correlations with IS1 solve times seen in the scatterplots for early week puzzles, there's a suggestion here that this feature may end up being useful in predictive modeling. Interestingly, positive correlations were variably present for the later week puzzle days. This suggests that once puzzles reach a sufficient level of difficulty, clue trickiness may not be as important for influencing solve times (but modeling will provide some answers here).* 

#### *Past Performance Features*

**<h4>Figure 21. IS1 Adjusted Recent Performance**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/83442ce0-8b0c-44b5-8323-2e9d73a5896b)
*<h5>IS1 solve times and 'GMS Adjusted Recent Performance (GMS-ARP)' had a strong positive correlation on 15x15 puzzles (r= .74).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of very strong correlation (r = .86).<br>*

*<h5>Correlation strengths for the early week 15x15 days (Mon-Wed) were higher than those for the later week days, and this was also true in the analyses for IS1 and the GMS. This trend likely is related to the relative heterogeneity of later week puzzles, both in terms of tricks/gimmicks employed and also in general difficulty. The lowest puzzle day correlation for both this solver and the GMS and IS1 was for Thursday, arguably the most heterogenous puzzle day of all as there's almost always a gimmick involved (e.g., rebuses of various flavors). Interestingly, Friday and Saturday both had substantially lower correlations for the other individual solver analyzed (IS2) than did Thursday. This is another indicaton that optimally modeling individual solver performance, as compared to modeling the 'typical' solver, will be a somewhat bespoke task.*

*<h5>Correlation Strength by Puzzle Day:*<br>
*IS1: Sun: .43, Mon: .49, Tue: .42, Wed: .30, Thu: .19, Fri: .29, Sat: .40*<br>
*GMS: Sun: .62, Mon: .54, Tue: .51, Wed: .44, Thu: .37, Fri: .40, Sat: .39*<br>
*These GMS by-puzzle day correlations are taken from the entire GMS sample in the GMS-specific analysis*



## Supplementary Figures


**<h4>Supplementary Figure 1. IS2 10-Puzzle Solve Time Moving Averages Adjusted by GMS Performance, by Puzzle Day** 
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/ff6e1f9b-4105-4d5f-a787-edd4b72311a8)
*<h5>For each puzzle completed by IS1, % difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2**) was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by-chance runs of greater or lesser difficulty per puzzle day.*

**<h4>Supplementary Figure 2. Number of Rebus Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/13a4d05e-cdcd-43f3-b767-3e012ae6feb2)
*<h5>Only Sunday and Thursday had an appreciable '# Rebus Squares' for IS1 solves. Rebus squares are those that must be filled with more than one letter, number or symbol for a given puzzle to be solved. There was a modest positive correlation between '# Rebus Squares' for both of these puzzle days (for both IS1 and the GMS), though a caveat is that the very large number of 0 rebus puzzles makes these correlations hard to interpret (ie, these are not exactly continuous distributions).*<br>

*Correlation Strength by Puzzle Day: IS1: Sun: .23, Thu: .21; GMS: Sun: .33, Thu: .16* 

**<h4>Supplementary Figure 3. Number of Circled Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/20c01532-2187-43d9-b082-27f16de9b16b)
*<h5>Circled squares were virtually non-existent in the tougher (Fri and Sat) puzzles. Their function is to reveal a puzzle theme, and in theory a solver can use this knowledge to "back in" to some full answers. Despite the apparent negative correlation for all 15x15 puzzles, the puzzle days with considerable '# Circles' mostly showed weakly positive correlations. One could speculate here, but it's probably not worth the effort; but there's potential for a small enhancement to modeling on a day-specific basis.*

**<h4>Supplementary Figure 4. Number of Shaded Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/ba86fbcf-fe07-411f-a990-c342068a8933)
*<h5>Shaded squares, like circled squares, were virtually non-existent in the tougher (Fri and Sat) puzzles. Also like with circled squares, their function is to reveal a puzzle theme and their presence may provide assistance to solvers on clues in which they are embedded. Though most puzzles with shaded squares were within the bottom third of IS1 15x15 puzzle solve times, this is likely mostly due to the fact that they essentially only occured in early week puzzles. As with circles, it can't hurt to include his feature in first-pass modeling and there might be some puzzle day-specific accuracy improvements with its inclusion.* 


**<h4>Supplementary Figure 5. Correlation Heatmapping of IS1 Individual Puzzle Performance vs Grid, Answer and Past-Performance Features by Puzzle Day (15x15 Puzzle Days)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/7a824723-c36b-49b2-ab80-ffae1e9a2888)


