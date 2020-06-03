# covid_chatbot_data

Repository for the crowdsourced data for the COVID-19 chatbot project. 

## Note
You need git lfs installed to properly clone the files - see: https://git-lfs.github.com/

## Folder format
* `[date]_[province]_[language]_[cleaned|noisy]_collection_[collection_id+]` : these folders contain training files. (Including training results also)

	- Province field indicates which province is the file for.
	- Language field specifies the language of the data. 
	- The cleaned/noisy field indicates whether we applied manual cleaning or not. 
	- Date indicates the date of the scrape we are using.   
	- Collection number indicates the version of the collection we used to create this training data. There can be more than one collection. Also, it may contain additional information related to the folder.

# Explanation of the fields in the files

The files contain two sections: `examples`, which contains the user questions, and `passages`, which contains the FAQ passage extracted from the websites.

* `examples` : These are used to define questions entered by the users. 
	- `id` : Unique id for the example within the file. 
	- `source` : Defines the dataset source (e.g., Quebec FAQ website) where we should look for the associated passage.
	- `question` : Question from the user.
	- `passage_id` : The id of the associated passage. 

* `passages` : These define the question-answer pairs, to which examples are associated. These also specify whether a particular example is in distribution, or out of distribution. 
	- `passage_id` : The unique id of the passage. 
	- `source` : Defines the dataset source. I.e., where the passage has been extracted from.
	- `uri`: Defines the uri from which the passage is taken. Note it may point to a local copy if we scraped the data.
	- `reference_type` : Defines whether this is a in-distribution passage that can be used to match the user question (starts with `faq`), or if this passage is associated to out-of-distribution question (does not start with `faq`, e.g. `noisy-or-ood`).
	- `reference` : 
		- `page_title` : Defines the highest level header of the webpage. Gives an idea on the topic, if present.
		- `section_header` : List of headers for this passage. The last header in the list is used as the question that we try to match.
		- `section_content` : The answer associated with the question. 
		- `selected_span` : Currently unused. 

# How to use this data for training (or to measure accuracy).

This data can be used to train a prediction system able to 1) match a user question with a "master" question from a pool of "master" questions (e.g., question from a FAQ website), or 2) match a user question with the relative answer.

## Match a question with a master question.
Given an `example`, the associated `question` can be the input for the prediction system. To get the target, first find the `passage_id`, and use it to find the related passage in the `passages` list. At this point, there can be two options:
* The passage `reference_type` does not start with `faq`. This means that the question shold be classified as out-of-distribution (i.e., the system is not able to answer this question, possibly because out of topic, or too generic) from the prediction system.
* The passage `reference_type` starts with `faq`. Then the prediction system should associate the question to this passage FAQ question, which is the last element in the list `section_headers`.

## Match a question with an answer.
Given an `example`, the associated `question` can be the input for the prediction system. To get the target, first find the `passage_id`, and use it to find the related passage in the `passages` list. At this point, there can be two options:
* The passage `reference_type` does not start with `faq`. This means that the question shold be classified as out-of-distribution (i.e., the system is not able to answer this question, possibly because out of topic, or too generic) from the prediction system.
* The passage `reference_type` starts with `faq`. Then the prediction system should associate the question to this passage FAQ content, which is `section_content`.
