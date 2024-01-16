# Exploratory Data Analysis of Individual Solver 1 (IS1) Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of my own (Individual Solver 1; IS1) performance on all puzzles issued during a 3+ year (Oct. 2020 - Jan. 2024) sample of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS1 solve times across this period, IS1 performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS1 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), properties of clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and IS1 puzzle day-of-week-specific past performance prior to a given solve. This EDA led to identification of a set of features that hold promise as useful inputs to a predictive model of IS1 future performance.

This project would not have been possible without access to two key data sources. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site (though [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/tree/main/notebooks)). The second, [XWStats](xwstats.com), was my source for historical solve time data (for both IS1 and the GMS).

The same analyses reported here for IS1 here were also carried out for another individual's (IS2) data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2?tab=readme-ov-file#readme).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS1 performance to that of the GMS over the same set of puzzles. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the term "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved over the complete set of puzzles issued between January 1, 2018 and January 13, 2024 (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it's not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS1 performance, however, is tracked by puzzle completion data since I *was* able to obtain completion timestamps for my own solves with Matt's assistance.  

**Figure 1. GMS Solve Time 10-Puzzle Moving Averages and Distributions by Puzzle Day**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/c8408fd1-e509-42ba-a812-c7f0857b9c43)




## Results
### Individual Solver 1 (IS1) Performance Over Time

IS1 solved N = 1,160 puzzles in the sample period: 230 (19.8%) in 2021, 493 (42.5%) in 2022, and 437 (37.7%) in 2023/24 (through Jan. 13, 2024). The total solve time for IS1 was 10.7 days (2021: 2.2 days; 2022: 4.6 days; 2023/24: 3.8 days). The total solve time for the GMS over this same set of puzzles was 14.6 days.     

IS1's 10-puzzle moving averages for each puzzle day (**Figure 2**; top panel) showed considerably more volatility over the IS1 solve period than those of the GMS. **Supplementary Figure 1** shows that this volatility was *not* likely due to chance stretches of puzzles, per-puzzle day, of higher or lower than usual median difficulty (as determined by GMS performance on the same puzzle set). Longer term volatility aside, there was a large amount of improvement in IS1 performance on the more difficult later week puzzle days (Thu-Sun) between early Q2 2023 and the end of the sample period. This improvement can be seen in both the top and bottom panels of **Fig. 2**. Like the GMS, IS1 also became more consistent on early week puzzle days (higher, sharper peaks in the most recent density plot; **Fig. 2** bottom panels), though this trend didn't carry through to the later week puzzle days to the extent that it did for the GMS.    

**Figure 2. 10-Puzzle Solve Time Moving Averages and Distributions by Puzzle Day**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/2150e145-c709-479b-b576-f5cc715beed2)

**Figure 3** shows IS1's solve time performance trajectory in 1-year solve interval violin plots with swarm plot overlays. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve year. Black lines on the violin plots demarcate solve time quartiles per puzzle day. Swarm plot overlays per-puzzle day show individual puzzle raw solve times.**  

**Figure 3. Violin Plots With Swarm Plot Overlay by Puzzle Day**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/cb07aba5-babe-4412-8b75-51782b3ee65a)
*<h5>* 
*<h5>Median[IQR] solve time (m), per puzzle day, per solve year:*<br>
*2021:    Sun: 24.8[22.7-29.0], Mon: 6.2[5.7-6.7], Tue: 7.6[6.8-8.5], Wed: 8.5[7.6-10.7], Thu: 13.5[11.2-16.2], Fri: 14.1[10.9-18.4], Sat: 18.2[12.8-22.0]*<br>
*2022:    Sun: 25.2[22.2-28.8], Mon: 6.1[5.7-6.6], Tue: 7.0[6.4-8.1], Wed: 9.1[7.9-10.6], Thu: 13.5[11.5-16.1], Fri: 13.6[11.5-16.8], Sat: 17.4[14.3-22.5]*<br>
*2023/24: Sun: 21.4[18.4-27.1], Mon: 5.2[4.8-5.7], Tue: 6.2[5.6-7.0], Wed: 8.4[7.1-10.2], Thu: 12.8[10.6-15.8], Fri: 11.4[9.3-15.0], Sat: 15.2[10.8-17.6]*<br>


