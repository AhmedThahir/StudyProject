tags:: #Visualization #Text

- Visualization of frequency of words
- # Implementation
	- ```python
	  pip install wordcloud
	  ```
	- ```python
	  import matplotlib.pyplot as plt
	  from wordcloud import STOPWORDS, WordCloud
	  ```
	- ```python
	  input_file = "evs.txt"
	  text = open(input_file, mode="r").read()
	  
	  wordcloud = WordCloud(
	      background_color="black",
	      width=1080,
	      height=720,
	      stopwords=STOPWORDS
	  )
	  wordcloud.generate(text)
	  ```
	- ```python
	  wordcloud.to_file("wordcloud_output.png")
	  ```