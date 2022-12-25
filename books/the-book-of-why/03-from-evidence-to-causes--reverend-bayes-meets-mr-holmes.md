## Bayesian Networks
- A [[causal diagram]] is a [[Bayesian network]] where every arrow "signifies a direct causal relation, or at least the possibility of one, in the direction of that arrow." [^1]
- [Bonaparte](https://www.bonaparte-dvi.com/) is a forensic tool that is used to identify victims of disasters using DNA from relatives and Bayesian networks.
- [[Bayesian network]]s are used in everyday applications
	- Speech-recognition software
	- Spam filters
	- Weather forecasting
	- Evaluation of potential oil wells
	- FDA's approval process for medical devices
	- Xbox game skill rankings
	- Belief propagation for cell phone signals
- Named, by Judea Pearl, after [Reverend Thomas Bayes](https://en.wikipedia.org/wiki/Thomas_Bayes) who wrote a paper that was posthumously published by [Richard Price](https://en.wikipedia.org/wiki/Richard_Price)
- Bayes' original question was "how much evidence would it take to convince us that something we consider improbable has actually happened?" [^2]
	- The import of his question held theological importance at that time, but the significance to causality is through the ability to deduce the probability of a cause from an effect.
- Pearl supplies the example of a pool table:
	- [[Forward probability]] is asking: given the length of a pool table, what is the probability of the ball stopping within $x$ feet of the end of the table
	- [[Inverse probability]] is asking: given that the ball stopped $x$ feet from the end of the table, what is the likelihood that the table is a given length?
- [[Forward probability]] is much easier to assess because it moves in the direction cause -> effect
- [[Inverse probability]] works in the opposite direction: given the effect, what is the likelihood of any given cause?

### [[Bayes's rule]]

- [[Teahouse example]]
- Suppose that 2/3 customers in a tea shop order tea
- Suppose also that 1/2 of customers who order tea, also order scones
- This means that 1/3 of customers order both tea and scones
- The starting point for [[Bayes's rule]] is to notice that we could have analyzed the data in reverse order
	- We could have observed that (given 12 customers) 5/12 ordered scones, and 4/5 of those customers also ordered tea.
	- With these numbers we can also compute that the proportion of customers who order both tea and scones is 1/3 --> (4/5) * (5/12) === 1/3
- $P(T)$ === probability that a customer orders tea
- $P(S)$ === probability that a customer orders a scone
- $P(S | T)$ === probability that a customer orders a scone given that they order tea
- $P(T | S)$ === probability that a customer orders tea given that they order a scone
	- First calculation could be expressed as --> $P(S AND T) = P(S | T) P(T)$
	- Second calculation could be expressed as --> $P(S AND T) = P(T | S) P(S)$
	- Because these are both equal to the same thing, they are equal to each other [[Euclid]] [[Euclidean geometry]]
		- This means that $P(S | T) P(T) = P(T | S) P(S)$
		- We already know $P(T)$ and $P(S)$, so if we have one of the other quantities, we can solve for the other.
- "We can estimate the conditional probability directly in one direction, for which our judgment is more reliable, and use mathematics to derive the conditional probability in the other direction, for which our judgment is rather hazy." [^3]
- [[Bayes's rule]] should be viewed "not just as a convenient definition of the new concept of 'conditional probabilty' but as an empirical claim to faithfully represent the English expression 'given that I know.'" [^4]
	- "It acts, in fact, as a normative rule for updating beliefs in response to evidence." [^5]

#### 2 Objections to [[Bayes's rule]]

- Philosophical Objection
	- This objection stems from the interpretation of probabilities as a degree of belief. Can we really translate the expression "given that I know" into the language of probabilities?
	- Pearl claims that we should view [[Bayes's rule]] as "an empirical claim to faithfully represent the English expression '**given that I know**'"
		- The argument is that the rule asserts "the belief a person attributes to $S$ after discovering $T$ is never lower than the degree of belief that person attributes to $S$ AND $T$ before discovering $T$"
		- It also implies that "the more surprising the evidence $T$&mdash;that is, the smaller $P(T)$ is&mdash;the more convinced one should become of its cause $S$." [^^6]
- Practical Objection
	- The practical objection is the role of subjectivity in the rule.
	- Going back to the example of a billiards table, someone who has never seen one of these tables in their life has no context for whether most tables are 10 feet, 20 feet, or 100 feet long.
	- He illustrates the solution to this practical objection with a long example discussing breast-cancer screening in 40-year-old women. [[Mammogram example]]
	- The thrust of the argument is that the relative risk of a patient having breast-cancer given a positive test is context dependent. 
		- Because the tests aren't perfect, there are bound to be false-positives.
		- Because the likelihood of the average 40-year-old woman having breast cancer is ~ 1 in 700, false positives can lead to more incorrect diagnoses than correct diagnoses
		- **The tiny number of true positives is overwhelmed by the number of false positives**
		- This illustrates the point that $P(disease | test)$ **is not the same for everyone**
	- Pearl's argument is that [[Bayes's rule]] tells us how to update our hypothetical beliefs in the real world.

### From [[Bayes's rule]] to [[Bayesian network]]s

- Between 1950 and the early 1980s, AI had struggled to formalize the process of inferential thinking. 
- During this period the use of [[expert systems]] organized knowledge as collections of specific and general facts, alongside inference rules connecting them. This worked in theory, but offered no way for the system to deal with inference in the face of uncertainty.
- "The computer could not replicate the inferential process of a human expert because the experts themselves were not able to articulate their thinking process within the language provided by the system." [^7]
- Pearl put forward the notion of representing probability as a network of loosely coupled variables passing messages between themselves, rather than huge probability tables.
	- This idea came from [David Rumelhart](https://en.wikipedia.org/wiki/David_Rumelhart)'s work studying how children read.
	- "The key point is that all the neurons are passing information back and forth, from the top down and from the bottom up and from side to side. It's a highly parallel system, and one that is quite different from our self-perception of the brain as a monolithic, centrally controlled system." [^8]
- The idea of [[belief propagation]] comes out of this message-passing structure if the system repeatedly applies these two rules to every node in the network:
	1. If the message goes from parent to child, the child updates its beliefs using conditional probabilities (like in the [[Teahouse example]])
	2. If the message goes from child to parent, the parent updates its beliefs by multiplying them by a likelihood ratio (like in the [[Mammogram example]])

### [[Bayesian network]]s: What Causes Say About Data

- We've already gone over "simple Bayesian networks" or two node networks:
	- Tea -> Scones
	- Disease -> Test
	- Hypothesis -> Evidence
- In contrast to [[causal diagram]]s, a [[Bayesian network]] carries no assumption that the arrow has any causal meaning. It only indicates that we know the [[Forward probability]]. [[Bayes's rule]] tells us how to reverse the procedure, "specifically by multiplying the prior probability by a likelihood ratio." [^9]
- After two node networks, we have three node networks or [[junction]]s
	- The three types of [[junction]]s "are sufficient for reading off all the independencies implied by a [[Bayesian network]], regardless of how complicated." [^10]
	- When examining these patterns, it is important to remember that if additional causal paths surround them, then these paths must also be accounted for.
	- [[Chain]]: $A$ -> $B$ -> $C$
		- Gives the example of Fire -> Smoke -> Alarm
		- The fire only causes the alarm to go off by way of smoke
		- The mediator ($B$) 'screens off' information about $A$ from $C$, and vice versa
		- We can 'condition on' a variable and only look at situations where, for example, Smoke is `true`. In that instance, Alarm will always be `true`.
			- In this example, we could say that Fire and Alarm are **conditionally independent**
	2. [[Fork]]: $A$ <- $B$ -> $C$
		- Here $B$ is called a common cause of [[confounder]] of $A$ and $C$
		- Gives the example of Shoe Size <- Age of Child -> Reading Ability (from [David Freedman](https://en.wikipedia.org/wiki/David_A._Freedman))
			- Kids with a larger shoe size tend to have better reading ability, but that is only because of their age.
			- If we condition on the age of child, then the correlation between shoe size and reading ability should disappear
	3. [[Collider]]: $A$ -> $B$ <- $C$
		- Gives the example of Talent -> Celebrity <- Beauty (from [Felix Elwert](https://sociology.wisc.edu/staff/elwert-felix-2/) and [Chris Winship](https://scholar.harvard.edu/cwinship/home))
		- "Here we assume that both talent and beauty contribute to an actor's success, but beauty and talent are completely unrelated to one another in the general population." [^11]
		- This pattern works in the opposite way to the prior two when we condition on the middle variable.
			- [[collider bias]] or the [[explain away effect]]:
				- If we hold celebrity `true`, then talent and beauty become related.
					- If we look only at famous actors, there will be a negative correlation between talent and beauty.
					- "Finding out that a celebrity is unattractive increases our belief that he or she is talented." [^12]
				- Ultimately this means that given the outcome Celebrity = `true`, talent and beauty are inversely related, **even though they are not inversely related in the population as a whole**
- "These three junctions&mdash;chains, forks, and colliders&mdash;are like keyholes through the door that separates the first and second levels of the [[Ladder of Causation]]. If we peek through them, we can see the secrets of the causal process that generated the data we observe; each stands for a distinct pattern of causal flow, and leaves its mark in the form of conditional dependences and independences in the data. In my public lectures I often call them 'gifts from the gods' because they enable us to test a [[causal model]], discover new models, evaluate effects of [[intervention]]s, and much more." [^13]

### Where is My Bag? From Aachen to Zanzibar

- In addition to diagrams and arrows, [[Bayesian network]]s also need [[conditional probability tables]]. Pearl calls these the 'fuel' of the [[Bayesian network]].
- The probability tables provide quantifiable data for the diagrams and arrows
- Gives the example of landing in Zanzibar after making a tight connection in Aachen, and waiting for your bag at the carousel. What are the chances that your suitcase did not actually make it onto the plane before leaving Aachen?
- Bag on Plane -> Bag on Carousel <- Elapsed Time
	- The bag must be on the plane to begin with
	- The more time elapses, the greater the probability that the bag will arrive at the carousel provided it was on the plane to begin with.
- To turn the diagram into a [[Bayesian network]], we must specify [[conditional probability tables]] to quantify each variable.
- We assume that the bags are unloaded from the plane at a constant rate
-  First, if the bag never made it on the plane, then no matter how much time passes the bag will never be on the carousel
- The interesting thing that can be examined with this approach is the inverse-probability: if $x$ minutes have passed and I still haven't gotten my bag, what is the probability that it was on the plane?
-  ![[Pasted image.png]]
-  This sort of computation is tedious to do by hand, and quickly can become too complex for even powerful computers.
-  It is important to reduce the complexity of the diagram under consideration and try to operate on 'sparse' networks

### [[Bayesian network]]s in the Real World

- [Bonaparte](https://www.bonaparte-dvi.com/index.php) uses DNA from distant relatives to assist in identifying victims of disasters.
	- Because we can't know which allele in the DNA of a victim comes from which branch of their ancestry, Bonaparte attempts to infer using belief propagation, updating the causal network as new information is added or learned.
	- Although Bonaparte is an elegant approach, at the end of the day it still depends on human intuition to make a determination. When its analysis is finished, it provides a ranking of the most likely identifications for each DNA sample, and the investigators then use other evidence and their own intuition to make a determination.
- Cell phone networks are another example.
	- Voice is encoded into binary, with some redundancy
	- [Claude Berrou](https://en.wikipedia.org/wiki/Claude_Berrou) created an error-correcting code that achieves near-perfect performance. Meaning the amount of redundant data is close to the theoretical minimum.
		- His approach used [[turbo codes]]
		- The idea is to encode each message twice, once directly and once after scrambling the message
		- By using [[Bayesian network]]s, you can analyze these duplicate messages and get a near-perfect accuracy rate

### From [[Bayesian network]]s to [[causal diagram]]s

- "[[Bayesian network]]s hold the key that enables [[causal diagram]]s to interface with data. All the probabilistic properties of Bayesian networks (including the junctions we discussed earlier in this chapter) and the belief propagation algorithms that were developed for them remain valid in causal diagrams." [^14]
- A [[Bayesian network]] is "literally nothing more than a compact representation of a huge probability table. The arrows mean only that the probabilities of child nodes are related to the values of parent nodes by a certain formula."
- The same diagram rendered as a [[causal diagram]] requires different thinking and interpretation.
	- We must determine which other variables each variable "listens to" before choosing its value
		- In chain example $A$ -> $B$ -> $C$, we say that $B$ *listens to* $A$ only
	- This means that causal relations are only derived from data, not invented at our whim
	- This also means the the graphical properties of the diagram determine "which causal models can be distinguished by data and which will forever remain indistinguishable, no matter how large the data." [^15]
- "The causal thinking that goes into the construction of the [[causal network]] will pay off[...]in the type of questions the network can answer. Whereas a [[Bayesian network]] can only tell us how likely one event is, given that we observed another (rung one information), [[causal diagram]]s can answer [[intervention]]al and [[counterfactual]] questions." [^16]
- The relationship between the diagram and the data allows us to perform 'experiments' without actually doing anything in the real world. Because we know that the causal relationships hold, they essentially become thought experiments.
	- I don't feel like I fully understand this, but this is his claim

[[04-confounding-and-deconfounding]]





[^1]: p.95
[^2]: p.97
[^3]: p.101
[^4]: p.103 
[^5]: p.103
[^6]: p.103
[^7]: p.109
[^8]: p.110
[^9]: p.113
[^10]: p.115
[^11]: p.115
[^12]: p.115
[^13]: p.116
[^14]: p.128
[^15]: p.130
[^16]: p.130