### Individual Solver 1 (IS1) Performance Vs Global Median Solver (GMS) 

The next series of figures directly compare IS1 solve performance to that of the GMS over the set of all IS1 solves. For these analyses, IS1 solves were broken into two solve date intervals: pre-2023 (n=723; 62.3% of total solves); 2023/24: n=437; 37.7%). Per puzzle day, in the figures relavent to these analyses, pre-2023 solves are represented by lighter-colored points and regression lines and 2023/24 solves by darker-colored ones. 

The next series of figures explicitly compare IS1 solve performance versus that of the GMS over the same set of puzzles. **Figure 4** shows per-puzzle day scatterplots of raw GMSTs (x-axis) versus IS1 solve times (y-axis). Points falling on the dashed diagonal line represent identical raw solve times for IS1 and GMST on a given puzzle, points above and below this line represent "wins" for the GMS and IS1, respectively. Win %s for IS1 were high across puzzle days pre-2023, but increased for the majority of puzzle days in 2023/24. The lowest IS1 win % for both time periods was for Monday puzzles, which aligns with my own sense that the more pure mechanical speed comes into play, the more of a relative disadvantage I am at versus the majority of skilled solvers (though my Mon win rate and mean solve time advantage both did improve substantially in 2023/24). Regression lines show that there was a relatively high degree of correlation in solve times between IS1 and GMST (see the next figure for a recent solver form-normalized take on this), with more of a downward shift away from the dashed diagonal indicating a greater magnitude of performance advantage for IS1 over the GMS. 

**Figure 4. Scatterplots of IS1 vs GMS Solve Performance by Puzzle Day and Solve Interval**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/39bcee3f-5315-41f0-b9b3-aa271953d021)
*<h5> Win Percentage for IS1 vs GMS, by IS1 solve interval:*<br>
*pre-2023: Sun: 96.9, Mon: 64.2, Tue: 89.1, Wed: 88.2, Thu: 91.3, Fri: 90.1, Sat: 89.6*<br>
*2023/24:  Sun: 91.2, Mon: 83.1, Tue: 83.9, Wed: 94.6, Thu: 88.7, Fri: 93.8, Sat: 95.0*<br>

*<h5> Mean(SD) Solve Time Difference (m) for IS1 vs GMS, by IS1 solve period (negative denotes faster for IS1):*<br>
*pre-2023:   Sun: -9.9(6.5), Mon: -.32(1.2), Tue: -1.8(1.7), Wed: -2.7(2.5), Thu: -5.2(4.1), Fri: -5.7(4.5), Sat: -7.3(6.0)*<br>
*2023/24:    Sun: -9.9(6.2), Mon: -.76(0.9), Tue: -1.8(1.6), Wed: -3.2(2.2), Thu: -5.7(4.2), Fri: -6.4(3.5), Sat: -8.2(5.4)*<br>
###
Along with comparison of raw solve performance between IS1 and GMS, the degree to which the same puzzles were *relatively* difficult for the two solvers was addressed. Each IS2 and GMS solve time was taken as a % difference from the solver's respective day-specific 10-puzzle moving average. These 'recent form-normalized' solve times for IS1 and the GMS were then plotted against each other on a per-puzzle day and per-solve period basis (**Figure 5**). Points falling in the lower left (LL; "relatively easy for both solvers") and upper right (UR; "relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. By far the most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (LL), with the second most common outcome being "relatively hard for both solvers" (UR). One reason for the asymmetry between these two quadrants is that it's relatively rare for the solver (either the GMST or individual solver) to solve a new puzzle more slowly than their 10-puzzle moving average, because of relentless improvement in underlying skill. Some of the many puzzles falling outside of the concordant quadrants may be accounted for somewhat trivially via IS1 hitting a ceiling rate of improvement at times on particular puzzle days (e.g., the high UL rates for Mon), and having nowhere to go but relatively slower. But it is highly unlikely that such an effect accounted for the majority of puzzles falling in the "non-concordant" quadrants. Starting in the next section, the focus is on analyses isolating the relationship of factors independent of baseline solver aptitude (ie, "why are there points in those three quadrants?".

**Figure 5. IS1 vs GMS Solve Times as Percentage Difference from 10-Puzzle Moving Average by Puzzle Day and Solve Interval**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/e714448e-3f44-4724-aed2-5b49763c8b1f)
*<h5>Overall, correlations between baseline-normalized IS1 and GMS solve times were moderately-to-strongly positive, with greater strength for most puzzle days in the more recent solve interval.*<br>
*IS1-GMS Correlation (Pearson r) of 10-puzzle moving average-adjusted solve difficulty by IS1 solve interval:*<br>
*pre-2023: Sun: .47, Mon: .38, Tue: .48, Wed: .56, Thu: .53, Fri: .50, Sat: .44*<br>
*2023/24:  Sun: .56, Mon: .38, Tue: .51, Wed: .70, Thu: .57, Fri: .63, Sat: .79*<br>

