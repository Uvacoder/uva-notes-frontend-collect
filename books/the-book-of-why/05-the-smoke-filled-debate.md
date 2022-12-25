# The Smoke-Filled Debate: Clearing the Air

Starts with the story of Jacob Yerushalmy (a biostatistician and [Abe Lilienfield](https://en.wikipedia.org/wiki/Abraham_Lilienfeld) (an epidemiologist), who were both involved in the debate in the 50s and 60s over whether cigarette smoking caused cancer.

This was a difficult argument for statisticians to settle because there was no way to perform a [[randomized controlled trial]]. It would be unethical to ask someone to smoke for 30 years so that we could study the effects on their health.

The real issue was the argument that there might be a third factor that accounts for lung cancer, and for people's tendency toward nicotine addiction. It wasn't until 1964 that the debate was "settled" by a US Surgeon General's report that declared that "cigarette smoking is causally related to lung cancer in men."

## Tobacco: A Manmade Epidemic

In 1902, cigarettes made up ~2% of the US tobacco market.

By 1952 that figure was 81%. Automation and advertising grew the market dramatically

Before cigarettes lung cancer was rather rare. Between 1900 and 1950 it quadrupled in frequency, and by 1960 was the most common form of cancer in men.

[Richard Doll](https://en.wikipedia.org/wiki/Richard_Doll) and [Austin Bradford Hill](https://en.wikipedia.org/wiki/Austin_Bradford_Hill) teamed up to figure out a way to examine the causes behind the cancer epidemic. 

They knew they couldn't perform a [[randomized controlled trial]], so they compared patients who had already been diagnosed with cancer to a control group of healthy volunteers. The interviewers were not told who had cancer and who did not, to avoid bias.

Their study showed an overwhelming correlation between smoking and cancer. Out of 649 cancer patients interviewed, all but 2 of them had been smokers.

The type of study they performed is now called a [[case-control study]] "because it compares 'cases' (people with a disease) to controls." [^1]

Some drawbacks of a [[case-control study]] that Pearl points to are:
1. It is retrospective, meaning they studied people who already had cancer and looked backward to discover why.
2. The probability logic is backward: the data tell us the probability that a cancer patient is a smoker instead of the probability that a smoker will get cancer.
3. It is susceptible to [[recall-bias]]
4. It is susceptible to [[selection-bias]]

[Jerome Cornfield](https://en.wikipedia.org/wiki/Jerome_Cornfield) put forward a crucial rebuttal of Fisher's objection by resorting to a mathematical analysis of the issue. He argued that, given that smokers have nine times the risk of developing lung cancer, if there were a [[confounder]] such as a 'smoking gene,' it would have to be at least nine times as common in smokers to explain the increase in risk.

This means that if 11 percent of nonsmokers have the 'smoking gene,' then 99 percent of smokers must have it. And if 12 percent or more of nonsmokers have it, then it's mathematically impossible for over 100 percent of smokers to have it. This argument is called [[cornfield-inequality]]. 

Pearl points to this argument as the beginning of an approach called [[sensitivity-analysis]].

[[hills-criteria]] arise at this point out of the surgeon general's advisory committee in 1963 (Hill put forward his version of the criteria in 1965).

This committee led to a sea-change in how the American government, and its people, viewed smoking, which caused the restrictions on advertisement and the requirement of warnings, etc.

Ultimately Pearl's point in this chapter is to demonstrate that what was lacking in all of these approaches was a way to examine causality effectively. He points to the power of [[causal diagram]]s again as being crucial to moving beyond this sort of confusion.


[^1]: p. 173