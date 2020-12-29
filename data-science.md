# Data Science Primer Intro + Machine Learning
## Important Concepts to Consider about ML
- How does this work in the real world?
- How much training data do you need?
- How is the tree created?
- What makes a good feature?

- if you want to get great results with machine learning, you must *develop a reliable systematic approach to solving problems*
- **Machine learning** is **not** about **algorithms**
    - it is a comprehensive approach to solving problems, algorithms are only a part of this process, where the rest of the pieces depend on *how you apply them*

Machine learning requires computers to teach themselves how to make decisions based on patterns from data
topic|definition
----|-----
model | a set of patterns learned from data
algorithm | a specific ML process used to train a model
training data | the dataset from which the algorithm learns the model
test data | new dataset for evaluating model performance
features | variables (columns) in dataset used to train model
target variable | specific variable you're trying to predict
observation | data points (rows) in the dataset

### Machine Learning Tasks
- a *task* is an objective for your algorithm
- algorithms can be swapped out
- you should *try* **multiple algorithms** bc you will not know which one will perform best
    - tasks are split into **supervised and unsupervised learning**
        - supervised learning includes tasks for labeled data
            - regression: modeling continuous target variables
            - classification: modeling categorical target variables
        - unsupervised learning includes tasks for unlabeled data
            - allow algorithm to learn patterns from the data
            - clustering: unsupervised learning and finds groups within your data
- ingredients for GREAT MACHINE LEARNING:
    1. a skilled chef; human guidance
    2. fresh ingredients (clean, relevant data)
    3. do not overcook (avoid overfitting)
- the *blueprint*:
    1. exploratory analysis
        - get to know the data, quick and effective
    2. data cleaning
        - clean data to avoid pitfalls
    3. feature engineering
        - help your algorithms focus on what is important by creating new features
    4. algorithm selection
        - choose most appropriate algorithms
    5. model training
        - train your models
    6. other steps
        - project scoping, data wrangling, preprocessing and ensembling

## Exploratory Analysis
- look for quick and effective data to use
- how many observations do I have?
- how many features?
- what are the data types of my features?
- do I have a target variable?

- get a feel for the dataset... Does everything make sense? Is there things that are missing that would be detrimental for later use?
## Data Cleaning
- better data over fancier algorithms
- remove *duplicate* or *irrelevant* observations
- fix structural errors: check for typos and/or inconsistent capitalization
- filter unwanted outliers
    - they are "innocent" until proven "guilty", so do not count them out automatically without fact-checking
- handle missing data
    - missingness can be INFORMATIVE
        - label this data as missing / flag the values and fill with 0 
## Feature Engineering
- create new input features from your existing ones
- think of it as process of addition compared to data cleaning which is process of subtraction
- think of information you want to isolate, it can be open-ended
    - create **interaction features** (two or more features together)
    - this can be products, sums, or differences between two features
- combine sparse classes
- remove unused features
## Algorithm Selection
- linear regression can be flaws
    1. it is prone to overfit with many input features
    2. it cannot easily express non-linear relationships
- use regularization to prevent overfitting
- types of regularized regression algos:
    - lasso regression
    - ridge regression
    - elastic-net
- tree ensembling:
    - bagging: attempts to reduce chance of overfitting complex models
    - boosting: attempts to improve predictive flexibility of simple models
## Model Training
- split the data, think of your data as a *limited resource*
- 
