# Exploratory Data Analysis of Individual Solver 1 (IS1) Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of my own (Individual Solver 1; IS1) performance on all puzzles issued during a 3+ year (Oct. 2020 - Jan. 2024) sample of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS1 solve times across this period, performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS1 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and puzzle day-specific recent past performance prior to a given solve. This EDA led to identification of a set of features that hold promise as useful inputs to a predictive model of IS1 future performance.

Without access to two specific data sources this project would not have been possible. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site. Nonetheless, [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/tree/main/notebooks). The second, [XWStats](xwstats.com), was my source for historical solve time data for both IS1 and the GMS.

Similar analyses to those reported here for IS1 were performed on another individual's (IS2) data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2?tab=readme-ov-file#readme).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS1 performance to that of the GMS over the set of all IS1 solves. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers of a given puzzle for whom he has (with their consent) acquired their data from NYT. Though Matt adopted the term "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved over the complete set of puzzles (N=2,216) issued between January 1, 2018 and January 25, 2024 (**Figure 1**), with fairly dramatic improvement seen early on for some puzzle days and graded improvement continuing for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it was not possible to disentangle improvement for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance is tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS1 performance, in contrast, is tracked by puzzle completion data since I *was* able to obtain completion timestamps for my own solves with Matt's assistance.  

**Figure 1. GMS Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/8679b7de-30a5-47e1-b0b4-ea865f48c7e5)
*<h5>GMS Final (as of Jan. 25, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 28.8, Mon: 5.7, Tue: 7.7, Wed: 11.4, Thu: 15.1, Fri: 17.8, Sat: 21.1*<br>


## Results
### Individual Solver 1 (IS1) Performance Over Time

IS1 solved N = 1,172 puzzles in the sample period: 230 (19.6%) in 2021, 493 (42.1%) in 2022, and 449 (38.3%) in 2023/24 (through Jan. 25, 2024). The total solve time for IS1 was 10.7 days (2021: 2.2 days; 2022: 4.6 days; 2023/24: 3.9 days). The total solve time for the GMS over this same set of puzzles was 14.7 days.     

IS1's per puzzle day 10-puzzle moving averages across the sample period are shown in **Figure 2** (top panel). Over the full solve period, IS1 had considerably more solve time volatility than did the GMS. **Supplementary Figure 1** shows that the volatility of IS1's per puzzle day solve times was *not* likely due to chance stretches of puzzles with higher or lower than usual median difficulty (as determined by GMS performance on the same puzzle set). Longer term volatility aside, there was a large amount of improvement in IS1 performance on the more difficult later week puzzle days (Thu-Sun) between early Q2 2023 and the end of the sample period. This improvement can be seen in both the top and bottom panels of **Fig. 2**. Like the GMS, IS1 also became more consistent on early week puzzle days (higher, sharper peaks in the most recent density plot; **Fig. 2** bottom panels), though this trend didn't carry through to the later week puzzle days to the extent that it did for the GMS.    

**Figure 2. Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/0474fa5d-8d3d-43af-bf75-f760094a5023)
*<h5>IS1 Final (as of Jan. 25, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 18.7, Mon: 4.7, Tue: 5.7, Wed: 7.4, Thu: 10.9, Fri: 10.6, Sat: 11.6*<br>

###
**Figure 3** shows IS1's solve time performance trajectory in violin plots with swarm plot overlays, broken out by 1-year solve date intervals. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve interval. Black lines on the violin plots demarcate solve time quartiles per puzzle day. Swarm plot overlays per puzzle day show individual puzzle raw solve times.  

**Figure 3. Solve Time Overview by Puzzle Day: Violin Plots With Swarm Plot Overlay**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/ce1241b7-a1eb-4ea4-a88a-1d9e91d8e39d)
*<h5>* 
*<h5>Median[IQR] solve time (m), per puzzle day, per solve year:*<br>
*2021:    Sun: 24.8[22.7-29.0], Mon: 6.2[5.7-6.7], Tue: 7.6[6.8-8.5], Wed: 8.5[7.6-10.7], Thu: 13.5[11.2-16.2], Fri: 14.1[10.9-18.4], Sat: 18.2[12.8-22.0]*<br>
*2022:    Sun: 25.2[22.2-28.8], Mon: 6.1[5.7-6.6], Tue: 7.0[6.4-8.1], Wed: 9.1[7.9-10.6], Thu: 13.5[11.5-16.1], Fri: 13.6[11.5-16.8], Sat: 17.4[14.3-22.5]*<br>
*2023/24: Sun: 20.8[18.3-27.1], Mon: 5.2[4.8-5.7], Tue: 6.2[5.6-6.9], Wed: 8.3[7.1-10.0], Thu: 13.0[10.7-15.8], Fri: 11.4[9.4-14.8], Sat: 15.1[10.9-17.5]*<br>


