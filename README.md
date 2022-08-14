# ml_betting_models

This repository provides the supporting code for my paper `Machine Learning for Sports Betting: A Multi Sport Study`.

All project code is written in Python, and within the repository the following files can be found:
- `epl.csv`: contains the dataset of English Premier League matches, complete with formatted features
- `nba.csv`: contains the dataset of NBA matches, complete with formatted features
- `ufc.csv`: contains the dataset of UFC fights, complete with formatted features
- `UFC Scraping.ipynb`, `UFC Individual Fight Stats.ipynb` and `Fighter Info Scraper.ipynb`, which contain code that scrapes ufcstats.com to pull together the basis for a dataset for use in the model.
- `ML Models.ipynb`: contains the code implementing Logistic Regression, K Nearest Neighbours, Random Forest Classifier and Support Vector Machine algorithms for the three sports studied. These algorithms are implemented primarily using the `sklearn` library
- `Neural Networks.ipynb`: contains the code implementing a Neural Network algorithm for the three sports studied. These algorithms are implemented through use of the `sklearn` library along with `keras`, part of the `tensorflow` package

The structure of `ML Models.ipynb` is as follows:

1. The functions `extract_x`, `extract_y` and `extract_odds` are used to read in a csv file, and correctly separate the features used to compute a prediction, the outcomes themselves, and the real historical odds associated with those predictions, into three separate dataframes, regardless of which of the 3 dataset files is passed to the function.
2. Static variables are created to capture metrics of interest, and the algorithms themselves are defined
3. The function `run_model` takes a parameter of a model type, and the sport to evaluate. It then creates the appropriate train and test split, using 80% of the data for training, and the final 20% chronologically for testing. The model is then fitted using these values. A list of predicted values is also created based on the probability the model assigns to outcome A and outcome B. Finally, the function returns the 5 metrics that explain the performance of the model being evaluated, along with the prediction for each sample in Y test, the true result of each sample in Y test, and the probabilities assigned to each of the two outcomes.
4. Several functions are defined in order to calculate returns based on different betting strategies.
5. The function `predictions_dataframe` creates a dataframe of the predicted result, the true result, the probabilities assigned to each possible outcome, and is then joined with a dataframe of the historical odds, that was created in step 1. Finally, `df.apply` is used to create new columns in the dataframe calculating returns for each of the 4 betting strategies evaluated.
6. The function `betting_summary` takes the dataframe created in step 5 as a parameter, and returns printed statements that calculate the total amount bet (assuming $100 per unit bet), the total amount returned, and the profit/loss incurred as a result of the strategy.
7. Accuracy stats and betting results are then displayed for each sport, with each type of model shown in turn.

A similar structure is used for `Neural Networks.ipynb`, with a few notable differences:
1. Data is preprocessed using the `MinMaxScaler` function to transform it into a suitable format for insertion into a Neural Network.
2. The `generate_model` function creates Neural Networks of different shapes depending on the sport being analysed, and the number of features inputted to the model. Each has a single hidden layer, with a final layer of 1 output node, as the result being predicted is a binary decision.
3. 10 epochs are used for training the network.