*<h5> IS1-GMS Quadrant Percentage by IS1 solve period: Lower Left(LL)/Upper Right(UR)/Upper Left(UL)/Lower Right(LR)*<br>
*LL: Relatively Easy for Both IS1 & GMS/ UR: Hard for IS1 & GMS/ UL: Easy for GMS-Hard for IS1/ LR: Easy for IS1-Hard for GMS*<br> 
*pre-2023: Sun: 45.7/21.3/22.3/10.6, Mon: 47.1/16.7/26.5/9.8, Tue: 53.8/17.0/19.8/9.4, Wed: 44.8/17.1/26.7/11.4, Thu: 54.5/21.8/16.8/6.9, Fri: 53.6/18.6/20.6/7.2,<br> Sat: 50.5/18.4/17.5/13.6*<br>
*2023/24:  Sun: 47.7/20.9/20.9/10.4, Mon: 51.8/10.7/23.2/14.3, Tue: 53.6/21.4/19.6/5.4, Wed: 48.2/30.4/12.5/8.9, Thu: 51.6/16.1/19.4/12.9, Fri: 55.7/23.0/19.7/1.6,<br> Sat: 44.6/37.5/14.3/3.6*<br>



### IS1 Performance By Puzzle Constructor(s)

The high proportion of puzzles by repeat individual constructors or specific constructor teams solved by IS1 (72%) afforded the opportunity to evaluate which constructors IS1 tended, in a relative sense, to struggle or do well against. A "mean constructor difficulty" measure (mean % difference from 10-puzzle moving average), normalized both for puzzle day and IS1 baseline solve performance, was computed. **Figure 6** shows heatmapping of IS1 performance against the n=71 constructor(s) contributing >=4 puzzles over the sample period. While only 13% of constructor(s) contributed this many puzzles, this group contributed 39% of all puzzles solved. **Fig. 6** also shows this metric for the GMS on the same set of puzzles for the sake of qualitative comparison. Warmer colors (-%) indicate that the solver solved relatively fast against a given constructor when controlling for day-of-week difficulty and recent solver form; cooler colors (+%) indicate the opposite. "Hot" or "cold" constructors for IS1 tended to also be relatively fast or slow, respectively, for GMS as well. However, there was clearly a substantial degree of discordance in terms of specific order and some constructors (e.g., Brad Wiegmann, Byron Walden, Will Nediger) stood out as being "hot" for one solver but "cold" for the other.

**Figure 6. Heatmapping of IS1 and GMS Performance Against Individual Constructor(s)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/e13a305d-99e6-4632-ae9a-c51ace3f6ab1)