### Individual Solver 1 (IS1) Performance Vs Global Median Solver (GMS) 

The next series of figures directly compare IS1 solve performance to that of the GMS over the same puzzle set. For these analyses, IS1 solves were broken into two solve intervals: pre-2023 (n=723; 61.9% of total solves); 2023/24: n=445; 38.1%). Per puzzle day, in the figures relevant to these analyses, pre-2023 solves are represented by lighter-colored points and regression lines and 2023/24 solves by darker-colored ones. 

**Figure 4** shows per-puzzle day scatterplots of raw GMSTs (x-axis) versus IS1 solve times (y-axis). Points falling on the dashed diagonal line represent identical raw solve times for IS1 and GMST on a given puzzle, points above and below this line represent "wins" for the GMS and IS1, respectively. Win % across all puzzle days was high pre-2023 (86.7%), but increased even further in the 2023/24 interval (90.6%). In terms of individual puzzle days, IS1's highest win % in the pre-2023 interval was for Sunday (96.9%), but was for Saturday (95.2%) in the 2023/24 interval. The lowest IS1 win % for both time periods was for Monday puzzles (I'm a fat-finger king), though my Monday win rate did improve substantially in 2023/24 (from 63.5% to 84.1%). The mean magnitude of performance advantage for IS1 over the GMST also increased in the more recent solve interval for all puzzle days together (-4.6 to -5.2 minutes), as well as for most individual puzzle days. Finally, per puzzle day regression lines show that there was a relatively high degree of correlation for raw solve times between IS1 and GMST (range across puzzle days and solve intervals: .31-.78). The next figure addresses this correlation in a way that is normalized for recent (prior to a give solve) baseline performance, per solver. 

**Figure 4. IS1 vs GMS: Comparison of Raw Solve Performance by Puzzle Day and Solve Interval**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/1bf7a4ba-80ba-48b8-8e27-359c8ed06a86)
*<h5> Win % for IS1 vs GMS, by IS1 solve interval:*<br>
*pre-2023: All: 86.7, Sun: 96.9, Mon: 63.5, Tue: 88.9, Wed: 88.0, Thu: 91.2, Fri: 90.0, Sat: 89.5*<br>
*2023/24:  All: 90.6, Sun: 91.5, Mon: 84.1, Tue: 85.0, Wed: 95.0, Thu: 89.4, Fri: 94.0, Sat: 95.2*<br>

