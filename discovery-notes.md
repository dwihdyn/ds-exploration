Question to ask :

- when Explore is enough ? (d6)
- what kind of descriptive analytics do kinesso and those 'analytics product provider' companies ? (d4)

Answers :

- OSEMN framework is an iterative process (NOT linear)
- obtain, scrub, explore, model, turns out get bad model
- get more data, or scrub better, or add/remove outliers whether it improve the model, etc
- make sure u check every distributions of each features. there could be a case where the reason why model gives more accurate result is solely because one feature has a unique distribution (parentom uniform, poisson, etc)
- TLDR, Explore is enough when model is already give a good train-test result. Just do these 3 checks (correlation check, add/remove outlier will affect model accuracy?, take note on each features distributions)

======

- Analytics Companies is honestly do research with focus group , and result share to client. thats all. nothing special

=====

- Boxplot is literally use to see whether we need to standardize/normalize the selected feature or not (Need to standard/normalize if alot of outliers)

- If got null data less than 10% of whole dataset, either dropna() OR drop those features that has too many null, but if more than that, the dataset is not deemed as a “good” dataset. In real world example, You might need to find more data from your team or from other sources

=====

Always scale your data before you put in inside the model. at worst, you will get same accuracy

Why ?
Purpose of scaling is to make sure that we can still bring in outlier data into the model without distorting the model result (since its way too far)

How ?
use StandardScaler() unless otherwise (eg : comp vision best using normalisation() because common practice)

=====

- random_state in [train_test_split](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html), is to make sure that we are fixed with a specific set of training data.
- if we dont put anything in random_state, what happen is that train_test_split will always takes different set of data on every run, hence we cant see whether the model is actually improving or not
- see this [notebook](https://github.com/dwihdyn/ds-exploration/blob/main/screenshots-samples-etc/random-seed-sample.ipynb)
  - if we dont state the random_seed, first run, the random_state could be 1, next is 37, and so on, which we have prove already in notebook that each random_state will gives out different set.
  - but as long as the seed is same, the training set data will always be the same, hence that way we can actually see whether our model improves or not

=====

- R-squared in linear regression :
  - accuracy on test data is SAME as R^squares
  - measure how close the data are to the line-of-best-fit
  - range between 0 to 1.
  - 1 means line fits perfectly with all datapoints, 0 vise versa

=====

NLP :

- unstructure data :

  - data that cant be stored in row & column (eg : audio, image)
  - use case : NLP

- Text preprocessing :
  - same as "Scrub" in OSEMN
  - once you build model, and model is bad, we might have to go back this step again to feature enginerring
  - steps text normalisation :
    - convert all letter in sentence to lowercase
    - covert numbers to word [ten to 10]
    - remove stop word (she, and, from the,...) or particular words (remove common terms like 'RT' in twitter)
    - tokenization (break whats remaining in the sentence into many words in that sentence)
    - n-grams combine tokens that must be combined,
      - eg :
        - 2-gram red apple, anti war
        - 4-gram thank you very much, national uni of singapore
  - method2 to scrub : stemming OR lemmatization : its a library that we input the whole sentence, and output tokenized letters from the inputSentence (output stem more machine-friendly, and lemmatization more human-friendly)
    - careful : eg sentence is "john run faster than ben", using stem OR lem will output as fast, not 'faster', which in this sentence is pretty crucial

=====

see more in dwi bookmarkPage > unstructured data & how to store them

metadata :

- data about the unstructure data that helps us explain it. in understandable format
- stored in mongoDB, firebase, neo4j (structured data stored in mysql, postgresql)

Types of unstructured data & where to store :

1. document : mongodb :

- type of document database that allow us to store data in JSON-like doc format
- dont need schema/database design beforehand (unlike mySQL)

2. column : hadoop hbase :

- column oriented non-relational database
- run on hadoop, store sparse dataset
- best for real-time dataset that has random read write access to large volume data (how long u stay on fb daily ?)

3. key value pair : redis (remote dictionary server) :

- serves as type of in-memory key method to store database
- best for retrieve data based on specific key at web server, & caching purpose to improve performance of our system

4. graph : neo4j :

- uses graph to extract added value to our data, where it shows different relationship between different elements in graph tables is defined by nodes & edges with those labels to indicate their relationship

=====

- Assigning binary column (eg : is_partner) from no yes to 0 1, this does NOT us saying that someone with partner have better chance just because we set yes as 1. we can just terbalik it yes no to 0 1, and yield same result. (model know already that 0 1 kind of data is binary, NOT weights. dont worry!)

- DO NOT ASSIGN WEIGHT DIRECTLY, just use get_dummies (onehotencoding).
  - its the ML model job to assign the weights, because we never know in the future (what we set as high weight now, does not mean in the future will stay true, future are very uncertain). assign weight DIRECTLY will lead to overfitting (high accuracy now, bad prediction towards live data)
  - For assigning weights to your model, wouldn’t that defeat the purpose of ML, since ML learns and assigns the weights onto itself? To improve your model you should adjust your parameters, threshold, etc. But you should avoid directly influencing what the model is learning on its own.
  - "but this method improved the accuracy on TEST dataset". chances this is overfitting. >90% accuracy on TEST dataset does NOT mean that it is a good model.

=====

- nltk vader compound value are min -1, max +1.

=====

- find a problem, and think of how to solve it using data science. NOT forcing a problem that the solution is using data science
- its COMPLETELY fine if the solution doesnt requires data science. some solution are way simpler to solve & not needed ot tough solution

=====

- DE get data ready, DA storytelling, DS predictions using ready-made packages, MLE build our own ML packages that best for our company

  - Hire DS first as they're jack of all trade
  - then DE, then DA, then MLE when need to create general analytical packages that can help ALL clients

- Churn Analysis works best for "subscription model" business. (odoo, netflix, etc)

- Webscraping good practices :
  - use cloud instances/virtualenv that allows you to use different IP
  - make sure the scraping behaviour are like human (not able to jump one page to other in matter of second)
  - webscrape ONLY if given website has no API services, best method is always been API

=====
