# Exploratory Data Analysis of Individual Solver 1 (IS1) Performance on the New York Times Crossword Puzzle
 
 ## Introduction

### Project Overview
This summary reports on exploratory data analysis (EDA) of my own (Individual Solver 1; IS1) performance on all puzzles issued during a 3+ year (Oct. 2020 - Jan. 2024) sample of the [New York Times (NYT) crossword puzzle](https://www.nytimes.com/crosswords). Included are visual and statistical descriptions of trends in IS1 solve times across this period, performance relative to the 'Global Median Solver' (GMS; see next section), and the relationship between IS1 performance and a number of variables. These variables included properties of the puzzle grids (e.g., number of answers, number of black squares), clues and answers (e.g., frequency of wordplay in clues, aggregate rarity of answers in a puzzle), environment (e.g., time of day a puzzle was completed), constructor identity, and puzzle day-specific recent past performance prior to a given solve. This EDA led to identification of a set of features that hold promise as useful inputs to a predictive model of IS1 future performance.

Without access to two specific data sources this project would not have been possible. The first, [XWord Info: New York Times Crossword Answers and Insights](https://www.xwordinfo.com/), was my source for data on the puzzles themselves. This included a number of proprietary metrics pertaining to the grids, answers, clues and constructors. XWord Info has a contract with NYT for access to the raw data underlying these metrics, but I unfortunately do not. Therefore, I will not be able to share raw or processed data that I've acquired from their site. Nonetheless, [Jupyter notebooks](https://jupyter.org/) with all of my Python code for analysis and figure generation can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/tree/main/notebooks). The second, [XWStats](xwstats.com), was my source for historical solve time data for both IS1 and the GMS.

Similar analyses to those reported here for IS1 were performed on another individual's (IS2) data over a comparable sample size and timespan, and are summarized [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-2?tab=readme-ov-file#readme).

### The Global Median Solver (GMS)

Many analyses included in this summary compare IS1 performance to that of the GMS over the set of all IS1 solves. My extensive summary analysis of GMS performance over a 6+ year timeframe (2018-2024) can be found [here](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Global-Median-Solver?tab=readme-ov-file#readme). XWStats (Matt) determines the global median solve time (GMST) for every individual puzzle from a pool of ~1-2K individual solvers from whom he has (with their consent) acquired personal solve data, via NYT. Though Matt adopted the term "global" to describe this solver sample per-puzzle, it likely skews faster than the overall population of solvers. The reasons for this assumption are twofold; only solvers who actually complete a given puzzle are included in its sample, and each sample contains only solvers motivated enough by the prospect of improvement to track their own progress to begin with. 

GMSTs improved on each puzzle day over the complete set of puzzles (N=2,218) issued between January 1, 2018 and January 27, 2024 (**Figure 1**). This improvement was fairly dramatic in the first few years for some puzzle days (most prominently for Sun), and graded improvement continued for each puzzle day until the end of the sample period (top panel). The 2-year interval density plots of raw solve time distributions (bottom panels) show that performance on individual puzzle days became more consistent over time (higher peaks with narrower distributions). Because I did not have access to the raw solver data from which the GMSTs were drawn, however, it was not possible to disentangle improvement and increased consistency for individual "early adopters" of Matt's tracking software versus stronger solvers joining the solver pool over time. Note also that GMS performance was tracked in my analyses by puzzle issue date, as I did not have access to GMS puzzle completion dates. It's reasonably safe to assume, however, that the GMS (a different individual solver for most puzzles, presumably) solved in approximately the sequence of puzzle issue. IS1 performance, in contrast, was tracked by puzzle completion data since I *was* able to obtain completion timestamps for my own solves with Matt's assistance.  

**Figure 1. GMS Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/c1893d67-f2ae-4fee-8392-318a3e843f19)
*<h5>GMS Final (as of Jan. 27, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 28.8, Mon: 5.7, Tue: 7.7, Wed: 11.4, Thu: 15.2, Fri: 17.3, Sat: 21.2*<br>


## Results
### Individual Solver 1 (IS1) Performance Over Time

IS1 solved N = 1,174 puzzles in the sample period: 230 (19.6%) in 2021, 493 (42.0%) in 2022, and 451 (38.4%) in 2023/24 (through Jan. 27, 2024). The total solve time for IS1 was 10.8 days (2021: 2.2 days; 2022: 4.7 days; 2023/24: 3.9 days). The total solve time for the GMS over this same set of puzzles was 14.7 days.     

IS1's per puzzle day 10-puzzle moving averages across the sample period are shown in **Figure 2** (top panel). Over the full solve period, IS1 had considerably more solve time volatility than did the GMS. **Supplementary Figure 1** shows that the volatility of IS1's per puzzle day solve times was *not* likely due to chance stretches of puzzles with higher or lower than usual median difficulty (as determined by GMS performance on the same puzzle set). Longer term volatility aside, there was a large amount of improvement in IS1 performance on the more difficult later week puzzle days (Thu-Sun) between Q2 2023 and the end of the sample period. This improvement can be seen in both the top and bottom panels of **Fig. 2**. Like the GMS, IS1 also became more consistent on early week puzzle days (narrower distributions and higher, sharper peaks across the last two solve intervals ; **Fig. 2** bottom panels), though this trend didn't carry through to the later week puzzle days to the extent that it did for the GMS.    

**Figure 2. Solve Time Overview by Puzzle Day: 10-Puzzle Moving Averages and Distributions of Raw Values**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/5b09bdbb-3511-4400-a9a1-3d56780bb7c9)
*<h5>IS1 Final (as of Jan. 27, 2024) 10-puzzle moving average of solve time (m), per puzzle day:*<br>
*Sun: 18.7, Mon: 4.7, Tue: 5.7, Wed: 7.4, Thu: 10.9, Fri: 10.9, Sat: 11.2*<br>

###
**Figure 3** shows IS1's solve time performance trajectory in violin plots with swarm plot overlays, broken out by 1-year solve date intervals. Violin plots show both the range (vertical extent) and distribution characteristics (width as it varies across the y-axis range) for each puzzle day, per solve interval. Black lines on the violin plots demarcate solve time quartiles per puzzle day. Swarm plot overlays per puzzle day show individual puzzle raw solve times. The narrow geometries of the later week violin plots relative to the earlier week ones correspond to greater relative performance variability on those solve days. This phenomenon will be discussed in the final section of the summary in the context of correlation between past and future performance and prospects for predictive modeling. 

**Figure 3. Solve Time Overview by Puzzle Day: Violin Plots With Swarm Plot Overlay**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/150b81f8-c5a0-4e3f-88c5-9260556a61e4)
*<h5>Median[IQR] solve time (m), per puzzle day, per solve interval:*<br>
*2021:    Sun: 24.8[22.7-29.0], Mon: 6.2[5.7-6.7], Tue: 7.6[6.8-8.5], Wed: 8.5[7.6-10.7], Thu: 13.5[11.2-16.2], Fri: 14.1[10.9-18.4], Sat: 18.2[12.8-22.0]*<br>
*2022:    Sun: 25.2[22.2-28.8], Mon: 6.1[5.7-6.6], Tue: 7.0[6.4-8.1], Wed: 9.1[7.9-10.6], Thu: 13.5[11.5-16.1], Fri: 13.6[11.5-16.8], Sat: 17.4[14.3-22.5]*<br>
*2023/24: Sun: 20.8[18.3-27.1], Mon: 5.2[4.8-5.7], Tue: 6.2[5.6-6.9], Wed: 8.3[7.1-10.0], Thu: 13.0[10.7-15.8], Fri: 11.4[9.4-14.5], Sat: 14.9[10.7-17.4]*<br>


### Individual Solver 1 (IS1) Performance Vs Global Median Solver (GMS) 

The next series of figures directly compare IS1 solve performance to that of the GMS over the same puzzle set. For these analyses, IS1 solves were broken into two solve intervals: pre-2023 (n=723; 61.6% of total solves); 2023/24: n=451; 38.4%). Per puzzle day, in the figures relevant to these analyses, pre-2023 solves are represented by lighter-colored points and regression lines and 2023/24 solves by darker-colored ones. 