Along with mean normalized performance against given constructor(s) shown in **Fig. 6**, a correlational analysis in the direction of assessing the potential predictive value of past performance against constructor(s) on future performance was performed. **Figure 7** shows the correlation between past performance against a given constructor(s) (x-axis) and performance on the next individual puzzle by that constructor(s) solved (y-axis). This analysis was restricted to only the n=233 puzzles by the constructor(s) included in **Fig. 6** solved *after* >=3 previous puzzles by the same constructor(s) (based on puzzle completion date for IS1, but issue date for GMS). There was a weak-to-moderate positive correlation for IS1, but a substantially stronger one for GMS. It may make sense for the 'typical' solver to have a more reliable relationship with specific constructor(s) than an individual solver, though predictive modeling will say a lot more on this topic. 

**Figure 7. Scatterplots of IS1 and GMS Past Performance Against Individual Constructor(s) Versus 'Next' Individual Puzzle Performance Against the Same Constructor(s)**  
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/aea046e4-9b43-4d98-bf2b-fce214b7e256)
*<h5>The past performance measure on the x-axis was normalized to control for variable puzzle day mix for prior puzzles by given constructor(s). The individual solve time measure on the y-axis was normalized to control for 'recent' puzzle day-specific IS1 (left panel) or GMS (right panel) performance. <br>Pearson correlation coefficient (r): IS1: .11, GMS: .37*

### IS1 Performance by Completion Time of Day

Many external variables are likely to have an impact on individual solver performance, for the large majority of which data collection would be very difficult. Examples include data relevant to how tired, stressed, influenced by substances, or distracted by other sensory stimuli the solver was while working on a given puzzle. One external variable that we *are* fortunate to have data on (thanks, once again, to Matt at XWord Stats) is time of day at puzzle completion. **Figure 8** shows IS1's solve performance by hour of day, overall (black) and by puzzle day (by color). To control for day-specific puzzle difficulty, solve times are expressed as % difference from day-specific 10-puzzle moving averages. IS1 completed most puzzles during the sample period either early in the morning (7-8 AM) or in the evening soon after their release (6 PM ET the evening before for Sun and Mon puzzles; 10 PM ET the evening before for Tue-Sat puzzles). There were no clear trends overall or in specific puzzle days, however for the more difficult puzzle days the small number of fastest solves relative to baseline were in the 10 PM (22:00) hour. Interpretation of this result is difficult because puzzle *start* times were not available. Thus, it can't be distinguished with the available data whether IS1 was a better performer at night or simply finished easier puzzles before bedtime and left harder ones for morning completion.   

**Figure 8. Scatterplots of IS1 Solve Times as Percentage Difference from 10-Puzzle Moving Average by Hour of Completion**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/95021a86-690b-439f-aae3-222e2d540495)


### Correlations of IS1 Performance on Individual Puzzles to Puzzle-Specific Features and Past Performance

Numerous potentially interesting features pertaining to puzzle grids, clues, and answers were obtained from XWord Info across the sample period. Features showing strong correlation to IS1 solve performance become strong candidates as input features for predictive modeling, in current forms and/or when combined in novel ways with other existing features. **Figure 9** shows correlation heatmapping separately for 15x15 puzzles (Mon-Sat) and 21x21 puzzles (Sun) for a subset of all measured features with distributions amenable to linear regression and correlation analysis. Numerous features not selected for this analysis might still be useful in predictive modeling but either had non-continuous distributions (e.g., 0 or 1 for puzzles with normal vs non-standard symmetry) or pertain to a feature that is largely specific to only one or several puzzle days (e.g. Rebuses, Circles, Shaded Squares; see **Supplementary Figures 2-4**). The Pearson correlation coefficient (r) captures linear correlation strength between a given feature and solve times (top row and leftmost column of correlation matrix; red indicates a strong positive correlation and green a strong negative correlation). See **Supplementary Figure 5** for breakdown for IS1 by individual puzzle days for the 15x15 puzzles. As can also be seen in these correlation matrices, a number of grid, clue and answer-related features correlated strongly with each other. For example, 'Mean Answer Length' and 'Freshness Factor' showed a strong negative correlation. This relationship makes intuitive sense because 'Freshness Factor' is a measure of aggregate answer rarity for a given puzzle, and longer answers have a higher likelihood of being uncommon than shorter ones. 

