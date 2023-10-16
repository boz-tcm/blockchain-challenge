# Columbia Engineering FinTech Bootcamp 2023-06

> Project: Module 14 Algorithmic-Trading-Challenge

> Background: In this challenge, we assume the role of a financial advisor at one of the top five financial advisory firms in the world.  Despite our firm having heavily profited from algorithmic high-speed trading throughout its history, in recent years we have begun to struggle to adapt to new and changing markets.

> Purpose: The purpose of this challenge is to improve our existing algorithmic trading systems and maintain our firm's competitive advantage in the markets by enhancing our existing algorithmic trading signals with machine learning algorithms that have the ability to adapt to new data and changing conditions.

## Table of Contents
* [General Info](#general-information)
* [Technologies Used](#technologies-used)
* [Features](#features)
* [Screenshots](#screenshots)
* [Setup](#setup)
* [Usage](#usage)
* [Project Status](#project-status)
* [Room for Improvement](#room-for-improvement)
* [Acknowledgements](#acknowledgements)
* [Contact](#contact)
<!-- * [License](#license) -->

## General Information
- We examined a baseline algorithmic trading machine learning model, along with three tuned variations of the model designed to tune, or optimize, the model.  These four models are described below:

    1. Baseline model:
        - Characterized by an atypically short training period, comprising just over 3% of the entire in-sample dataset, and;
        - Short-term moving average ('Fast') and long-term moving average ('Slow') technical trading price signals with windows of 4 and 100 periods, respectively.
        - See: [machine_learning_trading_bot_baseline.ipynb](machine_learning_trading_bot_baseline.ipynb)
        - `Question: Write your conclusions about the performance of the baseline trading algorithm.`
        - `Answer: For the testing period from 2015-07-06 to 2021-01-22, the cumulative returns for the baseline strategy (SVM model) exceeded actual buy-hold returns by 9.44% (1.518/1.387), as shown below:`     
![Screenshot depicts baseline model cumulative returns](Images/1._algo_trading_svm_model_returns_baseline_plot.png)

            `From the perspective of performance, the baseline strategy returns appear on their face impressive, exceeding by more than 9% returns from a simple buy-and-hold strategy.  However, closer examination of the classification report for the model's testing data reveals the overall model accuracy was only 55%, or that only just over half the time the model was picking up the target trade signal (-1 target label defined as sell, +1 target label defined as buy).  The recall for the sell signal was particularly poor, with the model only picking up the sell signal 4% of the time.  The training window is unrealistically short at just 3 months, representing just over 3% of the in-sample trading data, and the indications or results are likely unreliable and a stronger indication and lesson of data mining than robust model performance.`

    2. Tuning. A training-period variation in the baseline model:
        - Increased the training period from baseline's 3 months to 6 months.  Despite the increase in the training period window, this still represents just a small fraction, 6.5%, of the in-sample data.
        - See: [machine_learning_trading_bot_modified_training_period.ipynb](machine_learning_trading_bot_modified_training_period.ipynb)
        - `Question: What impact resulted from increasing or decreasing the training window?`
        - `Answer: By increasing the training period from 3 months to 6 months, the SVM SVC model's strategy returns relative to the simple buy-and-hold increased to 21.34% (1.842/1.560) from the baseline's increased relative returns of 9.44% (1.518/1.387) cited above.  Again, this tuning is illustrating the effects of data mining and not necessarily a robust improvement in the model, as the accuracy only increased from the baseline model's 55% to 56% after doubling the training period, and the model performed even worse when recalling, or picking up, the sell trade signal. Cumulative returns for the increased training period window are shown below:`
        
            ![Screenshot depicts cumulative returns for a variation in the baseline model's training period](Images/2._algo_trading_svm_model_returns_mod_train_period_plot.png)

    3. Tuning. Strategy windows variation in the baseline model:
        - Decreased the slow-moving average window from 100 to 95 periods, while keeping constant the fast-moving average window at 4 periods.
        - See: [machine_learning_trading_bot_modified_strategy_windows.ipynb](machine_learning_trading_bot_modified_strategy_windows.ipynb)
        - `Question: What impact resulted from increasing or decreasing either or both of the SMA windows?`
        - `Answer: A number of combinations of increasing or decreasing either or both of the slow-moving and fast-moving simple average moving (SMA) windows was explored.  By decreasing only the slow-moving average window from 100 periods to 95 periods, while keeping the fast-moving window constant at 4 periods, the SVM SVC model's strategy returns relative to the simple buy-and-hold increased to 13.65% (1.574/1.385) from the baseline's relative returns of 9.44% (1.518/1.387).  The model's accuracy remained unacceptably low at just 55%, and the sell signal recall remains poor at just 5% (vs. baseline's 4%).  Cumulative returns for the decrease in the slow-moving window from 100 to 95 periods are shown below:`
![Screenshot depicts cumulative returns for a variation in the baseline model's strategy windows](Images/3._algo_trading_svm_model_returns_mod_strategy_window_plot.png)

    4. Combined tuning. Optimized model for combined variation of training-period and strategy windows parameters:
        - See: [machine_learning_trading_bot_modified_parameters_combined.ipynb](machine_learning_trading_bot_modified_parameters_combined.ipynb)
        - `Question: Save a PNG image of the cumulative product of the actual returns vs. the strategy returns, and document your conclusion in your `README.md` file.`
        - `Answer: The combined effect of doubling the training period from 3 to 6 months and decreasing the slow-moving window from 100 to 95 periods was to increase the SVM SVC's strategy returns relative to the simple buy-and-hold to 24.7% (1.976/1.584 = combined tuned strategy/buy-and-hold) from the baseline's increased relative returns of 9.44% (1.518/1.387).  Despite the increased return performance observed in the combined tuning, the accuracy remained unacceptably low at just 56% and the sell signal recall remained particularly poor at just 2%.  Cumulative returns for the combined tuned model is shown below:`
![Screenshot depicts cumulative returns for optimized model resulting from the combined variation of training period and strategy windows in the baseline model](Images/4._algo_trading_svm_model_returns_mod_parameters_combined_plot.png)

- We evaluated a base New Machine Learning Classifier to contrast with the base SVM SVC model.  Two alternative models were examined:
    
    5. AdaBoost Machine Learning Classifier (an ensemble adaptive learning model):
        - See: [machine_learning_trading_bot_baseline.ipynb](machine_learning_trading_bot_baseline.ipynb)
        - `Questions: Did this new model perform better or worse than the provided baseline model? Did this new model perform better or worse than your tuned trading algorithm?`
        - `Answer: The untuned AdaBoost ensemble adaptive learning model improved relative returns to 13.27% (1.571/1.381) from the SVM SVC baseline model's relative returns of 9.44% (1.518/1.387 = strategy/buy-and-hold).  The classification report scores remained poor at only 55% accuracy and sell signal recall at just 8%.  Although the AdaBoost model's returns (13.27%) were superior to the SVM SVC model's baseline returns (9.44%), the untuned AdaBoost returns (13.27%) were inferior to the combined tuned SVM SVC model (24.7%).  However, if consistency holds, we suspect a tuned AdaBoost model to outperform the tuned SVM SVC model.  The AdaBoost model's returns are shown below:`   
![Screenshot](Images/5._algo_trading_ada_model_returns_baseline_plot.png)

    6. Decision Tree Machine Learning Classifier:
        - See: [machine_learning_trading_bot_baseline.ipynb](machine_learning_trading_bot_baseline.ipynb)
        - `We also explored a Decision Tree model for the dataset.  Using the same parameters as the SVM SVC baseline model, we were surprised by the degree of difference between the Decision Tree model and the SVM SVC and AdaBoost models collectively.  From a return perspective, the Decision Tree model performed much worse, with a relative return in our iteration of -54.87% (0.626/1.387) versus the SVM SVC's baseline relative return of 9.44% (1.518/1.387).  The Decision Tree model's accuracy was also quite poor at just 45%, while interestingly the model's recall metrics flipped, with the sell signal recall now at 89% and the buy signal recall at just 11%.  The Decision Tree model's returns are displayed below:`
![Screenshot](Images/6._algo_trading_decision_tree_model_returns_baseline_plot.png)

    7. The Decision Tree for our Decision Tree Machine Learning Classifier Model is illustrated below:
![Screenshot](Images/7._algo_trading_decision_tree.png)

## Technologies Used
- Python Version 3.10.12
- Jupyter Notebook within VS Code IDE
- README markdown

## Features

## Screenshots
- [Refer to General Information Section](#general-information)

## Setup
- GitHub Repository
    - name: 'unsupervised-learning-challenge'
    - location: uploaded to Bootcamp homework submission online portal and available publicly at:
        - [GitHub Repository](git@github.com:boz-tcm/unsupervised-learning-challenge.git)
- Python Standard Library (Version 3.10.12)
- Python Libraries and Modules:
    - holoviews
    - hvplot.pandas
    - IPython.display and Image
    - matplotlib and pyplot
    - pandas
    - pandas.tseries.offsets and DateOffset
    - pathlib and Path
    - phantomjs
    - pillow
    - pydotplus
    - selenium
    - sklearn.ensemble and AdaBoostClassifier
    - sklearn.metrics and classification_report
    - sklearn.preprocessing and StandardScaler
    - sklearn.svm and SVC
    - sklearn and tree
    - tensorflow
    - tensorflow-metal
    - Installation packages reference for virtual environment .venv on Mac Silicon (M1), including tensorflow-metal:
        - https://developer.apple.com/metal/tensorflow-plugin/
    
- Jupyter Notebook(s):
    - [machine_learning_trading_bot_baseline.ipynb](machine_learning_trading_bot_baseline.ipynb)
    - [machine_learning_trading_bot_modified_training_period.ipynb](machine_learning_trading_bot_modified_training_period.ipynb)
    - [machine_learning_trading_bot_modified_strategy_windows.ipynb](machine_learning_trading_bot_modified_strategy_windows.ipynb)
    - [machine_learning_trading_bot_modified_parameters_combined.ipynb](machine_learning_trading_bot_modified_parameters_combined.ipynb)
- Data
    - [emerging_markets_ohlcv.csv](Resources/emerging_markets_ohlcv.csv)
- Images
    - location: [Images](Images)

## Usage
The scripts are run in the project's four Jupyter Notebooks cited in both [General Instructions](#general-instructions) and [Setup](#setup), located within the 'algorithmic-trading-challenge' repository's root directory, executed using the Notebook environments' command 'Run All Cells...'.

## Project Status
Project is: _complete

## Room for Improvement
Room for improvement:   _

To do:  _

## Acknowledgements

## Contact
Created by Todd C. Meier, tmeier@bozcompany.com - feel free to contact me!

<!-- ## License --> All rights reserved.