**Figure 4** shows per puzzle day scatterplots of raw GMSTs (x-axis) versus IS1 solve times (y-axis). Points falling on the dashed diagonal line represent identical raw solve times for IS1 and GMST on a given puzzle. Points above and below this line represent "wins" for the GMS and IS1, respectively. Win % across all puzzle days was high pre-2023 (86.7%), but increased even further in the 2023/24 interval (90.7%). In terms of individual puzzle days, IS1's highest win % in the pre-2023 interval was for Sunday (96.9%), but was for Saturday (95.2%) in the 2023/24 interval. The lowest IS1 win % for both time periods was for Monday puzzles (I'm a fat-finger king), though my Monday win rate did improve substantially in 2023/24 (from 63.5% to 84.1%). The mean magnitude of performance advantage for IS1 over the GMST also increased in the more recent solve interval for all puzzle days together (-4.6 to -5.3 minutes), as well as for most individual puzzle days. Finally, per puzzle day regression lines show that there was a relatively high degree of correlation for raw solve times between IS1 and GMST (range across individual puzzle days and solve intervals: .31-.78). The next figure addresses this correlation in a way that is normalized for recent (prior to a give solve) baseline performance, per solver. 

**Figure 4. IS1 vs GMS: Comparison of Raw Solve Performance by Puzzle Day and Solve Interval**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/ba6bdff8-b3dd-4016-b028-44f04856bdab)
*<h5> Win % for IS1 vs GMS, by IS1 solve interval:*<br>
*pre-2023: All: 86.7, Sun: 96.9, Mon: 63.5, Tue: 88.9, Wed: 88.0, Thu: 91.2, Fri: 90.0, Sat: 89.5*<br>
*2023/24:  All: 90.6, Sun: 91.5, Mon: 84.1, Tue: 85.0, Wed: 95.0, Thu: 89.4, Fri: 94.1, Sat: 95.2*<br>

*<h5> Mean(SD) Solve Time Difference (m) for IS1 vs GMS, by IS1 solve period (negative denotes faster for IS1):*<br>
*pre-2023: All: -4.6(5.2),  Sun: -9.8(6.6), Mon: -.32(1.2), Tue: -1.8(1.7), Wed: -2.7(2.5), Thu: -5.2(4.2), Fri: -5.7(4.6), Sat: -7.3(6.0)*<br>
*2023/24:  All: -5.3(5.0),  Sun: -10.0(6.1), Mon: -.75(.86), Tue: -1.8(1.5), Wed: -3.2(2.2), Thu: -5.6(4.1), Fri: -6.4(3.5), Sat: -8.1(5.2)*<br>
###
Along with comparison of raw solve performance between IS1 and GMS, the degree to which the same puzzles were *relatively* difficult for the two solvers was addressed. Per solver (IS1 or GMS) each raw solve time was taken as a % difference from a decay-time weighted average of the *previous* 20 puzzles solved on the same puzzle day ('Recent Performance Baseline'; RPB). These RPB-adjusted solve times were then plotted against each other on a per puzzle day and per solve period basis (**Figure 5**). Points falling in the lower left ("relatively easy for both solvers") and upper right ("relatively hard for both solvers") quadrants represent concordance of relative difficulty for a given puzzle. The most common outcome across puzzle days for both solve periods was "relatively easy for both solvers" (pre-2023: 42.2%; 2023/24: 45.3%), and the second most common was "relatively hard for both solvers" (pre-2023: 24.3%; 2023/24: 26.9%). It's not surprising that "easy" concordance was more common than "hard" concordance, since solvers constantly improved/outperformed their RPB on a puzzle-to-puzzle basis. A substantial minority (~30%) of puzzles, however, were either relatively easy for IS1 and relatively hard for GMS or vice versa (lower right and upper left quadrants, respectively). This suggests that environmental and puzzle-specific variables may affect different solvers in different ways. Starting in the next section, the focus will be on summarizing the effects of some of these variables on IS1 (and GMS) performance.  