The rightmost column/bottom row per matrix shows the correlation between IS1 solve times for individual puzzles and a puzzle day-specific, time decay-weighted version of the 10-*prior* (to a given puzzle) puzzle moving average. For both 15x15 puzzles and 21x21 puzzles, this (positive) correlation was stronger than any other measured feature correlation to IS1 solve time. This finding generates a prediction that recent (relative to a puzzle date to be predicted) solver form per puzzle day will be more predictive of performance on a novel puzzle than will be any grid or answer (or clue) feature.         

**Figure 9. Correlation Heatmapping of IS1 Individual Puzzle Performance vs Grid, Clue, Answer and Past Performance Features**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/4d71482e-580f-43c1-b370-53c916484ce4)

**Figure 10** through **Figure 21** are companion figures to the correlation heatmapping shown in **Fig. 9**. These figures show, across all 15x15 puzzle days (black) and by-puzzle-day (colored), scatterplots of select features of interest vs IS1 raw solve times at the level of individual puzzles. A feature distribution density plot (FDP) shows puzzle day-specific trends in the distribution of each plotted feature. 

Though most features had at least a moderate correlation strength with IS1 solve times across all 15x15 puzzles, at the by-puzzle-day level these correlations were typically stronger for the more difficult puzzle days (Sat, in particular). It is very likely that the wider ranges of feature values in later week puzzle days (compare per-day widths in the FDPs or x-axis extents in the scatterplots) is related to this finding. There may be threshold values per feature below/above which the feature's effect is not significant in comparison with the effects of solver aptitude (see discussion above about **Fig. 9**, and also see **Fig. 21**). Early week puzzles may also simply not be difficult enough overall for certain features to have an impact on solve times. This is especially true with respect to 'grid features', as they will always necessarily interact with the difficulty of the content of the clue and/or answer.   

Each figure caption for **Figs. 10-21** compares the correlation strength for a given feature for IS1 with that for the global median solver (GMS) over the same set of puzzles. While GMS correlations were uniformly directionally the same as for IS1, they were also uniformly *stronger* than those for IS1. My hunch is that this was related to the more variable per-day baseline sole performance of IS1 relative to the GMS (**see Figs. 1 and 2**). Proving or disproving this hunch will require running the correlations (per solver) against times adjusted for each day-specific 10-puzzle moving average (stay tuned...).       

#### Scatterplots for Individual Features vs IS1 Solve Times, with Associated Feature Distribution Density Plots (FDPs)


#### *Grid Features*

**Figure 10. Number of Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/f98fd6c8-9469-4b58-b0b3-6abc8eb1f3ed)
*<h5>Individual Solver 1 (IS1) solve times and '# Answers' had a moderately strong negative correlation on 15x15 puzzles (r= -.48).<br>
Global Median Solver (GMS) correlation strength on the same set of 15x15 puzzles was considerably stronger (r = -.61).<br>*

*More answers typically meant shorter answers (see correlation matrices above), and shorter answers tended to be more common/easier answers (see 'Average Answer Length' and 'Freshness Factor' analyses below). This correlation strength for IS1, and even the directionality thereof, varied across puzzle days. However, the FDP for this feature shows that the toughest puzzle days (Fri and Sat) tended to have the fewest answers (and the Sat trend mirrored the overall 15x15 trend).*

**<h4>Figure 11. Number of Open Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/91fbf57c-da60-402e-8475-181eecc4abaa)
*<h5>IS1 solve times and '# Open Squares' had a moderately strong positive correlation on 15x15 puzzles (r= .48).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .60).<br>*

*'# Open Squares' is a proprietary measure from XWord Info that counts all white squares that are *not* bordered by black squares. '# Open Squares' was strongly positively correlated to 'Average Answer Length' (see matrices above), so it makes sense that more open squares was also positively correlated with solve times. The IS1 FDP shows that the most difficult puzzle days (Fri and Sat) had a rightward shift in '# Open Squares' relative to the easier 15x15 puzzle days. A large amount of the overall 15x15 correlation for IS1 appears to be accounted for by these more difficult puzzles with large numbers (>~80) of open squares.* 

