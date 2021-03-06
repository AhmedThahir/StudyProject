- # Research Name
  id:: 620ab120-88ef-4ee5-8832-be163ac8a663
  collapsed:: true
	- An Econometric Analysis of Sports Data
- # Literature Review
  collapsed:: true
	- ## Current Methods
	  collapsed:: true
		- ### Attributes
		  collapsed:: true
			- Onfield stats
			  collapsed:: true
				- Goals
				- Expected Goals
				- Points
				- Expected Points
				- many more
			- Mathematical
			  collapsed:: true
				- Pythagorean Expectation $\frac{x^2}{x^2 + y^2}$
				- Pezzali Score $\frac{ \text{my goal conversion rate} } { \text{opponent's goal conversion rate} }$
		- [[Data Type]]
		- Resources
		  collapsed:: true
			- Experiments
			- Simulations
			- Observational Data
	- ## Programming Languages
	  collapsed:: true
		- [[Python]]
		- [[Julia]]
		- [[R Programming Language]]
		- [[Octave]]
		- [[Scala]]
	- ## Tools
	  collapsed:: true
		- [[Spreadsheets ❌]]
		- [[Jupyter Notebook]]
		- Weka
	- ## Example Implementation
	  collapsed:: true
		- ![01.pdf](../assets/01_1644423481352_0.pdf)
		- [01.html](../assets/01_1644423030176_0.html)
	- ## Gaps
	  collapsed:: true
		- most of these papers talk about prediction, but not much on helping making informed decisions
		- statistics: i believe that current researches focus more on correlation rather than causation
		  collapsed:: true
			- football example
			  collapsed:: true
				- just because win% has high correlation with no of passes, doesn't mean that we have to increase it to win more
				- it could just be that winning teams pass more and not the other way around
				  collapsed:: true
					- for eg, if a team is winning by 3 goals, then obviously it will just pass the ball around to waste time
			- basketball example
			  collapsed:: true
				- just cuz 3 point accuracy for a random basketball player is 30% doesn't mean that a new player should adopt that
				- what if the reason the accuracy is that way is cuz only the good shooters take those shots
		- economics: i believe an economics perspective will help a lot
		  collapsed:: true
			- ==opportunity cost== of decision A over B
			- for example, in market value and the business side, the data that is available online is the absolute data, not the **real data**
			  collapsed:: true
			  real data means in relative terms; for example,
				- **Nominal income** = monetary income
				- **Real income** reflects the quantity of goods and services you can buy
				  $\frac{\text{nominal income}}{\text{average of prices of all goods and services bought}}$
- # Objective of my Research
	- ![analysis.png](../assets/analysis_1650024180461_0.png){:height 417, :width 603}
	- understand what a manager should devote their resources for and what not to do
	- causal analysis and econometrics
	  collapsed:: true
		- causal analysis
		  collapsed:: true
			- $E \big [y |\text{do}(x = a) \big]$ instead of $E \big [y |(x = a) \big]$
		- Economics - Sartaj sir
		- statistics - maneesha ma'am
	- choice of sport - football
	  collapsed:: true
		- basketball is a high scoring game, so accuracy of prediction will be greater??
		- but football > basketball?
		  collapsed:: true
			- global sport
			- more accessible data
			- larger scope; basketball is mainly popular cuz of NBA
	- test on current data and predict for upcoming world cup
	- analyze causally what is the most important factors
- # Methodology
  collapsed:: true
	- Datasets
	  collapsed:: true
		- Existing datasets
		  collapsed:: true
			- the ones provided by uni of michigan on coursera
		- Web Scraping from sites
		  collapsed:: true
			- stats
			  collapsed:: true
				- [Understat](https://understat.com)
				- [WhoScored](https://whoscored.com)
			- finances
			  collapsed:: true
				- [Capology](https://capology.com)
				- [Transfermarkt](https://transfermarkt.com)
	- Tools
	  collapsed:: true
		- Programming Language - Python
		- IDE - [[Jupyter Notebook]]