**Figure 5. IS1 vs GMS: Comparison of Baseline-Adjusted Solve Performance by Puzzle Day and Solve Interval**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/8c54a366-3697-4c1b-93e3-db0812f77944)
*<h5> IS1-GMS Quadrant % by IS1 solve period:*<br>
*LL: Relatively Easy for Both IS1 & GMS/ UR: Hard for IS1 & GMS/ UL: Easy for GMS-Hard for IS1/ LR: Easy for IS1-Hard for GMS*<br> 
*pre-2023: All: 42.2/24.3/14.8/18.7, Sun: 41.0/28.4/13.7/16.8, Mon: 37.9/20.4/22.3/19.4, Tue: 42.1/24.3/12.1/21.5, Wed: 43.0/26.2/14.0/16.8, Thu: 46.5/24.8/11.9/16.8,<br> Fri: 42.4/22.2/17.2/18.2, Sat: 42.3/24.0/12.5/21.2*<br>
*2023/24:  All: 45.3/26.9/12.2/15.6, Sun: 39.4/26.8/15.5/18.3, Mon: 45.2/19.4/14.5/21.0, Tue: 50.0/20.0/15.0/15.0, Wed: 48.3/31.7/8.3/11.7, Thu: 45.5/24.2/10.6/19.7,<br> Fri: 45.6/29.4/14.7/10.3, Sat: 44.4/36.5/6.3/12.7*<br>
###
Overall, correlations between baseline-normalized IS1 and GMS solve times were moderately-to-strongly positive, with greater strength for each puzzle day in the more recent solve interval. This increased correlation strength in the more recent solve interval relates to the increased consistency/decreased volatility in solve performance for both IS1 and the GMS, even as performance steadily improved across puzzle days for both solvers (see **Figs. 1 and 2**).<br> 
*<h5>IS1-GMS Correlation (Pearson r) of recent performance baseline(RPB)-adjusted solve difficulty by IS1 solve interval:*<br>
*pre-2023: All: .47, Sun: .45, Mon: .33, Tue: .45, Wed: .54, Thu: .54, Fri: .46, Sat: .46*<br>
*2023/24:  All: .63, Sun: .57, Mon: .46, Tue: .44, Wed: .66, Thu: .60, Fri: .65, Sat: .77*<br>

### IS1 Performance by Puzzle Constructor(s)

A high proportion of puzzles solved by IS1 (71.6%) were authored by either repeat individual constructors or repeat specific constructor teams (both referred to as "constructor" from here forward). This afforded the opportunity to evaluate which constructors IS1 tended, in a relative sense, to struggle against or do well against. Per constructor, the mean of % difference from puzzle day-specific recent performance baseline (RPB; see text section pertaining to **Fig. 5**) was computed. This measure allowed assessment of constructor difficulty adjusted for solver form at the time of a given solve and constructor past puzzle day heterogeneity. **Figure 6** shows heatmapping of IS1 performance using this normalized measure, along with GMS performance on the same set of puzzles, against the n=74 constructor(s) contributing >=4 puzzles over the sample period. While only 13.2% of constructor(s) contributed this many puzzles, this group contributed 39.9% of all puzzles solved by IS1.  

Warmer colors (-%) in **Fig. 6** indicate that on average the solver was relatively fast against a given constructor; cooler colors (+%) indicate slower solves. Mean difference from RPB for IS1 solve time against different constructors ranged from -41.7% for "easiest constructor" (John Clark-Levin) to +31.1% for "hardest constructor" (Kyle Dolan). The range for the GMS was slightly smaller, from -32.8% for "easiest constructor" (Brian Ori) to +22.3% for "hardest constructor" (Bruce Haight). "Hot" or "cold" constructors for IS1 tended to be relatively fast or slow, respectively, for the GMS. However, there was clearly a substantial degree of discordance in terms of specific order and some constructors stood out as being either "hot" for IS2 but "cold" for the GMS (e.g., Peter A. Collins, Brad Wiegmann) or vice versa (e.g., Will Nediger, David Tufts). 

**Figure 6. Heatmapping of IS1 and GMS Performance Against Individual Constructors**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/dbc837aa-5a55-4eef-9884-0b2122215d71)
*<h5>Constructor rankings are sorted by normalized IS1 relative solve speed. GMS values over the same set of puzzles are included for comparison.*<br>
###
The next correlational analysis was aimed at assessing the potential predictive value of IS1's baseline-adjusted past performance against specific constructors on their future performance against the same constructor. **Figure 7** shows this correlation between IS1 past performance (as mean % difference from RPB) against a given constructor (x-axis) and performance on the next solved individual puzzle by that constructor (y-axis). This analysis was restricted to only the n=242 puzzles by the constructor included in **Fig. 6** that were solved *after* >=3 previous puzzles by the same constructor (based on puzzle completion date for IS1, but issue date for GMS). There was a weak-to-moderate positive correlation for IS1 (r=.14), but a moderately strong one for GMS (r=.40). This weaker correlation for the individual solver relative to the GMS was also seen for IS2 (see link to analysis in Introduction). This disparity may have been due to the fact that performance for a single solver is inherently subject to more puzzle-to-puzzle variability than that of an "aggregate solver". Regardless, the evident positive correlations for all 3 solvers at relatively low puzzle n's provides optimism that including past performance vs constructor will have predictive value in the modeling phase.     

