# covid_chatbot_data

The repository for the crowdsourced data for the COVID-19 chatbot project. 

* `[date]_[province]_[language]_[cleaned|noisy]_collection_[collection_id+]` : these folders contain training files. (Including training results also)

	- Province field indicates which province is the file for.
	- Language field specifies the language of the data. 
	- The cleaned/noisy field indicates whether we applied manual cleaning or not. 
	- Date indicates the date of the scrape we are using.   
	- Collection number indicates the version of the collection we used to create this training data. There can be more than one collection.

