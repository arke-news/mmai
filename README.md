# ARKE News Bias Classification [MMAI work]

## In the repo

- Bert_Capstone_Senator_Tweet_Scrape_DCF.ipynb / Capstone_Senator_Tweet_Scrape_JH.ipynb:
  - retrieve senator's tweets
  - data cleaning
  - data analysis
  - work towards extracting politically charged phrases
- ARKENEWS_BERT_DANIEL_FACI.ipynb:
  - Republican vs. not classification model
  - built on an outdated version of Tensorflow, requires update to Tensorflow 2.0
- 2nd_ModelArkenews.ipynb:
  - Democratic vs. not
  - built using PyTorch, up to date and recommended to use this one to retrain the Republican model with

## Data

`data.zip` contains `tweets.csv`, a processed copy of the tweet data used to train the existing models. This can be used to reproduce the models the MMAI team built by following the steps outlined in the notebook.

`data.zip` also contains `manifesto.csv`. This is the most up-to-date data (v2021a) from [the Manifesto Project](https://manifesto-project.wzb.eu/datasets). This is a collection of the election programmes for all political parties which have won 1 or more seats in a national election for 56 different countries (including the US and Canada).

More details on the dataset can be found [here](https://manifesto-project.wzb.eu/down/data/2021a/codebooks/codebook_MPDataset_MPDS2021a.pdf) and information on how the data is encoded and should be worked with can be found [here](https://manifesto-project.wzb.eu/information/documents/handbooks).

## TODO - integration

1. Build a new dataset, combining the tweets data with the manifesto data
   - in doing so, should be careful to encode both datasets in the same way - either by encoding tweets using the method, or decoding the manifesto data and re-encoding along with twitter data.
   - data should also be randomly shuffled such that tweets are mixed with manifesto data - don't want to train on tweets then test/validate on manifestos
2. Retrain provided models on hybrid data
3. Save model and/or host on a server
   - considering long training times, it would be wise to save the model!
   - model can be hosted behind an API that simply takes an article's text, feeds into the model, and returns the output

## Future Work

1. Hyperparameter tuning - I suspect there are better model parameters that could improve the model's performance further
2. Experimenting with other LLMs - consider testing out how models like GPT-3 perform on this task
   - using ensembling methods could also greatly improve performance
3. Better training data - a not so simple problem, which will likely have the biggest impact
   - [political speeches](https://justfacts.votesmart.org/)
   - also recommend training on articles; could mitigate bias of hand labelling by averaging the labels assigned by multiple people

Once more people start using the ARKE news platform, adding a feature for the user to label what they think the bias score for the article should be, then averaging all users rankings could be used to generate a constant stream of training data.

Averaging user opinions would theoretically eliminate bias, however the efficacy is largely dependent on the distribution of the user's biases. This only works assuming a normal distribution of users across the political spectrum. Assuming users are not normally distributed, you could just use a subset of users in the average calculation to achieve this.