**Figure 7. IS1 and GMS: Past Performance Against Individual Constructors as "Prediction" of Next Puzzle Performance Against the Same Constructor**  

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/aab07630-f7ba-4ec8-b284-22fe1cbfb29a)
*<h5>Pearson correlation coefficient (r): IS1: .14, GMS: .40*

### IS1 Performance by Completion Time of Day

Many external variables are likely to have an impact on individual solver performance, for the large majority of which data collection would be very difficult. Examples include data relevant to how tired, stressed, influenced by caffeine and other substances, or distracted by other sensory stimuli the solver was while working on a given puzzle. The hardware technology used to solve a given puzzle (e.g., phone vs tablet vs computer) will also likely influence solve times in idiosyncratic ways. One external variable that we *are* fortunate to have data on (thanks, once again, to Matt at XWord Stats) is time of day at puzzle completion. **Figure 8** shows IS1's solve performance by hour of day, overall (black) and by puzzle day (by color). To control for day-specific puzzle difficulty, solve times are expressed as % difference from puzzle day-specific recent performance baseline (RPB). 

IS1 completed most puzzles during the sample period either early in the morning (7-8 AM; 35.3% of all solves) or in the evening between 6-10 PM (52.5% of all solves). The most notable trend in IS1's data in terms of time of completion was that a disproportionate number of "very fast" solves (>=50% faster than day-specific RPB) took place in the 10 PM hour. Eleven of seventy-seven (14.3%) "very fast" solves took place in the 10 PM hour, but only 32/1097 (2.9%) "very fast" solves took place in all other hours combined. Nonetheless, interpretation of this result is still difficult because puzzle *start* times were not available. Thus, it can't be distinguished with the available data whether IS1 was a better performer at night or simply finished easier puzzles before bedtime and left harder ones for morning completion. To this point, nearly all of the "very fast" 10 PM solves were for new Friday or Saturday puzzles released the evening before at exactly 10 PM. An additional caveat is that all solve times were recorded with respect to the US Eastern Time Zone, and there is no indication for if/when individual puzzles were completed in other time zones.        

**Figure 8. Recent Performance Baseline-Adjusted Solve Times by Hour of Completion**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/dac5f87e-022c-4f5b-abaa-a4ef5384df60)


### Correlations of IS1 Performance on Individual Puzzles to Puzzle-Specific Features and Recent Past Performance

Numerous potentially interesting features pertaining to puzzle grids, clues, and answers were obtained from XWord Info across the sample period. Features showing strong correlation to IS1 solve performance become promising candidates as input features for predictive modeling, in current forms and/or when combined in novel ways with other existing features. **Figure 9** shows correlation heatmapping separately for 15x15 puzzles (Mon-Sat) and 21x21 puzzles (Sun) for a subset of all measured features with distributions amenable to linear regression and correlation analysis (see **Supplementary Figure 2** for individual 15x15 puzzle day matrices). The Pearson correlation coefficient (r) captures linear correlation strength between a given feature and solve times (top row and leftmost column of correlation matrix; red indicates a strong positive correlation and green a strong negative correlation). The rightmost column/bottom row per matrix shows the correlation between IS1 solve times for individual puzzles and puzzle day-specific recent performance baseline (RPB). For both 15x15 puzzles and 21x21 puzzles, this (positive) correlation was stronger than any other measured feature correlation to IS1 solve time. This finding generates a prediction that recent (relative to a puzzle date to be predicted) solver form per puzzle day will be more predictive of performance on a novel puzzle than will be any individual grid, clue or answer feature. 

As can also be seen in the **Fig. 9** correlation matrices, a number of grid, clue and answer-related features correlated strongly with each other. For example, 'Average Answer Length' and 'Freshness Factor' showed a strong negative correlation. This relationship makes intuitive sense because 'Freshness Factor' is a measure of aggregate answer rarity for a given puzzle, and longer answers have a higher likelihood of being uncommon than shorter ones. Additionally, numerous features not selected for this analysis might still be useful in predictive modeling but either had non-continuous distributions (e.g., 0 or 1 for puzzles with normal vs non-standard symmetry) or pertain to a feature that is largely specific to only one or several puzzle days (e.g. Rebuses, Circles, Shaded Squares; see **Supplementary Figures 3-5**). 

One additional note on data inclusion time range: 2021 solves (n=230) have been removed for this analysis due to the relatively large degree of volatility in solve times seen during that initial year of digital solving (see **Fig. 3**). Also see discussion in the next section about the tradeoff between being able to identify patterns in the relationships between features and solve time across puzzle days vs accounting for the contantly shifting baseline in performance by normalizing solve times to recent performance baseline (RPB). 

**Figure 9. Correlation Heatmapping of IS1 Raw Solve Times vs Grid, Clue, Answer and Past Performance Features**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/5aee5168-c1e4-4bda-9d8a-bbc56c72bfe3)
*<h5>Correlation heatmaps derived from N=810 15x15 (left panel) and N=134 21x21 (right panel) puzzles solved by IS1 from 2022-2024.*

