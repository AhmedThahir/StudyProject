tags:: #[[Panel Data]] 
alias:: Within Model

- Assumes that individual-specific effects are **dependent** on the regressors
	- $$
	  \text{Corr}(\alpha_i, X_i) \textcolor{hotpink}{\ne} 0
	  $$
- Drops variables independent over time, such as education
- # Steps
	- Find $\bar y_i = function$ (average of a person's salary over time)
	- Find $y_it - \bar y_i$
	- Run OLS