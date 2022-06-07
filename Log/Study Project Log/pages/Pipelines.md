- # What?
  collapsed:: true
	- Systematic organization of required operations
- # Parts
	- ## Transformer
		- filter and/or modify data
		- `fit()` and `transform()`
	- ## Estimator
		- Learn from data
		- `fit()` and `predict()`
	-
- # Implementation
	- ## Libraries
		- ```python
		  from sklearn.linear_model import LogisticRegression
		  from sklearn.tree import DecisionTreeClassifier
		  from sklearn.ensemble import RandomForestClassifier
		  
		  from sklearn.model_selection import train_test_split
		  from sklearn.preprocessing import StandardScaler
		  from sklearn.decomposition import PCA
		  
		  from sklearn.pipeline import Pipeline
		  ```
	- ## Pipeline Used Here
		- Data Preprocessing by using Standard Scaler
		- Reduce Dimension using PCA
		- Apply Classifier
	- ## Initializing Pipelines
		- ```python
		  pipeline_lr=Pipeline([('scalar1',StandardScaler()),
		                       ('pca1',PCA(n_components=2)),
		                       ('lr_classifier',LogisticRegression(random_state=0))])
		  
		  pipeline_dt=Pipeline([('scalar2',StandardScaler()),
		                       ('pca2',PCA(n_components=2)),
		                       ('dt_classifier',DecisionTreeClassifier())])
		  
		  pipeline_randomforest=Pipeline([('scalar3',StandardScaler()),
		                       ('pca3',PCA(n_components=2)),
		                       ('rf_classifier',RandomForestClassifier())])
		  ```
		- ```python
		  pipelines = [pipeline_lr, pipeline_dt, pipeline_randomforest]
		  
		  # Dictionary of pipelines and classifier types for ease of reference
		  pipe_dict = {
		    0: 'Logistic Regression',
		    1: 'Decision Tree',
		    2: 'RandomForest'
		  }
		      
		  best_accuracy = 0.0
		  best_classifier = 0
		  best_pipeline=""
		  ```
	- ## Training/Fitting
		- ```python
		  # Fit the pipelines
		  for pipe in pipelines:
		  	pipe.fit(X_train, y_train)
		  ```
	- ## Results
		- ```python
		  for i,model in enumerate(pipelines):
		      print(
		        pipe_dict[i], "Test Accuracy:", model.score(X_test,y_test)
		      )
		  ```
		- ```python
		  for i,model in enumerate(pipelines):
		      if model.score(X_test,y_test)>best_accuracy:
		          best_accuracy=model.score(X_test,y_test)
		          best_classifier=i
		          best_pipeline=model
		          
		  print('Classifier with best accuracy:{}'.format(pipe_dict[best_classifier]))
		  ```