###
**Figure 10** through **Figure 21** are companion figures to the correlation heatmapping shown in **Fig. 9**. These figures show, across all 15x15 puzzle days (black) and by-puzzle-day (colors), scatterplots of select features of interest vs IS1 raw solve times at the level of individual puzzles. A feature distribution density plot (FDP) shows puzzle day-specific trends in the distribution of each plotted feature. 

Per feature, raw IS1 solve times are plotted on the y-axis of the **all 15x15 puzzle days plot** and the correlation (Pearson r) between raw IS1 solve times and the feature across all 15x15 puzzles is reported. This allowed trends spanning across the full set of 15x15 puzzles to be visuaized and quantified. However, for the **puzzle day plots**, IS1 solve times on the y-axis were normalized as % difference from puzzle day-specific recent performance (RPB). This normalization was performed to aid in teasing out potentially subtle correlations between features and solve times on the individual day level that might otherwise have been lost in the noise of the ever-shifting performance baseline. Normalizing the all 15x15 data to remove baseline volatility removes cross-puzzle day trends, trends that we very much would like to see in the evaluation of features for potential inclusion in a predictive model that is agnostic to puzzle day. Hence, the "best of both worlds" approach I've taken here.     

Though most features had at least moderate strength correlations with IS1 solve times across all 15x15 puzzles, at the by puzzle day level these correlations were typically stronger for the more difficult puzzle days (Sat, in particular). Correlations robust enough to show through within a given puzzle day, where many variables related to puzzle difficulty presumably had similar properties across puzzles, are likely to have a meaningful impact on solve times. As is evident across the scatterplot figures below, several factors make it more likely for later week puzzle days (e.g., Sat) to show within-day correlations that may also be associated with predictive value. For one, there may be threshold values per feature below/above which that feature's impact was not significant in comparison with the contribution of solver aptitude (see discussion above about **Fig. 9**, and also see **Fig. 21**). Because late week puzzle days almost uniformly had considerably wider ranges of feature values than earlier week puzzle days (compare per day widths in the FDPs or x-axis extents in the scatterplots), effects apparent on those late week days may have been severely clipped by limited ranges on the early week days. Secondly, early week puzzles may also simply not have been difficult enough overall for given features (especially grid features, as a clue is only as difficult as the answer content that it houses) to have had discernable impacts on solve times.
    
Each figure caption for **Figs. 10-21** compares the correlation strength for a given feature for IS1 with that for the global median solver (GMS) over the same set of puzzles. While GMS correlations were uniformly directionally the same as for IS1, they were also uniformly *stronger* than those for IS1. This relative strength was likely related to the more variable per day baseline solve performance of IS1 relative to the GMS (**see Figs. 1 and 2**), which in turn relates to one being a single human subject to puzzle-to-puzzle variability in many aspects and the other being a "mathematical entity" selected from many individual solvers on a given puzzle for being right in the middle of solve performance on that puzzle.        

#### Scatterplots for Individual Features vs IS1 Solve Times, with Associated Feature Distribution Density Plots (FDPs)


#### *Grid Features*

**Figure 10. Number of Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/231a323d-41be-4222-b3bf-867151f63318)
*<h5>Individual Solver 1 (IS1) solve times and '# Answers' had a moderately strong negative correlation for 15x15 puzzles (r= -.47).<br>
Global Median Solver (GMS) correlation strength on the same set of 15x15 puzzles was considerably stronger (r = -.61).<br>*

*Most of the strength of the all 15x15 puzzles correlation (black) was related to the large leftward shift in the FDP for the two most difficult puzzle days (Fri and Sat). '# Answers' was strongly negatively correlated with 'Average Answer Length' (see Fig. 13) and measures of answer rarity (e.g., 'Freshness Factor'; see Fig. 19). Thus, when puzzles were difficult (Fri and Sat), this fewer answers/more long answers combination meant more answers that were rarely encountered/unique. Within the most difficult puzzle days (Fri and Sat) a correlation of the same sign (negative) as the overall 15x15 puzzles correlation was seen, emphasizing this relationship. Moreover, relatively strong correlations of the reverse sign (positive) were seen for the early week puzzle days (Mon-Wed). This finding suggests that, below a particular per-clue/answer difficulty threshold mostly only attained in later week puzzles, the time penalty incurred by having to read relatively more clues was greater than the time savings from encountering relatively fewer longer answers.*       
       
**<h4>Figure 11. Number of Open Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/c599a916-c992-4905-99c2-8786aa604900)
*<h5>IS1 solve times and '# Open Squares' had a moderately strong positive correlation for 15x15 puzzles (r= .47).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .60).<br>*

*'# Open Squares' is a proprietary measure from XWord Info that counts all white squares that are *not* bordered by black squares. Most of the strength of the all 15x15 puzzles correlation (black) was related to the large rightward shift in the FDP for the two most difficult puzzle days (Fri and Sat), with nearly all 15x15 puzzles with >~80 open squares falling on those days. '# Open Squares' was strongly negatively correlated with '# Answers' (see Fig. 10) and strongly positively correlated with '# Average Answer Length' (see Fig. 13). For difficult puzzle days (Fri and Sat), these relationships translated to longer answers that were also more difficult. As with '# Answers' for this solver, the strongest within-puzzle day correlation of the same sign as the overall correlation (positive) was seen for the most difficult puzzle day (Sat). This indicates that, for this solver, there may have been an overall difficulty threshold in play for this feature to have a discernble impact on solve times. However, because nearly all puzzles with >~100 '# Open Squares' were on Saturday (and almost none of these puzzles had "very fast" solves), it is difficult to distinguish a difficulty threshold from a feature value range effect.*   
    