**<h4>Figure 12. Number of Black Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/d8b635b7-744f-447e-92ec-356486e1e3d1)
*<h5>IS1 solve times and '# Black Squares' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.31).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of moderate correlation (r = -.40).<br>*

*This relationship was essentially the opposite (albeit a weaker form) of that between solve times and '# Open Squares' (more black squares = shorter answers = easier answers). As with '# Open Squares', the correlation was most apparent at the puzzle day level for the Saturday scatterplots for IS1, and Friday and Saturday were prominently shifted away from the earlier week puzzle days in the FDP.*

**<h4>Figure 13. Average Answer Length**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/fcd75129-35b7-41a0-b766-ea6e945281e5)
*<h5>IS1 solve times and 'Average Answer Length' had a moderately strong positive correlation on 15x15 puzzles (r= .57).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .71).<br>*

*This finding was consistent with other grid feature relationships with IS1 solve times, as longer answers means more multiword and relatively-rare answers (see correlation matrices above and **Figs. 17-19**). This correlation was apparent within most of the individual puzzle days (strongest for Sat, as with most of the grid features), and perhaps more so than any other puzzle feature, the sequence in peaks of puzzle day distributions in the FDP tracked with that in mean IS1 solve time by puzzle day. Perhaps this is an indication that this feature will be highly predictive of solve time in the modeling phase??*

**<h4>Figure 14. Number of Cheater Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/b2f8d622-205e-4b46-b868-45d7826a9823)
*<h5>IS1 solve times and '# Cheater Squares' had a weak positive correlation on 15x15 puzzles (r= .19).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .23).<br>*

*Cheater Squares, by definition, are black squares than can be removed without affecting the overall word count of the grid. These squares make construction easier (hence their name), and it can be seen that large numbers of them (say, >10) almost always appear on the difficult puzzle days. Interestingly, within a given puzzle day, however, it's clear that puzzles with larger numbers of them tended to be easier for IS1. So the seeming paradox between the overall 15x15 trend and the individual puzzle day trends is likely related to the competing effects of cheater squares allowing trickier constructions, but also reducing the number of answers and answer lengths overall. Incidentally, the reason they were only rarely seen in odd numbers is the only rarely-violated NYT requirement for grid symmetry.*

#### *Answer and Clue Content Features*
**<h4>Figure 15. Number of Fill-in-the-Blank Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/cfacd65f-9b96-49ed-ba50-a0b4e76d8aef)
*<h5>IS1 solve times and '# Fill-in-the-Blank Answers' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.24).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.27).<br>*

*Taken together, the FDP and scatterplots indicate that most of the strength of this correlation was due to the easiest puzzles (note the rightward FDP peak shift for Mon, even relative to Tue) employing a heavy dose of FITB answers. It will be interesting to see how important this feature is in the modeling phase to prediction of early week solve times, specifically.*

**<h4>Figure 16. Scrabble Average**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/94767623-0470-430f-915b-356394eddf56)
*<h5>IS1 solve times and 'Scrabble Average' had a weak-to-nonexistent negative correlation on 15x15 puzzles (r= -.04).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.05).<br>*

*'Scrabble Average' is another proprietary XWord Info measure, in which each letter in the answer grid is assigned its equivalent value in Scrabble. Since tile values in Scrabble increase with rarity of letter frequency in English texts, it would make sense that a higher value for this feature would be associated with *answers* of greater rarity. If anything, the opposite was true in practice here and as can be seen in the next few figures there are direct measures of answer rarity that *do* have strong positive correlations to solve times. So this one is a candidate to either be left out of predictive modeling entirely or to be combined with other answer rarity/difficulty measures to generate a useful predictive feature.*

**<h4>Figure 17. Number of Scrabble Illegal Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/0510d5fd-6e80-4709-9896-9e6a4ef86eb8)
*<h5>IS1 solve times and '# Scrabble Illegal' had a weak positive correlation on 15x15 puzzles (r= .15).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .18).<br>*

