- Refresh Repo
	- #+BEGIN_WARNING
	  ==Make backup(s) **before** doing this==
	  #+END_WARNING
	- Go to repo local folder
	- Right-click, open bash here
	- ```bash
	  git checkout --orphan last
	  git add -A
	  git commit -am "Repo Refresh"
	  git branch -D main
	  git branch -m main
	  git push -f origin main
	  git gc --aggressive --prune=all
	  ```