**<h4>Figure 12. Number of Black Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/0e292e61-74ea-4061-816b-bf5c0ceee7e1)
*<h5>IS1 solve times and '# Black Squares' had a weak-to-moderate negative correlation for 15x15 puzzles (r= -.29).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = -.38).<br>*

*Most of the strength of the all 15x15 puzzles correlation (black) was related to the large leftward shift in the FDP for the two most difficult puzzle days (Fri and Sat), with nearly all 15x15 puzzles with <~32 black squares falling on those days. '# Black Squares' was strongly negatively correlated with both '# Open Squares' and 'Average Answer Length'. So an increase in '# Black Squares' meant shorter, easier answers and a faster solve on average. Within Saturday a relatively strong correlation of the same directionality as the overall 15x15 puzzles correlation was seen, emphasizing these dynamics. The more modest and mixed-sign correlations on the earlier week puzzle days, however, might indicate a difficulty threshold for '# Black Squares' to have an impact on solve times, though the lack of puzzles with <~32 black squares on early week puzzle days makes it hard to discern that from a feature value range effect.*

**<h4>Figure 13. Average Answer Length**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/8eeeb743-4a44-4120-b54d-254bbfa1a80c)
*<h5>IS1 solve times and 'Average Answer Length' had a moderately strong positive correlation for 15x15 puzzles (r= .56).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .71).<br>*

*The strong all 15x15 puzzles correlation for GMS was related to the large rightward shift in the FDP for the two most difficult puzzle days (Fri and Sat). Saturday also showed a relatively strong positive correlation across a wide range of feature values, with higher 'Average Answer Length' being associated with slower solves. As discussed in the context of Figs. 10 and 11, 'Average Answer Length' was strongly negatively correlated with '# Answers' and strongly positively correlated with measures of answer rarity (e.g. 'Freshness Factor; see Fig. 19). So it makes intuitive sense that as 'Average Answer Length' increased, particularly on difficult puzzle days, the answers themelves became more difficult and slowed down solve times even as they decreased in absolute number.* 

*Another interesting observation regarding this feature is that, unlike for the other grid features discussed thus far, the Thursday peak was well-differentiated to the right of those for the earlier week puzzle days in the FDP. Given the relatively strong positive correlations overall and for several late week puzzle days with wide feature value ranges (including Thursday), plus the need to explain why solve times for Thursday were well right-shifted from the earlier week puzzle days (see Fig. 2), this feature becomes an attractive candidate for having some predictive value across multiple puzzle days in the modeling phase.*

**<h4>Figure 14. Number of Cheater Squares**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/a39a1aba-d1a9-4951-b22d-5b30c19fa642)
*<h5>IS1 solve times and '# Cheater Squares' had a weak positive correlation for 15x15 puzzles (r= .20).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .24).<br>*

*Cheater Squares are black squares than can be removed without affecting the overall word count of the grid. These squares make construction easier (hence their name). It can be seen in the FDP that large numbers of them (>~10) almost always appeared on the difficult puzzle days (Fri and Sat), which likely accounted for the (modest) positive correlation across all 15x15 puzzles. Saturday, with by far the widest feature value range of any of the 15x15 puzzle days, showed a moderate reverse sign (negative) correlation. This is not really at odds with the overall 15x15 positive correlation, since these squares are ultimately just black squares even if they facilitate tricky constructions for difficult puzzles. Add enough of them and they will reduce solve time simply by lowering the amount of fill. Incidentally, the reason cheater squares were only rarely seen in odd numbers is the NYT general requirement for grid symmetry.*


#### *Answer and Clue Content Features*

**<h4>Figure 15. Number of Fill-in-the-Blank Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/25e844b0-a02d-4ffe-b601-85ee3321e116)
*<h5>IS1 solve times and '# Fill-in-the-Blank Answers' had a weak-to-moderate negative correlation for 15x15 puzzles (r= -.23).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.26).<br>*

*Most of the strength of this weak-to-moderate correlation for all 15x15 puzzles was related to the moderate rightward shift in the FDP for Monday. Along with the easiest puzzle day employing the largest dose of '#Fill-in-the-Blank', the hardest puzzle day (Saturday) was also slightly left-shifted relative to the other 15x15 puzzle days. There was a moderate negative correlation within Saturday as well, with the rare puzzles employing >~5 fill-in-the blank clues associating with distinctly faster solve times. This indicates that above a certain level of difficulty, fill-in-the blanks likely provide a speed-up mechanism. The lack of correlations within the other puzzles days, however, indicates that the difficulty threshold for this feature to matter was quite high.* 

**<h4>Figure 16. Scrabble Average**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/b211717a-24a4-46c6-9da0-e50cba08ff74)
*<h5>IS1 solve times and 'Scrabble Average' had a weak-to-nonexistent negative correlation for 15x15 puzzles (r= -.05).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = -.06).<br>*

*'Scrabble Average' is another proprietary XWord Info measure, in which each letter in the answer grid is assigned its equivalent value in Scrabble. Since tile values in Scrabble increase with rarity of letter frequency in English texts, it would make sense that a higher value for this feature would be associated with *answers* of greater rarity. However, 'Scrabble Average' had only moderate positive correlations with other more direct measures of answer rarity both across 15x15 puzzles (Fig. 9) and specifically within the later-week puzzle days (Supp. Fig. 1). Given that these more direct measures of answer rarity DID have strong positive correlations to solve times (see Figs. 17-19), and that the correlation of 'Scrabble Average' itself to IS1 solve times across puzzle days was weak, this feature is a candidate to be left out of predictive modeling entirely.*