*'# Scrabble Illegal' answers is a proprietary measure of XWord Info that gets at answer rarity more directly than does 'Scrabble Average' (though not as directly as the measures in **Figs. 18 and 19**). Interestingly, this (modest) positive correlation was seen both across all 15x15 puzzles and within each puzzle day (save for Fri). Also interesting is that, apart from a Monday relative leftward shift in the FDP, the distributions for the other 15x15 puzzle days were highly overlapping. I had assumed that the days with more open squares and longer average answers would also have substantially more answers that are not standard English vocabulary words. This finding suggests that more non-standard vocabulary *alone* may not signify or predict puzzle difficulty.*  

**<h4>Figure 18. Number of Unique Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/3d9718b1-98d8-40df-a7ee-78735a5d127a)
*<h5>IS1 solve times and '# Unique Answers' had a weak-to-moderate positive correlation on 15x15 puzzles (r= .35).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of moderate correlation (r = .42).<br>*

*<h5>A unique answer is defined here as one that does not appear in any other NYT crossword puzzle in either the Shortz or pre-Shortz eras (either before or after the puzzle release date). This is perhaps an overly stringent criterion to define answer rarity (see **Fig. 19** for a graded approach to defining answer rarity). Nonetheless, the positive correlation was clearly apparent when considering all 15x15 puzzles together and also especially within the most challenging puzzle day (Sat). It is also clear in the FDP that '# Unique Answers' tended to increase as puzzle day difficulty increased.*

**<h4>Figure 19. Freshness Factor**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/12ee745c-2232-4700-a6bb-b085f95dc3be)
*<h5>IS1 solve times and 'Freshness Factor' had a strong positive correlation on 15x15 puzzles (r= .58).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .72).<br>*

*<h5>'Freshness Factor' is yet another, and very possibly the most useful for solve time prediction(?), proprietary XWord Info measure that assesses the aggregate relative novelty of all answers in a given crossword puzzle as compared to those in all other crossword puzzles in the NYT archive. The much stronger correlation to IS1 (and GMS) solve times as compared to that for '# Unique Answers' suggests that there's much to be gained by taking a graded, as opposed to all-or-none, approach in assessing answer rarity. As with 'Average Answer Length', it can be seen in the FDP that puzzle days peaked in this measure in close concordance with the per-day sequence for solve times.*

**<h4>Figure 20. Number of Wordplay Clues**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/d03dc516-79e5-4417-91d9-93df352c8304)
*<h5>IS1 solve times and '# Wordplay Clues' had a moderate positive correlation on 15x15 puzzles (r= .39).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .49).<br>*

*<h5>'# Wordplay' clues is an admittedly somewhat subjective measure that I have manually evaluated and calculated clue-by-clue across the entire puzzle sample completed by IS1. The FDP for this feature has some interesting properties, including the clear result that later week (Thu, Fri, Sat) puzzles indeed have a larger allocation of 'trickier' clues than early week puzzles. But also of interest is the distinct bimodality for Monday puzzles. Coupled to the positive correlations with IS1 solve times seen in the scatterplots for early week puzzles, there's a suggestion here that this feature may end up being useful in predictive modeling. Interestingly, positive correlations were variably present for the later week puzzle days. This suggests that once puzzles reach a sufficient level of difficulty, clue trickiness may not be as important for influencing solve times (but modeling will provide some answers here).* 

#### *Past Performance Features*

**<h4>Figure 21. GMS Adjusted Recent Performance**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/e9612353-52ef-41f2-b402-0bef3509458a)
*<h5>IS1 solve times and 'GMS Adjusted Recent Performance (GMS-ARP)' had a strong positive correlation on 15x15 puzzles (r= .74).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of very strong correlation (r = .86).<br>*

*<h5>To obtain 'GMS-ARP' for a given puzzle the 10 most recent *prior* puzzles from the same puzzle day were averaged after first being decay weighted (10 for the most recent prior puzzle, 9 for the one before that and so on down to a weight of 1 for the 10th prior puzzle). Recent past performance across all 15x15 puzzles for IS1 (and, to an even larger degree, for GMS) by this measure was more strongly correlated to performance on the "next" puzzle than were the specific characteristics of that puzzle.*