*<h5> Mean(SD) Solve Time Difference (m) for IS1 vs GMS, by IS1 solve period (negative denotes faster for IS1):*<br>
*pre-2023: All: -4.6(5.2),  Sun: -9.8(6.6), Mon: -.32(1.2), Tue: -1.8(1.7), Wed: -2.7(2.5), Thu: -5.2(4.2), Fri: -5.7(4.6), Sat: -7.3(6.0)*<br>
*2023/24:  All: -5.2(5.0),  Sun: -10.0(6.1), Mon: -.75(.86), Tue: -1.8(1.5), Wed: -3.2(2.2), Thu: -5.6(4.1), Fri: -6.4(3.5), Sat: -8.1(5.3)*<br>
###
Along with comparison of raw solve performance between IS1 and GMS, the degree to which the same puzzles were *relatively* difficult for the two solvers was addressed. Per solver (IS1 or GMS) each raw solve time was taken as a % difference from a decay-time weighted average of the *previous* 10 puzzles solved on the same puzzle day ('Recent Performance Baseline'; RPB). These RPB-adjusted solve times were then plotted against each other on a per puzzle day and per solve period basis (**Figure 5**). Points falling in the lower left ("relatively easy for both solvers") and upper right ("relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. The most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (pre-2023: 41.3%; 2023/24: 39.6%), and the second most common was "relatively hard for both solvers" (pre-2023: 25.2%; 2023/24: 28.7%). It's not surprising that "easy" concordance was more common than "hard" concordance, since solvers constantly improved/outperformed their RPB on a puzzle-to-puzzle basis. A substantial minority (~30%) of puzzles, however, were either relatively easy for IS1 and relatively hard for GMS or vice versa (lower right and upper left quadrants, respectively). This suggests that environmental and puzzle-specific variables may affect different solvers in different ways. Starting in the next section, the focus will be on summarizing the effects of some of these variables on IS1 (and GMS) performance.  

**Figure 5. IS1 vs GMS: Comparison of Baseline-Adjusted Solve Performance by Puzzle Day and Solve Interval**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/b82c2ea9-c70a-46ab-8d8e-bb359bf01f67)
*<h5> IS1-GMS Quadrant Percentage by IS1 solve period: Lower Left(LL)/Upper Right(UR)/Upper Left(UL)/Lower Right(LR)*<br>
*LL: Relatively Easy for Both IS1 & GMS/ UR: Hard for IS1 & GMS/ UL: Easy for GMS-Hard for IS1/ LR: Easy for IS1-Hard for GMS*<br> 
*pre-2023: All: 41.3/25.2/15.5/18.0, Sun: 41.1/31.6/12.6/14.7, Mon: 38.2/22.5/20.6/18.6, Tue: 43.9/25.2/12.1/18.7, Wed: 41.1/25.20/16.8/16.8, Thu: 44.6/27.7/11.9/15.8,<br> Fri: 42.4/21.2/18.2/18.2, Sat: 37.5/23.1/16.3/23.1*<br>
*2023/24:  All: 39.6/28.7/14.3/17.4, Sun: 35.2/28.2/18.3/18.3, Mon: 38.1/23.8/14.3/23.8, Tue: 43.3/21.7/16.7/18.3, Wed: 41.7/33.3/11.7/13.3, Thu: 37.9/22.7/16.7/22.7,<br> Fri: 44.8/31.3/13.4/10.4, Sat: 37.1/40.3/8.1/14.5*<br>

*<h5>Overall, correlations between baseline-normalized IS1 and GMS solve times were moderately-to-strongly positive, with greater strength for each puzzle day in the more recent solve interval.*<br>
*IS1-GMS Correlation (Pearson r) of recent performance baseline(RPB)-adjusted solve difficulty by IS1 solve interval:*<br>
*pre-2023: All: .47, Sun: .46, Mon: .37, Tue: .43, Wed: .55, Thu: .55, Fri: .47, Sat: .43*<br>
*2023/24:  All: .62, Sun: .55, Mon: .47, Tue: .45, Wed: .66, Thu: .59, Fri: .64, Sat: .74*<br>

### IS1 Performance by Puzzle Constructor(s)

A high proportion of puzzles solved by IS1 (72%) were authored by either repeat individual constructors or specific constructor teams (both referred to as "constructor" from here forward). This afforded the opportunity to evaluate which constructors IS1 tended, in a relative sense, to struggle or do well against. Per constructor, the mean of % difference from puzzle day-specific recent performance baseline (RPB; see text section pertaining to **Fig. 5**) was computed. This measure allowed assessment of constructor difficulty adjusted for solver form at the time of a given solve and constructor past puzzle day heterogeneity. **Figure 6** shows heatmapping of IS1 performance, using this normalized measure, against the n=73 constructor(s) contributing >=4 puzzles over the sample period. While only 13% of constructor(s) contributed this many puzzles, this group contributed 40% of all puzzles solved. **Fig. 6** also shows this metric for the GMS on the same set of puzzles for the sake of qualitative comparison. Warmer colors (-%) indicate that the solver solved relatively fast against a given constructor; cooler colors (+%) indicate the opposite. "Hot" or "cold" constructors for IS1 tended to also be relatively fast or slow, respectively, for GMS as well. However, there was clearly a substantial degree of discordance in terms of specific order and some constructors stood out as being either "hot" for IS2 but "cold" for the GMS (e.g., Peter A. Collins, Brad Wiegmann) or vice versa (e.g., Will Nediger, David Tufts).
**Figure 6. Heatmapping of IS1 and GMS Performance Against Individual Constructor**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/e1f2f2d0-4a6e-4520-af6a-737660e1aaf7)