**<h4>Figure 17. Number of Scrabble Illegal Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/6b6b5d6c-ce48-4990-8b2b-18912f3f01f8)
*<h5>IS1 solve times and '# Scrabble Illegal' had a weak positive correlation for 15x15 puzzles (r= .13).<br>
GMS correlation strength on the same set of 15x15 puzzles was slightly stronger (r = .18).<br>*

*'# Scrabble Illegal' answers is a proprietary measure of XWord Info that gets at answer rarity more directly than does 'Scrabble Average'. Interestingly, the distributions for 15x15 puzzle days in the FDP were highly overlapping, other than a small leftward shift for Monday and Tuesday that likely accounted for the (modest) overall 15x15 puzzles positive correlation. '# Scrabble Illegal" had only moderate positive correlations with the most direct measures of answer rarity ('# Unique Answers' and 'Freshness Factor'; see Figs. 18 and 19), which was somewhat surprising to me. There were hints, particularly in the Monday and Saturday correlation plots, that this feature might have impacted solve times at the extreme low and high ends of its value range. However, the weak overall and within-day correlations to IS1 solve times shown by this feature suggest that more non-standard vocabulary *alone* may not strongly signify or predict puzzle difficulty.*    

**<h4>Figure 18. Number of Unique Answers**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/f54d872b-371d-4796-910d-ee156fe9aa05)
*<h5>IS1 solve times and '# Unique Answers' had a weak-to-moderate positive correlation for 15x15 puzzles (r= .36).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger, reaching the level of moderate correlation (r = .42).<br>*

*<h5>A unique answer is defined here as one that does not appear in any other NYT crossword puzzle in either the Shortz or pre-Shortz eras (either before or after the puzzle release date). The (albeit modest) strength of the all 15x15 puzzle day correlation was related to the easiest puzzle day (Monday) having a leftward shift in the FDP while the most difficult puzzle days (Fri and Sat) had rightward shifts. Given the relatively low correlations and the results shown in the next figure, uniqueness is perhaps an overly stringent criterion with which to define answer rarity. However, as evidenced in the all 15x15 puzzles scatterplot, there may still be some use for this feature in the predictive modeling phase when values reach both extremes of the range*

**<h4>Figure 19. Freshness Factor**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/aa9ab0e8-39c3-4e7d-a123-c4cdb6b87280)
*<h5>IS1 solve times and 'Freshness Factor' had a strong positive correlation for 15x15 puzzles (r= .57).<br>
GMS correlation strength on the same set of 15x15 puzzles was considerably stronger, reaching the level of strong correlation (r = .71).<br>*

*<h5>'Freshness Factor' is a proprietary XWord Info measure that assesses the aggregate relative novelty of all answers in a given crossword puzzle as compared to those in all other crossword puzzles in the NYT archive. The much stronger correlation to IS1's solve times as compared to that for '# Unique Answers' suggests that there's much to be gained by taking a graded, as opposed to all-or-none, approach in assessing answer rarity. Overall, this feature had the strongest correlation with GMS solve times of any grid, clue or answer feature evaluated (but see Fig. 21 for a past performance feature with a stronger correlation to solve time).* 

*Additionally, with potential relevance to predictive modeling, the 15x15 puzzle days peaked in this measure (seen in the FDP) in relatively close concordance to the by day peaks in raw solve times (see **Fig. 2**) for IS1. The only other puzzle feature coming close to this degree and concordance of peak separation was 'Average Answer Length', though 'Freshness Factor' showed a Monday-Tuesday separation more in line with the solve time peaks separation for those two easy puzzle days. The positive correlation for this feature was also seen to a relatively consistent degree within each of the individual puzzle days. Saturday, strikingly, had both the strongest within-day correlation and also the widest range of feature values of any individual puzzle day. The observations discussed here lead me to believe that 'Freshness Factor' will be the most useful puzzle feature evaluated presently in terms of predictive modeling of solve performance.*


**<h4>Figure 20. Number of Wordplay Clues**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/dff8d098-ce79-42d6-b72d-a5bc76e0a80a)
*<h5>IS1 solve times and '# Wordplay Clues' had a moderate positive correlation for 15x15 puzzles (r= .39).<br>
GMS correlation strength on the same set of 15x15 puzzles was stronger (r = .49).<br>*

*<h5>'# Wordplay' clues is an (admittedly) somewhat subjective measure that I have manually evaluated and calculated clue-by-clue across the entire puzzle sample completed by IS1. The FDP for this feature had some interesting properties, including the clear result that later week (Thu-Sat) puzzles indeed had a larger allocation of 'trickier' clues than early week puzzles. The was also a prominent leftward shift for Monday puzzles, though with a strong second peak aligned with the Tuesday peak. Taken together, these early and late week distribution offsets were likely related to the moderate overall positive correlation across all 15x15 puzzles. The rare early week (Mon-Wed) puzzles with a relatively large '# Wordplay' clues clearly mostly had slower IS1 solve times, which makes intuitive sense in the context of how straightforward those puzzles generally were. Past Tuesday, however, there were only weakish within-puzzle day correlations for this feature. This suggests that there may have been an overall difficulty threshold that largely dictated the impact that '# Wordplay Clues' might have had on solve speed.* 

#### *Past Performance Features*

**<h4>Figure 21. Decay-Time Weighted Recent Performance (RPB)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/060142dc-c640-4b7a-b6ab-0a112df30973)
*<h5>IS1 next raw solve time and IS1 'Recent Performance Baseline (RPB)' had a strong positive correlation for 15x15 puzzles (r= .74).<br>
GMS next raw solve time and GMS 'RPB' correlation strength was stronger, reaching the level of very strong correlation (r = .87).<br>*

