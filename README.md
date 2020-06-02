# covid_chatbot_data

The repository for the crowdsourced data for the COVID-19 chatbot project. 

* `[date]_[province]_[language]_[cleaned|noisy]_collection_[collection_id+]` : these folders contain training files. (Including training results also)

	- Province field indicates which province is the file for.
	- Language field specifies the language of the data. 
	- The cleaned/noisy field indicates whether we applied manual cleaning or not. 
	- Date indicates the date of the scrape we are using.   
	- Collection number indicates the version of the collection we used to create this training data. There can be more than one collection.

# Explanation of the fields in the files

* `examples` : These are used to define questions entered by the users. 
	- `id` : Unique id for the example within the file. 
	- `source` : Defines the dataset source where the passage was extracted. E.g. `healthtap`. 
	- `question` : User entry for the question
	- `passage_id` : The id of the associated passage. 

* `passages` : These define the question-answer pairs, to which examples are associated. These also specify whether a particular example is in distribution, or out of distribution. 
	- `passage_id` : The unique id of the passage. 
	- `source` : Defines the source from dataset. E.g. `healthtap`. 
	- `uri`: Defines the uri from which the passage is taken. Note it may point to a local copy if we scraped the data.
	- `reference_type` : Defines whether this is a in-distribution passage that can be used to match the user question (starts with `faq`), or if this passage is associated to out-of-distribution question (does not start with `faq`, e.g. `noisy-or-ood`).
	- `reference` : 
		- `page_title` : Defines the highest level header of the webpage. Gives an idea on the topic, if present.
		- `section_header` : List of headers for this passage. The last header in the list is used as the question that we try to match.
		- `section_content` : The answer associated with the question. 
		- `selected_span` : Currently unused. 