The next correlational analysis was aimed at assessing the potential predictive value of IS1's baseline=adjusted past performance against specific constructors on their future performance against the same constructor. **Figure 7** shows this correlation between IS1 past performance (as mean % difference from RPB) against a given constructor (x-axis) and performance on the next solved individual puzzle by that constructor (y-axis). This analysis was restricted to only the n=239 puzzles by the constructor included in **Fig. 6** that were solved *after* >=3 previous puzzles by the same constructor (based on puzzle completion date for IS1, but issue date for GMS). There was a weak-to-moderate positive correlation for IS1, but a substantially stronger one for GMS. It may make sense for the 'typical' solver to have a more reliable relationship with a specific constructor than an individual solver, though predictive modeling will say a lot more on this topic. 

**Figure 7. IS1 and GMS: Past Performance Against Individual Constructors as "Prediction" of Next Puzzle Performance Against the Same Constructor**  

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/4e387d7d-51b6-4a5d-ba2f-1fa60dbbff6a)
*<h5>Pearson correlation coefficient (r): IS1: .11, GMS: .33*

### IS1 Performance by Completion Time of Day

Many external variables are likely to have an impact on individual solver performance, for the large majority of which data collection would be very difficult. Examples include data relevant to how tired, stressed, influenced by caffeine and other substances, or distracted by other sensory stimuli the solver was while working on a given puzzle. One external variable that we *are* fortunate to have data on (thanks, once again, to Matt at XWord Stats) is time of day at puzzle completion. **Figure 8** shows IS1's solve performance by hour of day, overall (black) and by puzzle day (by color). To control for day-specific puzzle difficulty, solve times are expressed as % difference from puzzle day-specific recent performance baseline (RPB). 

IS1 completed most puzzles during the sample period either early in the morning (7-8 AM; 35% of all solves) or in the evening between 6-10 PM (52% of all solves). The most notable trend in IS1's data in terms of time of completion was that a disproportionate number of "extremely fast" solves (>=50% faster than day-specific RPB) took place in the 10 PM hour. This included 9/77 (11.7%) of solves in the 10 PM hour, but only 30/1091 (2.7%) solves at all other hours. Nonetheless, interpretation of this result is still difficult because puzzle *start* times were not available. Thus, it can't be distinguished with the available data whether IS1 was a better performer at night or simply finished easier puzzles before bedtime and left harder ones for morning completion. To this end, nearly all of the "extremely fast" 10 PM solves were for new Friday or Saturday puzzles released the evening before at exactly 10 PM. An additional caveat is that all solve times were recorded with respect to the US Eastern Time Zone, and there is no indication for puzzles completed in other time zones.        

**Figure 8. Recent Performance Baseline-Adjusted Solve Times by Hour of Completion**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/1f7d224b-d325-4b8b-ad80-8196b0ede6a2)
*<h5>Times are all US Eastern Time Zone, adjusted for Daylight Savings Time as necessary.*

### Correlations of IS1 Performance on Individual Puzzles to Puzzle-Specific Features and Recent Performance

Numerous potentially interesting features pertaining to puzzle grids, clues, and answers were obtained from XWord Info across the sample period. Features showing strong correlation to IS1 solve performance become strong candidates as input features for predictive modeling, in current forms and/or when combined in novel ways with other existing features. **Figure 9** shows correlation heatmapping separately for 15x15 puzzles (Mon-Sat) and 21x21 puzzles (Sun) for a subset of all measured features with distributions amenable to linear regression and correlation analysis (see **Supplementary Figure 2** for individual 15x15 puzzle day matrices). The Pearson correlation coefficient (r) captures linear correlation strength between a given feature and solve times (top row and leftmost column of correlation matrix; red indicates a strong positive correlation and green a strong negative correlation). The rightmost column/bottom row per matrix shows the correlation between IS1 solve times for individual puzzles and puzzle day-specific recent performance baseline (RPB). For both 15x15 puzzles and 21x21 puzzles, this (positive) correlation was stronger than any other measured feature correlation to IS1 solve time. This finding generates a prediction that recent (relative to a puzzle date to be predicted) solver form per puzzle day will be more predictive of performance on a novel puzzle than will be any individual grid, clue or answer feature. 

As can also be seen in the **Fig. 9** correlation matrices, a number of grid, clue and answer-related features correlated strongly with each other. For example, 'Average Answer Length' and 'Freshness Factor' showed a strong negative correlation. This relationship makes intuitive sense because 'Freshness Factor' is a measure of aggregate answer rarity for a given puzzle, and longer answers have a higher likelihood of being uncommon than shorter ones. Additionally, numerous features not selected for this analysis might still be useful in predictive modeling but either had non-continuous distributions (e.g., 0 or 1 for puzzles with normal vs non-standard symmetry) or pertain to a feature that is largely specific to only one or several puzzle days (e.g. Rebuses, Circles, Shaded Squares; see **Supplementary Figures 3-5**).   