*<h5>Very interestingly, correlation strengths for the early week 15x15 days (Mon-Wed) were higher than those for the later week days (see below in caption). This attests to the relative heterogeneity of later week puzzles, and the likely fact that the likelihood of a solver getting stuck in one particular spot for an extended period of time goes way up. I have zero actual evidence for this, but I will further speculate as an experienced solver that Thursday puzzles have the lowest correlation of all, for both IS1 and the GMS, because they are the most heterogeneous of all puzzle days due to the varied gimmicks and tricks employed. Finally, Saturday correlations for both IS1 and GMS do approach those seen in the early week puzzles. My hunch (again with zero proof) here is that this is at least partially related to a smaller set of constructors, specializing in difficult themeless puzzles (e.g., Byron Walden), being employed for that puzzle day.*

*<h5>Correlation Strength by Puzzle Day:*<br>
*IS1: Sun: .43, Mon: .48, Tue: .41, Wed: .30, Thu: .18, Fri: .28, Sat: .40*<br>
*GMS: Sun: .12, Mon: .39, Tue: .22, Wed: .02, Thu: .01, Fri: .09, Sat: .17*<br>




## Supplementary Figures

**<h4>Supplementary Figure 1. IS1 10-Puzzle Solve Time Moving Averages, Adjusted by GMS Performance by Puzzle Day** 

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/12d757eb-8280-45b5-aca8-fc90e091d2ce)
*<h5>For each puzzle completed by IS1, the percentage difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2**) was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by-chance runs of greater or lesser difficulty per-puzzle day.*

**<h4>Supplementary Figure 2. Scatterplots of Number of Rebus Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/50d0225c-ba28-44b4-8af4-448885d8ee84)
*<h5>Only Sunday and Thursday had an appreciable '# Rebus Squares', which are squares that must be filled with more than one letter, number or symbol for a given puzzle to be solved. There was a modest positive correlation between '# Rebus Squares' for both of these puzzle days (for both IS1 and the GMS), though a caveat is that the very large number of 0 rebus puzzles makes these correlations hard to interpret (ie, these are not exactly continuous distributions).*<br>

*Correlation Strength by Puzzle Day: IS1: Sun: .23, Thu: .21; GMS: Sun: .32, Thu: .16* 

**<h4>Supplementary Figure 3. Scatterplots of Number of Circled Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/19057d5f-ef91-4e2c-bd72-670764da0e2e)
*<h5>Circled squares were virtually non-existent in the tougher (Fri and Sat) puzzles. Their function is to reveal a puzzle theme, and in theory a solver can use this knowledge to "back in" to some full answers. Despite the apparent negative correlation for all 15x15 puzzles, the puzzle days with considerable '# Circles' mostly showed weakly positive correlations. One could speculate here, but it's probably not worth the effort; but there's potential for a small enhancement to modeling on a day-specific basis.*

**<h4>Supplementary Figure 4. Scatterplots of Number of Shaded Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/c9be8ffc-07cf-409f-8c96-00abd70ea88b)
*<h5>Shaded squares, like circled squares, were virtually non-existent in the tougher (Fri and Sat) puzzles. Also like with circled squares, their function is to reveal a puzzle theme and their presence may provide assistance to solvers on clues in which they are embedded. Though most puzzles with shaded squares were within the bottom third of IS1 15x15 puzzle solve times, this is likely mostly due to the fact that they essentially only occured in early week puzzles. As with circles, it can't hurt to include his feature in first-pass modeling and there might be some puzzle day-specific accuracy improvements with its inclusion.* 


**<h4>Supplementary Figure 5. Correlation Heatmapping of IS1 Individual Puzzle Performance vs Grid, Answer and Past-Performance Features by Puzzle Day (15x15 Puzzle Days)**
![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/7a824723-c36b-49b2-ab80-ffae1e9a2888)


