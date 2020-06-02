# Explanation of the files

* `train.json` contains crowdsourced paraphrase dataset based on Quebec government's FAQ for COVID-19. We added 2000 examples from the healthtap dataset for out of distribution data. 
* `validation.json` contains crowdsourced dataset, plus 2000 additional examples from the healthtap dataset. 
	- `validation_ONLY_QUEBEC_FAQ.json` contains examples only from the crowdsourced dataset. 
	- `validation_ONLY_HEALTHTAP.json` contains examples only from the healthtap dataset. 

# Explanation of the fields in the files

* `examples` : these are used to define questions entered by the users. 
	- `id` : unique idea for the example within the file. 
	- `source` : defines the source from dataset. E.g. `healthtap`. 
	- `question` : user entry for the question
	- `passage_id` : the id of the associated passage. 

* `passages` : These define the question-answer pairs, to which examples are associated. These also specify whether a particular example is in distribution, or out of distribution. 
	- `passage_id` : the unique id of the passage. 
	- `source` : defines the source from dataset. E.g. `healthtap`. 
	- `uri`: defines the uri from which the passage is taken. E.g. for the quebec faq, this points to the files of the scrape. 
	- `reference_type` : defines whether this is an entry for an In distribution (`faq`), or an out-of-distribution (`noisy-or-ood`) entry. 
	- `reference` : 
		- `page_title` : defines the highest level header of the webpage. Gives an idea on the topic, if present.
		- `section_header` : The ground truth question. 
		- `section_content` : The answer associated with the question. 
		- `selected_span` : Currently unused. 