**Figure 9. Correlation Heatmapping of IS1 Raw Solve Times vs Grid, Clue, Answer and Past Performance Features**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/e3709a67-826c-4e7f-94c2-078e1692fdd3)
*<h5>Correlation heatmaps derived from N=804 15x15 (left panel) and N=134 21x21 (right panel) puzzles solved by IS1 from 2022-2024.*

*Note on Inclusion Time Range*: As is clear in **Fig. 9**, RPB had the strongest correlation to individual solve times of any feature evaluated by a considerable degree. As such, there was a concern that shifts in baseline solve speed could overwhelm or mask correlations with puzzle-specific features. But normalizing raw solve times (e.g., with RPB) cancels out cross-puzzle day trends that I was interested in identifying prior to the modeling stage. As such, I arrived at a compromise in which I removed all solves from the first solve interval (2021; n=230), which reduced baseline volatility across the solve pool to a considerable degree and allowed me to keep raw solve times as the y-axis variable across these analyses.*

###
**Figure 10** through **Figure 21** are companion figures to the correlation heatmapping shown in **Fig. 9**. These figures show, across all 15x15 puzzle days (black) and by-puzzle-day (colored), scatterplots of select features of interest vs IS1 raw solve times at the level of individual puzzles. A feature distribution density plot (FDP) shows puzzle day-specific trends in the distribution of each plotted feature. 

Though most features had at least a moderate correlation strength with IS1 solve times across all 15x15 puzzles, at the by-puzzle-day level these correlations were typically stronger for the more difficult puzzle days (Sat, in particular). Any feature showing a relatively strong correlation within the late week puzzles days is a strong candidate for having a causal impact on solve times in the modeling phase. Correlations robust enough to show through when many other variables are controlled for within a given puzzle day are likely to have a meaningful impact on solve times. Furthermore, there may be threshold values per feature below/above which that feature's impact is not significant in comparison with the effects of solver aptitude (see discussion above about **Fig. 9**, and also see **Fig. 21**). Because late week puzzle days almost uniformly had considerably wider ranges of feature values than earlier week puzzle days (compare per day widths in the FDPs or x-axis extents in the scatterplots), effects apparent on those late week days would be absent or severely clipped by the limited ranges on the early week days. Finally, early week puzzles may also simply not be difficult enough overall for given features (especially grid features, as a clue is only as difficult as the answer content that it houses) to have discernable impacts on solve times.    

Each figure caption for **Figs. 10-21** compares the correlation strength for a given feature for IS1 with that for the global median solver (GMS) over the same set of puzzles. While GMS correlations were uniformly directionally the same as for IS1, they were also uniformly *stronger* than those for IS1. This relative strength was likely related to the more variable per day baseline solve performance of IS1 relative to the GMS (**see Figs. 1 and 2**), which in turn relates to one being a single human subject to puzzle-to-puzzle variability in many aspects and the other being a "mathematical entity" selected from many individual solvers on a given puzzle for being right in the middle of solve performance on that puzzle.        

#### Scatterplots for Individual Features vs IS1 Solve Times, with Associated Feature Distribution Density Plots (FDPs)


#### *Grid Features*

**Figure 10. Number of Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/8b3d8765-a18d-4a2e-b640-126e91dfc864)
*<h5>Individual Solver 1 (IS1) solve times and '# Answers' had a moderately strong negative correlation on 15x15 puzzles (r= -.48).<br>
Global Median Solver (GMS) correlation strength on the same set of 15x15 puzzles was considerably stronger (r = -.62).<br>*

*More answers typically meant shorter answers (see correlation matrices above), and shorter answers tended to be more common/easier answers (see 'Average Answer Length' and 'Freshness Factor' analyses below). Aligned with this relationship, the FDP for this feature shows that the toughest puzzle days (Fri and Sat) tended to have the fewest answers. The relatively strong *positive* correlations seen for the early week puzzle days (also seen for Mon for IS2 and GMS) suggest that, below a particular per-clue/answer difficulty threshold, merely having to read more clues to solve the puzzle may penalize the solver more they are rewarded for avoiding longer answers.*

