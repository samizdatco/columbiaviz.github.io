#### New Querying Interfaces

[Scalable](https://www.microsoft.com/en-us/research/uploads/prod/2019/01/Wu-drucker-QueryingVideos.pdf),
[Image](http://cidrdb.org/cidr2019/papers/p141-kang-cidr19.pdf),
[Databases](http://cidrdb.org/cidr2019/papers/p40-krishnan-cidr19.pdf) are on the horizon.  However, a major limitation is that the query interface is incredibly impoverished.  How do you specify that you want to find red cars that move along a trajectory?  Or to look for relationships between two objects over time?  Certainly not by writing SQL-like text queries.   The challenge is that video is fundamentally 3D, but query interfaces are 1D.  

* Idea 1: the core abstraction in relational algebra is Joins.  In video, it is likely also joins, but for the same image across video frames, or the relationship between objects across video frames.  The nature of trajectories, positioning, and timing are all core aspects to relating concepts in video.  Propose and implement a prototype to help users express video joins.
* Idea 2: VR can render videos as 3D objects.  What does a query language look like if designed for VR?  What types of joins, or filtering, make sense?  You should have VR experience.   


#### What We Talk About When We Talk About Data

How are data and analyses referred to and described in scientific work?  When data is presented as figures or tables, how is it referred to?  What are the verbs and nouns?  Is there a universal set of ways that figures are described (e.g., in terms of comparisons? in relative terms? ).  This can serve as the evidence for a new data analysis language.  

[ArXiV](https://arxiv.org/help/bulk_data_s3) releases dumps of the submitted papers.  Identify the papers that include latex source files, parse the documents to find the charts, captions, and references to those charts in the text.



#### Precision Interfaces

[Precision interfaces](https://www.dropbox.com/s/09ri46n9zcv7jxh/precisioninterface-ipa20-submitted.pdf?dl=0) analyzes query logs and generates custom interaction components from the logs.  The goal is to scalably generate dozens or hundreds of custom interactive analysis interfaces for any analysis found in a log.    

* Precision interfaces is currently language agnostic and does not take into account the database nor the database contents.   Adapting the system to make weak but general assumptions about the nature of query plans, data, and query results can potentially improve the usability and usefulness of the generated interfaces.  
* Visualization design algorithms such as Draco propose ways to measure the "appropriateness" and "effectiveness" of a visualization.  HCI research has studied UI complexity for software interfaces based on ideas such as GOMS and Fitt's law.    Given a candidate interactive visualization interface (views and interactions) as well as a "workload" of queries users want to express, devise an "interactive interface appropriateness" measure.


#### Vis

Core Data Processing for Viz

* **Request Probabilities:** instead of the typical request-response model of interaction, what if the client constantly sends probability distributions of what the user might do?  What if the server constantly sends data to the client at maximum bandwidth?
  * How does a data processing system execute a probability distribution of queries?
  * What data should the server send to the client?
* **Run studies:** What are humans able to perceive anyways?  Run perception studies to build user perception models that could be used for perceptual push-down. 
  * Related: [pfunk](http://sirrice.github.io/files/papers/pfunk-hilda16.pdf), [Section 3.2 of CIDR paper](https://www.dropbox.com/s/0rdjsv7m7wbhmlk/cidr17-camera.pdf?dl=1)
* Pick a class of visual analyses, and get it to scale to 10M+ points in the browser using [technologies such as Arrow.js](https://observablehq.com/@lmeyerov/rich-data-types-in-apache-arrow-js-efficient-data-tables-wit).  


#### Documents

* Public datasets (UCI ML data, government datasets) are often accompanied by description files that describe the attributes and the contents.  Automatically identify the segments in the description files that relate to attributes in the dataset, and create a tool for users to make use of these metadata files to assist them as they learn about a new dataset.    Make it work for some simple domains (datasets)

<!--

Run some perceptual studies:

*  What are humans able to perceive anyways?  Run perception studies to build user perception models that could be used for perceptual push-down. 
  * Related: [pfunk](http://sirrice.github.io/files/papers/pfunk-hilda16.pdf), [Section 3.2 of CIDR paper](https://www.dropbox.com/s/0rdjsv7m7wbhmlk/cidr17-camera.pdf?dl=1)


Modalities

* **Augment, not Replace:** I suspect that analysts don't want to perform NLP/voice-only data analysis, but would rather use voice to _augment_ their programming-based analysis?   For example, if the analyst asks "what's that?" then it probably has to do with the part of the visualization that the cursor is pointing to.  Survey existing human computer interaction literature on multi-modal approaches to data analysis (or run an informal user study) and build a prototype using Alex/NLP that _augments_ a data scientist's job.  Some ideas of what to augment:
  * While a user explores an interactive visualization, automatically zoom in, highlight data, generate new views, etc based on the user's comments.
  * Data science analysis session
* **Checklist Manifesto:** Customer service representatives (and most chat bots) follow a fill-in-the-blank rubric when communicating with users/customers.  The purpose is to extract the most information to solve your problem in the least amount of time.  Given a collection of chat logs, can you infer an optimized rubric?
* **Google Time:** With Google Maps, people can browse the world in their laptop. The aim of Google Times is to do the same thing, but for time instead of space. The project is made of two parts: 1. Extract as many dates as possible from public data sets, to obtain a huge database of dates, 2. Create a browsing system to explore this timeline in real time.
* **Audification:** While data visualization is well understood, its small cousin audification is still in its infancy [https://en.wikipedia.org/wiki/Audification] The aim of this project is to answer the question: what is the grammar of audification? What would the "Tableau of audio" look (sound) like? 

Explanation and Cleaning

* **But, Why?** Identify a context during data exploration (either in a visualization system, or via any other modality) where the user will natually ask "why?" and expect an explanation.  Formalize the context, formalize the problem and develop a prototype solution.
  * Prior examples: [Scorpion](http://sirrice.github.io/files/papers/scorpion-vldb13.pdf), [QFix](http://eugenewu.net/files/papers/qfix-sigmod17.pdf), [Dialectic](https://www.dropbox.com/s/9lgkbku2aa80fui/dialectic-icwsm17.pdf?dl=0)
* **Cleaning and Extraction Pushdown:** Data collected from the web (e.g., from a form) is typically used by downstream applications for a variety of purposes such as training data for models, or to analyze using queries.  However if the data is not collected and validated appropriately, then the analyst needs to perform expensive data cleaning to fix errors, or extract structured information from free-form text.  Is there a way, given the downstream applications or the existing data cleaning steps, to augment the input form so that the submitted data is already clean and in the appropriate form?    
  * Related to [Dialectic](https://www.dropbox.com/s/9lgkbku2aa80fui/dialectic-icwsm17.pdf?dl=0).
* **Will it Clean?** Even automatic error _detection_ is notoriously difficult due to the ambiguounotion of what "clean" means.  However in data science applications, the test data for the prediction model provides a crisp notion of "clean" and has been used in BoostClean to perform automatic error detection and cleaning.  BoostClean simply worked for simple static datasets: extend its ideas to streaming datasets where the errors may change over time.
* **Excel Sucks:** Many many very important datasets are shared as a big collection of excel files.  For example, the [Equality of Opportunity Project](http://www.equality-of-opportunity.org/data/) shares their data as 6 - 15 excel files for each category, and you end up needing to figure out how to download all of them, identify the schema, and join them together to even _start_ exploration.  Your project is to fix this.  Let me point to a website with links, get the excel files, automatically infer the joins (they may be at different granularities such as county and state!) to produce a single set of database tables to query.
  * data: [OECD](https://data.oecd.org/searchresults/?r=+f/type/datasets), [Equality](http://www.equality-of-opportunity.org/data/), [data.gov](http://www.data.gov)


Recommendations and Predictions

* **Causality and viz:** Recently, the ML community has made great progress in the field of causality detection, i.e., understand what variable causes another variable in a data set [see this paper](https://arxiv.org/abs/1412.3773). Can these methods help recommend interesting visualization views? 
  * Related: [Zenvisage](http://data-people.cs.illinois.edu/papers/zenvisage-vldb.pdf), [Voyager](https://idl.cs.washington.edu/papers/voyager), [Voyager2](https://idl.cs.washington.edu/papers/voyager2/)
* **Text and viz:** In many cases, datasets come with a text description of what they contain. For instance, UCI repo data often include a file that describes the columns. How can you mine this information to recommend interesting new visualizations? Can you make it better with external knowledge, e.g., a knowledge base or a Web crawl?  
* **Predicting crime:** You work for the FBI, you lead a team of 30 agents, and you just discovered this dump of dark web marketplaces:
https://www.gwern.net/Black-market%20archives
Where will you send your agents? 

-->

<!--

2. Win: pick an existing useful application and a well-recognized metric (latency, prediction, etc) and win against the state of the art.
3. Break and fix: implement a state of the art algorithm on real data, show that it doesn't actually work (results are poor, it's slow, etc), make it work.
4. Evaluate: there are many options out there, it's not clear which ones are actually best, and under what conditions.  Run a bake-off and evaluate.

#### Precision Interfaces

[Precision interfaces](https://www.dropbox.com/s/bac9qjz0s5m4kpx/precisioninterface-sigmod19-v2.pdf?dl=0) analyzes query logs and generates custom interaction components from the logs.  The goal is to scalably generate dozens or hundreds of custom interactive analysis interfaces for any analysis found in a log.    

* Precision interfaces is currently language agnostic and does not take into account the database nor the database contents.   Adapting the system to make weak but general assumptions about the nature of query plans, data, and query results can potentially improve the usability and usefulness of the generated interfaces.  
* Embed design heuristics into the interface generation process.  The system currently has a very simple model of "interface complexity" --- make it more real by taking existing HCI research into UI complexity and design into account.


#### Data Processing


#### Query-based Graph Visualization

Graphs are fundamentally high dimensional, and generating good graph visualizations is still an unsolved problem.  There are plenty of ways to visualize a graph---as a matrix, as a node-link layout (with many mayn layout algorithms), as histograms, and so on.  Suppose you know what analysis _queries_ (e.g., recursive SQL queries, or a query workload) have been run on the graph.  Can those queries be analyzed to recommend the appropriate visualization?


#### Data Cleaning

Understand how scientific articles use and talk about data.  Two possible directions:

Arachnid is a new explanation engine that automatically generates cleaning programs based on user specifications of data quality.  It is an extension to ideas from [Scorpion](https://www.dropbox.com/s/1v6dcb16r840sdo/scorpion-vldb13.pdf?dl=0).  Contact Eugene for a copy of Arachnid.  Some possible projects:

* Integrate Arachnid into an interactive data exploration interface in a way that the user can clean any part of a visualization without programming
* Implement a fast version of Arachnid in the browser


-->

