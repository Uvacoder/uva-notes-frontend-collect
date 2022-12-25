# Confounding and Deconfounding: or, Slaying the Lurking Variable

Pearl offers the story of Daniel from Genesis as an example of a [[controlled experiment]].

- King Aspenaz asks a question about causation: Will a vegetarian diet cause my servants to lose weight?
- To understand the causal effect of the diet, he compares what happens to Daniel on the vegetarian diet with what happens to others who do not follow the same.
- The experiment must compare common groups, not just single people.
- The experiment must be prospective, the groups being chosen in advance.
- The one key thing that isn't taken into account is the effect of [[confounding bias]].

> Occurs when a variable influences both who is selected for the treatment and the outcome of the experiment. [^1]

The term confounding originally meant "mixing," indicating that with confounding the causal effects are mixed in some way. The job of the statistician is to determine which variables are true confounders and to remove their influence from the results.

There is a balance to be struck here, as the tendency of most statisticians has been to control for more than they must.

> Statisticians have been immensely confused about what variables should and should not be controlled for, so the default practice has been to control for everything one can measure. [^2]

> Confounding is a causal concept&mdash;it belongs on rung two of the [[Ladder of Causation]] [^3]

It seems that one of the main points that Pearl is making in this chapter is that the hesitance of researchers to make causal claims is overstated. If we can properly adjust for [[confounding bias]], we have a better view of the causal situation and we should be able to make claims about it. If we truly believe that we've eliminated all the important [[confounder]]s, we should also believe in the value of the experiment's results.

## The Skillful Interrogation of Nature: Why RCTs Work

RCT === [[randomized controlled trial]]. Pearl argues that **the primary objective of an RCT is to eliminate confounding**.

[R.A. Fisher](https://en.wikipedia.org/wiki/Ronald_Fisher) initially started using [[randomized controlled trial]]s in his research comparing manurial treatments of fields. He at first attempted to systematically plot different combinations of plants and soil types. He realized that in order to get the best results, randomly assigning the plots allowed an insight that was a better representation, because it eliminates some of the confounding effects.

Because fertility isn't evenly distributed through a field, randomly assigning plants, fertilizers, and soil types and running repeated experiments allows the results to tend toward a more general understanding.

> Thus, randomization actually brings two benefits. First, it eliminates confounder bias (it asks Nature the right question). Second, it enables the researcher to quantify his uncertainty. [^4]

In the example of choosing which of two fertilizers to use on a field, the only influence on the fertilizer choice must be a random process. Drawing a random card from a well-shuffled deck would work.

> Randomization is a way of [disabling] all the old [[confounder]]s without introducing any new [[confounder]]s [^5]

It is so important that the process be truly random that often a [[double blind]] approach is used in human experiments that hides the random element from both the experimenters and the patients.

> Randomization does have one great advantage: it severs every incoming link to the randomized variable, including the ones we don't know about or cannot measure. [^6]

[[randomized controlled trial]]s, while useful, are not always possible. He gives the example of examining the effect of obesity on heart disease: we cannot randomly assign people to be obese or not. Or to smoke or not.

## The New Paradigm of Confounding

Confounding ([[confounder]]) can be loosely defined as anything that leads to a discrepancy between observing and intervening. (see p. 151).

> "Confounding is not a statistical notion. It stands for the discrepancy between what we want to assess (the causal effect) and what we actually do assess using statistical methods." [^7]

[[Exchangebility]] -- Robins & Greenfield approach that requires the researcher to consider the treatment group, imagine what would have happened if they hadn't gotten treatment, and then judge whether the outcome would be the same as for those who had never had treatment. This can be used as a determinant of whether confounding exists in the study.

They expressed this idea of confounding ([[confounder]]) in terms of potential outcomes, dividing the population into four types of individuals: doomed, causative, preventive, and immune.

He uses a flu vaccine as an example:

1. Doomed people are those for whom the vaccine will never work
2. Causative people are those for whom the vaccine causes the disease
3. Preventive people are those for whom the vaccine prevents the disease
4. Immune people are those who will not get the disease in either case

The exchangeable bit here is that the proportion between these four groups in the experiment ought to be the same as the proportion in the general population, otherwise there is a [[confounder]] and our estimate of the effectiveness of the vaccine may be off.

Pearl argues that the biggest benefit to the [[Exchangebility]] approach is that it shows that the prior definitions of confounding 'were inadequate.' However their definition still falls short because we can't know in which group a person will be, so we can't know if the experimental group and the general population are exchangeable.

## The Do-Operator and the Back-Door Criterion

A [[back-door path]] is any path from X to Y that starts with an arrow pointing into X.

X and Y will be deconfounded if we block every back-door path, since these paths allow for "spurious correlation between X and Y."


[[05-the-smoke-filled-debate]]

---
[^1]: p.137
[^2]: p.139
[^3]: p.140
[^4]: p.147
[^5]: p.149
[^6]: p.149
[^7]: p.151