# Explanation of the files

* `train.json` contains crowdsourced paraphrase dataset based on Quebec government's FAQ for COVID-19. We added 2000 examples from the healthtap dataset for out of distribution data. 
* `validation.json` contains crowdsourced dataset, plus 2000 additional examples from the healthtap dataset. 
	- `validation_ONLY_QUEBEC_FAQ.json` contains examples only from the crowdsourced dataset. 
	- `validation_ONLY_HEALTHTAP.json` contains examples only from the healthtap dataset. 