**<h4>Figure 11. Number of Open Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/26664f13-c4d1-4672-9ded-1f4836cc72c5)
*<h5>IS1 solve times and '# Open Squares' had a moderately strong positive correlation on 15x15 puzzles (r= .47).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .61).<br>*

*'# Open Squares' is a proprietary measure from XWord Info that counts all white squares that are *not* bordered by black squares. '# Open Squares' was strongly positively correlated to 'Average Answer Length' (see matrices above), so it makes sense that a greater '# Open Squares' was also positively correlated with solve times. The FDP shows that the most difficult puzzle days (Fri and Sat) had a rightward shift in '# Open Squares' relative to the easier 15x15 puzzle days. A large amount of the overall 15x15 correlation for IS1 appears to be accounted for by these more difficult puzzles with large numbers (>~80) of open squares.* 

**<h4>Figure 12. Number of Black Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/4b2b4dd9-956c-4abb-a36f-5233596b87c4)
*<h5>IS1 solve times and '# Black Squares' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.29).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = -.38).<br>*

*This relationship was essentially the opposite (albeit a weaker form) of that between solve times and '# Open Squares' (more black squares = shorter answers = easier answers). Both Friday and Saturday were strongly left-shifted in the FDP, which suggests that most of the overall 15x15 puzzle negative correlation was due to the most difficult days tending to have relatively few black squares. For IS1, the within-puzzle day correlations were variable in both strength and directionality, though the Saturday negative correlation was nearly as strong as the overall 15x15 correlation.*

**<h4>Figure 13. Average Answer Length**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/6eb81340-2819-4d08-b13b-2bfbcd303e74)
*<h5>IS1 solve times and 'Average Answer Length' had a moderately strong positive correlation on 15x15 puzzles (r= .56).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .71).<br>*

*This finding was consistent with other grid feature relationships to IS1 solve times, which makes sense since longer answers meant more multiword and relatively-rare answers (see correlation matrices above and **Figs. 17-19**). This positive correlation was apparent for the majority of the individual puzzle days, and as was typical for grid features for IS1 was strongest for Saturday. As with '# Answers', several early-week puzzle days (particularly Mon) stood out among in showing the reverse correlation sign. Given that these two features are themselves strongly negatively correlated (see **Fig. 10**), it makes sense that early-week puzzle days would again serve as the exception that proves the rule. Longer answers that are still easy may increase solver speed in the aggregate by reducing the amount of clues consumed needed for a solve, without a counterbalancing 'difficulty penalty' that might occur with longer answers on later puzzle days.* 

**<h4>Figure 14. Number of Cheater Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/298be7c2-af89-408e-8552-1b063cb44b53)
*<h5>IS1 solve times and '# Cheater Squares' had a weak positive correlation on 15x15 puzzles (r= .20).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .23).<br>*

*Cheater Squares are black squares than can be removed without affecting the overall word count of the grid. These squares make construction easier (hence their name), and it can be seen in the FDP that large numbers of them (say, >10) almost always appeared on the difficult puzzle days (Fri and Sat). The lack of strong within-day correlations for those more difficult puzzle days, however, makes me skeptical that there's a strong causal impact on solve time. This is in contrast to features like 'Average Answer Length' and '# Open Squares', where there were reasonably strong Saturday correlations in the same direction as the overall 15x15 correlations. Incidentally, the reason cheater squares were only rarely seen in odd numbers is the NYT general requirement for grid symmetry.*


#### *Answer and Clue Content Features*
**<h4>Figure 15. Number of Fill-in-the-Blank Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/c6cf53ca-8b74-4977-bb17-b7c0c9000618)
*<h5>IS1 solve times and '# Fill-in-the-Blank Answers' had a weak-to-moderate negative correlation on 15x15 puzzles (r= -.24).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.26).<br>*

*Taken together, the FDP and scatterplots indicate that most of the strength of this correlation was due to the easiest puzzles (note the rightward FDP peak shift for Mon, even relative to Tue) employing a heavy dose of FITB answers. It's also noteworthy that the most difficult puzzle days (Thu and Fri) clearly made less use of FITB answers than the other puzzle days. It will be interesting to see how important this feature is in the modeling phase to prediction of early week solve times, specifically.*

**<h4>Figure 16. Scrabble Average**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/d7fa4d12-644a-4273-a36c-e817ae13cb5a)
*<h5>IS1 solve times and 'Scrabble Average' had a weak-to-nonexistent negative correlation on 15x15 puzzles (r= -.05).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.07).<br>*

