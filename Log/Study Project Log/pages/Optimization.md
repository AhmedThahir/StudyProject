- # Aim
	- Minimize Cost and/or Maximize Profit
	- It's literally the essence of [[Economics]]
- # Implementation
	- You can incorporate with pandas to make this even more dynamic
	- ```python
	  from gekko import GEKKO
	  m = GEKKO()
	  ```
	- ```python
	  # Variables
	  
	  x1 = m.Var(
	      integer = True,
	      lb = 5,
	      ub = 100
	  )
	  x2 = m.Var(
	      integer = True,
	      lb = 5,
	      ub = 100
	  )
	  
	  X = [x1, x2]
	  ```
	- ```python
	  # Constraints
	  
	  m.Equation(
	      x1 + x2 <= 100
	  )
	  
	  m.Equation(
	      x1**2 <= 100
	  )
	  ```
	- ```python
	  # Objective Function(s)
	  
	  def revenue():
	      return 2*x1 + 2*x2
	  
	  def cost():
	      return x1 + x2
	  
	  m.Maximize( revenue() )
	  m.Minimize( cost() )
	  
	  # equivalent to
	  
	  def profit():
	      return x1 + x2
	  
	  m.Maximize( profit() )
	  ```
	- ```python
	  # Solving
	  
	  m.options.IMODE = 3
	  # Steady State solution - solution does not change over time
	  
	  m.solve(disp = False)
	  
	  optimized_value = -m.options.OBJFCNVAl
	  # remove - if you're minimizing
	  ```
	- ```python
	  # Display
	  
	  for index,x in enumerate(X):
	      print(
	          "x" + str(index+1) + " =",
	          x.value[0]
	      )
	  
	  print(
	      "Optimized Value =", optimized_value
	  )
	  ```