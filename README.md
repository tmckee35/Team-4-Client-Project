# Project 4: Newlight Technologies for FEMA    
Authors: Sarah Berner, Kenneth Lee, True McKee, Anna Pavlova

## Problem Statement:
Natural incidents occur on a daily basis, however only a subsection of those qualify as disasters. Those disasters can be reported via a variety of sources. The employees that need to be responding to these incidents do not have the time to do that and manually monitor and sift through all incoming information. We want to provide a way to alert these employees to relevant disasters allowing them to marshal the necessary.
 
## Executive Summary:

### Project Summary:
In order to accomplish this we developed a model to determine the validity of a (flood, to start) "worthy of response" disaster using an NLP model, which was fed into a function that led to the surfacing of the location of the incident. This was accomplished by using the NewsAPI to search for articles that were flood-relevant to train our model on and then using that model to create a function that pushed the relevant articles and locations to the relevant users.

### Background:

The data obtained was articles ranging from 11/5/2018 to 4/11/2019, using the NewsAPI - NewsAPI only allows querying six months into the past so we were limited to the aforementioned date range. 

- Of note: Floods (like many, but not all, disasters) are seasonal and relatively frequent. This was part of the reason we chose to focus on floods as a proof of concept instead of alternatives such as earthquakes or tornados.

For the purpose of this project we only searched for articles with the keyword of "flood" as we felt that a flood-related disaster was bound to use that term.  

### Process:

- Query NewsAPI for 1,000 articles using 'flood' as the keyword, searching the dates 11/5/2018 to 4/11/2019 and store those articles in a CSV
- Turn the resulting CSV into a dataframe and create a column labeled "flood_relevance"
- Utilize an iterave Data Cleaning/EDA process to drop missing columns, duplicates, and irrelevant words/sequences (such as removing words like "playing" that showed up because of "Now Playing" results) in order to determine the "true" relevant terms
- Manually search those articles, determine if the articles were relevant to our purpose and impute the appropriate 0 (if not relevant) or 1 (if relevant) into the "flood_relevance" column
- Run through several model variations to determine the most appropriate model to use
- Incorporate the best model (Random Forest) into a function to alert the relevant users
- Build a model that alerts the users of this application and tell them where the the incident is occuring and give them insight into the relevant article. This allows them to determine if the notice is relevant or is a false positive and marshall resources appropriately

This would be expanded upon in future iterations that looked for disasters that were non-flood related. 

These articles, numbering approximately 1,000, were used to train our model, which has since been set on unseen data and performed with an 92.5% accuracy score.

### Production Model, Function, and Reasoning: 

- The production function uses a Random Forest model to analyze the following:
   - Title of the article
   - Description (summary) of the article
   - Content of the article  
- A TFIDF vectorizer was used to vectorize the above content
- Removes standard English stop words and others as they are not descriptive to the issue at hand
- Uses a Random Forest model with the titles, descriptions, and total content as inputs and assigns a "flood_relevance" score of 0 or 1 to the incoming articles from the relevant news feeds. This is then passed to the function, which passes the relevant information from the relevant articles to the relevant user.

The model we settled on is a bit overfit, however we found it to be the most accurate at classifying unseen (new) articles.

### Data Dictionary:
|Feature|Description|
|---|---|
|**content**|The content of the article| 
|**description**|A summary of the article| 
|**publishedAt**|When the article was published| 
|**title**|The title of the article| 
|**source_name**|The source of the article (sources listed below)| 
|**flood_relevance**|1 means Flood Relevant; 0 means Not Flood Relevant|

### Data Sources:

We used NewsAPI as our Data Source - specifically using the "everything" parameter (instead of "top headlines").

We used the following sources:

[Washington Post](https://www.washingtonpost.com/?noredirect=on) 

[New York Times](https://www.nytimes.com/)

[Reuters](https://www.reuters.com/)

[NBC News](https://www.nbcnews.com/) 

[MSNBC](https://www.msnbc.com/)

[Google News](https://news.google.com/?hl=en-US&gl=US&ceid=US%3Aen)

[FOX News](https://www.foxnews.com/)

[CNN News](https://www.cnn.com/)

[CBS News](https://www.cbsnews.com/)

[ABC News](https://abcnews.go.com/)

[Associated Press](https://www.apnews.com/)

Please note that when this project was started the source keys were provided by NewsAPI but during the course of this project, the source keys were removed from public access. During the course of our project we would have liked to expand our sources but were unable to.
                    
## Limitations:

- Limited training data - NewsAPI only goes back 6 months
    - Additionally, sources was removed as a query-able field mid-project so we were stuck with a specific, non-expandable set of sources

- Indexing local news sources a massive undertaking

- Some disasters are relatively infrequent (e.g. earthquakes, tornados) so not many articles to train on


## Conclusions:

- Conclusion: Based off our implementation and testing of this model and function we feel we have achieved a "better than Google" result; using this model and the resulting function we are able to surface occuring/to be occuring flood disaster incidents on an automated basis that would be more applicable to a disaster response employee than simply searching something like "floods" or "disasters" using Google

## Next Steps:

- Turn the function into production application that runs automatically in background of user’s workflow

- Expand disaster recognition beyond floods

- Expand source info beyond NewsAPI (e.g. Local news sources)
# Team-4-Client-Project