*'Scrabble Average' is another proprietary XWord Info measure, in which each letter in the answer grid is assigned its equivalent value in Scrabble. Since tile values in Scrabble increase with rarity of letter frequency in English texts, it would make sense that a higher value for this feature would be associated with *answers* of greater rarity. If anything, the opposite was true in practice here. Furthermore, as can be seen in the next series of figures, there are direct measures of answer rarity that *do* have strong positive correlations to solve times. So this one is a candidate to either be left out of predictive modeling entirely or to be combined with other answer rarity/difficulty measures to generate a useful predictive feature.*

**<h4>Figure 17. Number of Scrabble Illegal Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/090e245e-5887-432f-a25b-27615d32798f)
*<h5>IS1 solve times and '# Scrabble Illegal' had a weak positive correlation on 15x15 puzzles (r= .13).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .18).<br>*

*'# Scrabble Illegal' answers is a proprietary measure of XWord Info that gets at answer rarity more directly than does 'Scrabble Average' (though not as directly as the measures in **Figs. 18 and 19**). Interestingly, the distributions for 15x15 puzzle days in the FDP were highly overlapping, other than a leftward shift for the easy puzzle days (Mon and Tue) that appears to account for the overall 15x15 puzzles (modest) positive correlation. I had assumed that the days with higher 'Open Squares' and 'Average Answer Length' would also have had substantially proportionally more answers that were not standard English vocabulary words. There were also not discernable trends for correlation strength within the more difficult puzzle days across the range of '# Scrabble Illegal' values. Taken together, these findings suggest that more non-standard vocabulary *alone* may not signify or predict puzzle difficulty.*  

**<h4>Figure 18. Number of Unique Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/ead186e2-32e3-4ee8-8207-e6a66a58632f)
*<h5>IS1 solve times and '# Unique Answers' had a weak-to-moderate positive correlation on 15x15 puzzles (r= .36).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of moderate correlation (r = .42).<br>*

*<h5>A unique answer is defined here as one that does not appear in any other NYT crossword puzzle in either the Shortz or pre-Shortz eras (either before or after the puzzle release date). This is perhaps an overly stringent criterion to define answer rarity (see **Fig. 19** for a graded approach to defining answer rarity). Nonetheless, the positive correlation was clearly apparent when considering all 15x15 puzzles together and also especially within the most challenging puzzle day (Sat). It is also clear in the FDP that '# Unique Answers' tended to increase as puzzle day difficulty increased.*

**<h4>Figure 19. Freshness Factor**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/47a6b53e-9e32-4c86-8ca8-2ab8930966c4)
*<h5>IS1 solve times and 'Freshness Factor' had a strong positive correlation on 15x15 puzzles (r= .57).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .71).<br>*

*<h5>'Freshness Factor' is yet another proprietary XWord Info measure that assesses the aggregate relative novelty of all answers in a given crossword puzzle as compared to those in all other crossword puzzles in the NYT archive. The much stronger correlation to IS1 solve times as compared to that for '# Unique Answers' suggests that there's much to be gained by taking a graded, as opposed to all-or-none, approach in assessing answer rarity.  More so than any other grid, clue or puzzle feature, 15x15 puzzle days peaked in this measure (seen in the FDP) in close concordance with the peaks in the per day sequence for solve times (see **Fig. 2**). The positive correlation was also seen to some degree within each of the individual puzzle days. This finding generates a prediction that, apart from recent puzzle day-specific solver performance prior to a given solve (see **Figure 21**), 'Freshness Factor' will be the most useful feature evaluated in this analysis for predictive modeling of solve performance.*

**<h4>Figure 20. Number of Wordplay Clues**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/099f8e4d-2503-4133-891f-99e2c32787cb)
*<h5>IS1 solve times and '# Wordplay Clues' had a moderate positive correlation on 15x15 puzzles (r= .39).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .49).<br>*

*<h5>'# Wordplay' clues is an admittedly somewhat subjective measure that I have manually evaluated and calculated clue-by-clue across the entire puzzle sample completed by IS1. The FDP for this feature has some interesting properties, including the clear result that later week (Thu, Fri, Sat) puzzles indeed have a larger allocation of 'trickier' clues than early week puzzles. But also of interest is the distinct bimodality for Monday puzzles. Coupled to the positive correlations with IS1 solve times seen in the scatterplots for early week puzzles, there's a suggestion here that this feature may end up being useful in predictive modeling. Interestingly, positive correlations were variably present for the later week puzzle days. This suggests that once puzzles reach a sufficient level of difficulty, clue trickiness may not be as important for influencing solve times (but modeling will provide some answers here).* 

