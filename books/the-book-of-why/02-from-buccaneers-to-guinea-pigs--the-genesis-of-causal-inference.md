# [[Galton]]

- [Francis Galton](https://en.wikipedia.org/wiki/Francis_Galton)
  - First cousin of [Charles Darwin](https://en.wikipedia.org/wiki/Charles_Darwin) [[Charles Darwin]]
  - 2/7/1877 presented at the Friday Evening Disclosure at the Royal Institution of Great Britain in London
    - His presentation was titled "Typical Laws of Heredity"
  - His presentation used what he called a 'quincunx,' now called a [Galton board](https://en.wikipedia.org/wiki/Bean_machine) or bean machine to demonstrate the [central limit theorem](https://en.wikipedia.org/wiki/Central_limit_theorem), which was originally and without much notice proven in 1733 by [Abraham de Moivre](https://en.wikipedia.org/wiki/Abraham_de_Moivre), then popularly put forward again by [Pierre-Simon Laplace](https://en.wikipedia.org/wiki/Pierre-Simon_Laplace)
	  - [[Galton Board]]
    - The theorem states that any random process (coin clips, the galton board) will lead to the same probability distribution (the bell curve)
  - Galton was trying to explain a puzzle.
    - If you increase the number of rows of the board, ostensibly demonstrating what happens with subsequent generations, the base of the bell curve gets wider and wider.
    - This is not what happens with human attributes like height. The width of the distribution stays relatively constant over time.
    - "We didn't have nine-foot humans a century ago, and we still don't"[^1]
    - Galton put forward that there must be some mechanism that facilitates "regression toward the mean"
      - "Sons of tall men tend to be taller than average&mdash;but not as tall as their fathers. Sons of short men tend to be shorter than average&mdash;but not as short as their fathers." [^2]
    - Galton installed chutes in his board after the first "generation" that brought the balls back toward the middle of the board. _The chutes were Galton's causal explanation for regression to the mean_
      - Galton's ideas were the birth of statistics as a field of study
      - He noticed that certain physical qualities of people were correlated when considering entire populations.
      - He realized the importance of the **[[regression line]]** when looking at scatter plot diagrams
        - "the predictions always fall on a line, which he called the regression line, which is less steep than the major axis (or axis of symmetry) of the ellipse. In fact there are two such lines, depending on which variable is being predicted and which is being used as evidence. You can predict the son's height based on the father's or the father's based on the son's. The situation is completely symmetric. Once again this shows that where regression to the mean is concerned, there is no difference between cause and effect." [^3]
      - The slope of the regression line cannot be greater than 1, or else regression to the mean will not hold
    - "For the first time, Galton's idea of correlation gave an objective measure, independent of human judgment or interpretation, of how two variables are related to one another.[...]Galton's disciple [Karl Pearson](https://en.wikipedia.org/wiki/Karl_Pearson) later derived a formula for the slope of the (properly rescaled) regression line and called it the **correlation coefficient.**"[^4]
		- [[Karl Pearson]]
      - [[Correlation coefficient]] is still one of the major numbers statisticians compute when they want to know how strongly two variables in a data set are related

## Galton And The Abandoned Quest

- Galton failed to demonstrate a biological mechanism that explained the chutes he added to his board to explain regression to the mean, and eventually stopped trying to explain the causal forces behind that mechanism and instead focused on correlation.
  - "What was silently missing was Darwin, the chutes, and all the 'survival of the fittest.'...In supreme irony, what had started out as an attempt to mathematize the framework of the _Origin of Species_ ended with the essence of that great work being discarded as unnecessary!"[^5]
	  - [[Charles Darwin]]
- Pearl admits to "committing a cardinal sin of history writing" by adopting a hindsighted style with regards to Galton and Pearson.
  - But, he says that "there is no other way to understand how statistics became a model-blind data-reduction enterprise, except by putting on our causal lenses and retelling the stories of Galton and Pearson in the light of the new science of cause and effect. In fact, by so doing, he rectifies the distortions introduced by mainstream historians who, lacking causal vocabulary, marvel at the invention of correlation and fail to note its casualty&mdash;**the death of causation**"[^^6]

## Pearson: The Wrath Of The Zealot
- [[Karl Pearson]]
- Pearson viewed Galton's work as reducing causation to a special case of correlation (the case where the slope of the regression line (the correlation coefficient) is 1 or -1 and the relationship is deterministic).
- Pearson belonged to a school of philosophical thought called [positivism](https://en.wikipedia.org/wiki/Positivism)
  - [[Positivism]] puts forward the notion that information derived from sensory experience, interpreted through reason/logic, is the exclusive source of certainty
  - Pearson's belief in positivism brought along a belief that causation, because it is construed as an objective process that occurs in the world outside the human brain, could not have scientific meaning
  - "Meaningful thoughts can only reflect patterns of observations, and these can be completely described by correlations[...]Pearson was prepared to discard causation completely." [^7]
- It seems that Pearson's beliefs stemmed from a general view that science was [^8]
  - "in reality a classification and analysis of the contents of the mind..."
  - "In truth, the field of science is much more consciousness than an external world"
  - "Law in the scientific sense is thus essentially a product of the human mind and has no meaning apart from man"

## Sewall Wright, Guinea Pigs, And Path Diagrams

- [[Sewall Wright]]
- Wright studied at Harvard shortly after [Gregor Mendel](https://en.wikipedia.org/wiki/Gregor_Mendel)'s theories were rediscovered.
	- [[Gregor Mendel]]
- Where Mendel focused on peas, and Darwin on finches on the Galapagos, Wright focused on guinea pigs.
  - "Wright was an early advocate of the view that evolution is not gradual, as Darwin had posited, but takes place in relatively sudden bursts." [^9]
- Wright was trying to determine genes that affect fur color in guinea pigs while working at USDA.
  - Fur color appeared to violate Mendelian rules&mdash;it proved nearly impossible to breed an all-white or all-colored guinea pig.
  - According to Mendel, in-breeding should have eventually led to specific traits becoming "fixed"
  - "Wright began to doubt that genetics alone governed the amount of white and postulated that 'developmental factors' in the womb were causing some of the variations." [^10]
- Wright's major breakthrough was showing that, if we know certain causal quantities, **we can predict certain correlations in the data by a simple graphical rule.**
  - "It was the first bridge ever built between causality and probability, the first crossing of the barrier between rung two and rung one on the [[Ladder of Causation]]." [^11]
  - His diagrams implied that some correlations can indeed imply causation, using algebraic equations.
- In modern [[path diagrams]], path coefficients represent the results of a hypothetical intervention on the source variable.
- Pearl is arguing that the path diagrams should be viewed as a powerful computational device, because it provides a way to calculate correlations.
- Wright's ideas garnered a large amount of push-back, as Pearson's ideas [[02-from-buccaneers-to-guinea-pigs--the-genesis-of-causal-inference#Pearson The Wrath Of The Zealot]] were still very much in vogue.
  - The argument was still that "causation is simply perfect correlation."
- Wright pushed back against the criticism with absolute clarity on one point:
  - "You cannot draw causal conclusions without some causal hypotheses[...]you cannot answer a question on rung two of the Ladder of Causality using only data collected from rung one." [^12]
- "The focus of Wright's research, as well as this book, is representing plausible causal knowledge in some mathematical language, combining it with empirical data, and answering causal queries that are of practical value." [^13] [focus of the book]

## E Pur Si Muove (And Yet It Moves)

- One solace to Wright with his system, against all the criticism of the correlation crowd, was that he could answer questions that cannot be answered any other way.
- Pearl shows an analysis that Wright did where he investigated how much a guinea pig's birth weight is affected if it spends one additional day in the womb.
  - The obvious approach is to weigh pups that have spent 1 day longer in the womb compared to pups that spent one day less
    - The issue Wright identified was that there also seems to be a relationship with the litter size in that pups that are born later usually have fewer litter mates. This means that the causal relationship is more complex than just days in the womb
	- He used path diagrams to plot out the entire system, and the already-known affects of all the component pieces, such that algebra could be used to solve for the unknown pieces.
- Two lessons from this example:
	1. Causal analysis allows us to quantify processes in the real world, not just patterns in the data
	2. [[Path analysis]] allows us to draw conclusions about individual causal relationships by examining the diagram as a whole. "The entire structure of the diagram may be needed to estimate each individual parameter." [^14]
- **Why didn't Wright's path analysis find more widespread adoption in his time?**
	- "[[Path analysis]] requires scientific thinking, as does every exercise in causal inference. Statistics, as frequently practiced, discourages it and encourages 'canned' procedures instead. Scientists will always prefer routine calculations on data to methods that challenge their scientific knowledge." [^15]
- The promise of Wright's [[causal diagram]]s for the study of causality continued to not be realized until the 1990s.
- Wright wrote a paper in 1983 defending his approach from attack by mathematician [Samuel Karlin](https://en.wikipedia.org/wiki/Samuel_Karlin). Karlin had two main criticisms.
	1. Path analysis assumes that the relationships between two variables in a path diagram are linear, allowing a single number to be used to describe the relationship.
		- Non-linear theory was a few years around the corner
	2. He argued that the data already contain all scientific wisdom, in line with previous statistical thinking. This would mean that there is no reason to take into account the process that generated the data, we can arrive at true understanding with a "model-free" approach.
- Ultimately, Karlin and other statisticians insisted that we can fully understand correlative relationships just by examining the data. This is similar to how "big data" analytics endeavors operate now. What's missing is a discussion of the relative importance of various causes, which Pearl argues is necessary to get beyond the first rung of the Ladder of Causation.

## From Objectivity to Subjectivity -- The Bayesian Connection

- [[Path analysis]] should be based on the user's personal understanding of causal processes, reflected in the causal diagram.
- Causal analysis forces the user to make a subjective commitment. A causal diagram must be drawn that reflects a qualitative belief.
- "Where causation is concerned, a grain of wise subjectivity tells us more about the real world than any amount of objectivity."
- Pearl argues that most of the tools of statistics aim for complete objectivity, except for Bayesian analysis.

### Bayesian Analysis

- Prior Belief + New Evidence -> Revised Belief
- Gives the example of a coin that lands on heads on 9 out of 10 tosses
	- Traditional statistics would think that the coin wasn't fair, and bet with 9:1 odds that the next toss will be heads.
	- Bayesian statistics would consider prior knowledge about the coin.
		- Did it come from the local store, or from a shady character?
		- If it's an ordinary coin, then it probably doesn't have a 90% chance to land heads
		- If it came from a shady character, then the probability might be 90% that it'll land heads.
- Bayesian statistics gives us an objective way to combine observed evidence with prior knowledge.

[[03-from-evidence-to-causes--reverend-bayes-meets-mr-holmes]]
[^1]: p.55
[^2]: p.56
[^3]: p.61
[^4]: p.62
[^5]: p.63
[^6]: p.66
[^7]: p.67
[^8]: <https://archive.org/stream/grammarofscience1900pear#page/n7/mode/2up>
[^9]: p.73
[^10]: p.73
[^11]: p.75
[^12]: p.79
[^13]: p.79-80
[^14]: p.84
[^15]: p.84-85