*<h5>The all 15x15 puzzles correlation for this feature was considerably stronger than that for any puzzle feature. The implication is that time decay-time weighted IS1 recent past performance (RPB over the 20 day-specific puzzles previous to a given solve) will likely have more predictive value for the next IS1 raw solve time than will any single puzzle, clue or answer feature. Not all puzzle days were created equally, however, with regard to correlational strength (and, potentially, predictive power) of RPB and next raw solve time for this solver. Monday (r=.51) having an very strong correlation relative to the other 15x15 puzzle days was unsurprising, given how few "degrees of freedom" there are in the easiest puzzles. By a considerable amount, the lowest puzzle day-level correlation for IS1 next raw solve time with RPB was for Thursday (.15). This is perhaps unsurprising, since Thursday had a large degree of heterogeneity, with nearly all puzzles on that day involving a gimmick or trick of some variety (including rebuses of various flavors; see Supp. Fig. 3). Thursday also had the second lowest puzzle day correlation for the other individual solver (IS2; see link to analysis in Introduction to this summary), indicating that this may generalize in the solver pool to at least some degree.* 

*It is noteworthy, however, that the lowest correlation for the GMS was for Saturday (.22), with Thursday coming in as only the second lowest correlation (.35). My suspicion is that this largely related to the volatility of the Saturday solver pool that the GMS was drawn from. Because Saturday was considerably more difficult than the other puzzle days, there may have been both a lower N to draw from for any given puzzle as well as a much more variable roster of puzzle completers. Of course, there may also have been a substantial contribution to the relatively low Saturday correlation for the GMS from the heterogeneity of Saturday puzzles (e.g., typically wide feature value ranges) and the high likelihood of middle-of-the-pack solvers getting "stuck" for extended stretches on one or several tough clues or answers.*

*<h5> Next raw solve time and 'RPB' Correlation Strength by Solver (IS1 or GMS) and Puzzle Day:*<br>
*IS1: Sun: .44, Mon: .51, Tue: .39, Wed: .32, Thu: .15, Fri: .32, Sat: .35*<br>
*GMS: Sun: .55, Mon: .59, Tue: .49, Wed: .39, Thu: .35, Fri: .40, Sat: .22*<br>


## Supplementary Figures

**<h4>Figure S1. IS1 10-Puzzle Solve Time Moving Averages Adjusted by GMS Performance, by Puzzle Day** 

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/31caf7c5-2f7c-483f-8917-6c8a9d5b4a54)
*<h5>For each puzzle completed by IS1, % difference for the raw solve time from the global median solve time (GMST) was computed. The 10-puzzle moving average of this difference was then plotted, per puzzle day, by completion date. The volatility present in the raw solve times (see **Fig. 2**) was still mostly present in these adjusted data plots, indicating that this volatility was due to factors other than by-chance runs of greater or lesser difficulty per puzzle day.*

**<h4>Figure S2. Correlation Heatmapping of IS1 Individual Puzzle Performance vs Grid, Answer and Past-Performance Features by Puzzle Day (15x15 Puzzle Days)**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/f1a71f41-1654-4de2-8554-50b344713715)


**<h4>Figure S3. Number of Rebus Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/a11d02ea-7bd2-49ce-8249-88e109fa89ee)
*<h5>Only Sunday and Thursday had an appreciable '# Rebus Squares' for the set of IS1 solves. Rebus squares are those that must be filled with more than one letter, number or symbol for a given puzzle to be solved. There were weak-to-moderate positive correlations for IS1 for both Sunday (r=.26) and Thursday (r=.29). The directionality of the correlations does make intuitive sense, as both their existence and the "rules" for any given rebus can often take a little while to figure out. Additionally, they increase solve time by some degree simply by requiring additional fill and menu toggling relative to a non-rebus puzzle. One caveat here is that the very large number of 0 rebus puzzles, even on Sunday and Thursday, make the strength of these correlations hard to interpret (ie, these are not exactly continuous distributions).*<br>

*Correlation Strength by Puzzle Day: IS1: Sun: .26, Thu: .29; GMS: Sun: .34, Thu: .19* 

**<h4>Figure S4. Number of Circled Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/2e2455de-9565-43a6-9eb8-cf37dac8c583)
*<h5>Circled squares were virtually non-existent in the tougher (Fri and Sat) puzzles. The modest negative correlation seen across all 15x15 puzzle days (-.12) is attributable to the fact that most 15x15 puzzles with circles appeared early in the week. The smattering of puzzles with circles on Sunday almost all fell in the middle of the solve time range regardless of "# Circles", indicating that this feature didn't likely have a major impact on solve times.*

**<h4>Figure S5. Number of Shaded Squares vs IS1 Solve Time by Puzzle Day**

![image](https://github.com/ursus-maritimus-714/NYT-XWord-EDA-Individual-Solver-1/assets/90933302/3ba59f70-c579-437f-9399-934836b65834)
*<h5>Shaded squares, like circled squares, were virtually non-existent on the tougher (Fri and Sat) puzzle days. Also like with circled squares, their function is to reveal a puzzle theme and their presence may provide assistance to solvers on clues in which they are embedded. Most puzzles with shaded squares were within the bottom third of IS1 15x15 puzzle solve times, most likely due to shaded squares almost exclusively showing up only in early week puzzles. Also as with '# Circles', the smattering of Sunday puzzles almost all fell in the middle of the solve time range regardless of "# Shaded Squares", indicating that this feature also didn't likely have a major impact on solve times.* 