#### *Past Performance Features*

**<h4>Figure 21. IS1 Adjusted Recent Performance**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/32baa7fb-f457-4df1-95f2-d04b99bbb5ba)
*<h5>IS1 solve times and 'Recent Performance Baseline (RPB)' had a strong positive correlation on 15x15 puzzles (r= .74).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of very strong correlation (r = .84).<br>*

*<h5>Correlation strengths for the early week 15x15 days (Mon-Wed) were higher than those for the later week days, and this was also true in the analyses for IS2 and the GMS. This trend likely is related to the relative heterogeneity of later week puzzles, both in terms of tricks/gimmicks employed and also in general difficulty. The lowest puzzle day correlation for both this solver (.14) and the GMS (.37) was for Thursday, arguably the most heterogenous puzzle day of all as there's almost always a gimmick involved (e.g., rebuses of various flavors). Interestingly, Friday and Saturday both had substantially lower correlations for the other individual solver analyzed (IS2) than did Thursday. This finding is an indicaton that effectively modeling individual solver performance, as compared to modeling the 'typical' solver, will be a somewhat bespoke task.*

*<h5>Correlation Strength by Puzzle Day:*<br>
*IS1: Sun: .47, Mon: .51, Tue: .38, Wed: .35, Thu: .14, Fri: .33, Sat: .40*<br>
*GMS: Sun: .63, Mon: .55, Tue: .51, Wed: .45, Thu: .37, Fri: .40, Sat: .40*<br>
*These GMS by-puzzle day correlations are taken from the entire GMS sample in the GMS-specific analysis*



## Supplementary Figures

**<h4>Supplementary Figure 1. IS1 10-Puzzle Solve Time Moving Averages Adjusted by GMS Performance, by Puzzle Day** 

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/42fa6893-7f58-4922-8c09-e29d350974ab)
*<h5>For each puzzle completed by IS1, % difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2**) was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by-chance runs of greater or lesser difficulty per puzzle day.*

**<h4>Supplementary Figure 2. Correlation Heatmapping of IS1 Individual Puzzle Performance vs Grid, Answer and Past-Performance Features by Puzzle Day (15x15 Puzzle Days)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/d0342cfc-b3a9-43dc-9e2d-e66c557a0d79)

**<h4>Supplementary Figure 3. Number of Rebus Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/03bf53f4-534b-40f9-adde-844574e2d983)
*<h5>Only Sunday and Thursday had an appreciable '# Rebus Squares' for IS1 solves. Rebus squares are those that must be filled with more than one letter, number or symbol for a given puzzle to be solved. There was a weak-to-moderate positive correlation between '# Rebus Squares' for both of these puzzle days for both IS1 and the GMS, though a caveat is that the very large number of 0 rebus puzzles makes these correlations hard to interpret (ie, these are not exactly continuous distributions).*<br>

*Correlation Strength by Puzzle Day: IS1: Sun: .26, Thu: .29; GMS: Sun: .34, Thu: .19* 

**<h4>Supplementary Figure 4. Number of Circled Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/a4e0530f-6e6e-4a07-b6e2-324bff966cdb)
*<h5>Circled squares were virtually non-existent in the tougher (Fri and Sat) puzzles. The modest negative correlation seen across all 15x15 puzzle days (-.12) is attributable to the fact that most 15x15 puzzles with circles appeared early in the week. The smattering of puzzles with circles on Sunday almost all fell in the middle of the solve time range regardless of "# Circles", indicating that this feature isn't likely having a major impact on solve times.*

**<h4>Supplementary Figure 5. Number of Shaded Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/cb8f9a52-c802-4fbb-bf86-46f378605327)
*<h5>Shaded squares, like circled squares, were virtually non-existent in the tougher (Fri and Sat) puzzles. Also like with circled squares, their function is to reveal a puzzle theme and their presence may provide assistance to solvers on clues in which they are embedded. Most puzzles with shaded squares were within the bottom third of IS1 15x15 puzzle solve times, most likely due to shaded squares almost exclusively showing up only in early week puzzles. Also as with '# Circles', the smattering of Sunday puzzles almost all fell in the middle of the solve time range regardless of "# Shaded Squares", indicating that this feature also isn't likely having a major impact on solve times.* 






