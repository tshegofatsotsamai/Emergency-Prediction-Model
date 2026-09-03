# Passenger Emergency Assistance Assessment

An AI-assisted passenger assessment system built using the Titanic dataset and a Decision Tree Classifier. The application uses passenger characteristics to estimate historical survival risk and translates the model's output into an emergency assistance level for crew briefing and evacuation-planning purposes.


## Project Overview

This project combines a machine learning model with an interactive web interface to demonstrate how passenger information can be used to support emergency-assistance planning.

The underlying model was trained on the Titanic dataset to classify whether a passenger survived or did not survive. The resulting class probabilities are then interpreted by the application as an indication of potential assistance requirements:

 **LOW** - standard evacuation procedures
 **MEDIUM** - additional evacuation guidance and monitoring
 **HIGH** - closer assistance and priority evacuation support

The web application allows users to enter passenger information and immediately receive an assessment, recommended actions, and an explanation of the model's decision path.


## Features

* Interactive passenger assessment form
* Decision Tree machine learning model
* Titanic dataset-based predictions
* Automatic family-size feature engineering
* Age and fare *Min-Max scaling*
* Sex *label encoding*
* Model confidence display
* Visual emergency-assistance gauge
* Recommended crew actions
* Basic model explainability through decision-path factors
* Responsive web interface
* No backend required. The fitted model logic is replicated directly in JavaScript


## Machine Learning Model - Decision Tree Classifier

Algorithm: Decision Tree
Criterion: Entropy
Maximum Depth: 3
Random State: 42


## Data Preprocessing

Before making a prediction, the application applies the same preprocessing used during model training.

### 1. Family Size

A new 'family_size' feature is calculated:
family_size = sibsp + parch + 1
This represents the passenger plus their siblings/spouse and parents/children aboard.

### 2. Numerical Scaling

'Age' and 'Fare' are transformed using *Min-Max Scaling* based on the training-data ranges.

scaled_age  = (age  - age_min)  / (age_max  - age_min)
scaled_fare = (fare - fare_min) / (fare_max - fare_min)

### 3. Categorical Encoding

The 'sex' variable is encoded using Label Encoding:
female = 0
male   = 1


## Explainable AI

One of the project's features is a simple explainability layer.

The application tracks the path a passenger takes through the Decision Tree and identifies the factors involved in reaching the final prediction.

The model can make decisions based on variables such as:

* Sex
* Passenger class
* Fare
* Family size
* Age

The interface then presents these factors as explanatory indicators to show why a particular assessment was produced.

For example, the application may communicate factors such as:

Female passenger
Higher passenger class accommodation
Lower fare bracket
Small or standard-sized family group

This provides users with more context than simply displaying a classification.


## Recommended Actions

The application translates the assistance level into suggested crew actions.

### HIGH

Recommended actions may include:

* Assigning a nearby crew member to accompany the passenger.
* Prioritizing the passenger for escort toward the nearest lifeboat.

### MEDIUM

Recommended actions may include:

* Providing additional evacuation guidance.
* Confirming the passenger understands their muster point.
* Checking on the passenger during the evacuation sweep.

### LOW

Standard evacuation procedures are considered sufficient by the application.

Additional rules can also trigger recommendations for passengers travelling in larger family groups or passengers in younger/older age ranges.


## Application Interface

The application provides two main sections.

### Passenger Details

Users can enter:

* Passenger class
* Sex
* Age
* Siblings/spouse aboard
* Parents/children aboard
* Fare paid

Family size is automatically calculated from the 'sibsp' and 'parch' values.

### Assessment Results

After submitting the passenger information, the application displays:

* Emergency assistance level
* Model confidence
* Passenger summary
* Recommended actions
* Explainability factors


## Technologies Used

### Machine Learning

* Python
* Scikit-learn
* Decision Tree Classification
* Min-Max Scaling
* Label Encoding

### Frontend

* HTML5
* CSS3
* JavaScript
* SVG

The current interface is implemented as a standalone HTML application and uses vanilla JavaScript to reproduce the trained model's preprocessing and decision-tree logic.


## Model Implementation

Rather than requiring a Python environment to make predictions, the fitted Decision Tree has been reproduced in JavaScript.

The implementation contains the learned tree nodes, feature thresholds, and leaf probabilities extracted from the trained model. This allows the browser-based application to follow the same decision logic without loading the original Python model at runtime.

The prediction process follows:

Input
  |
Preprocessing
  |
Feature Vector
  |
Decision Tree
  |
Leaf Probability
  |
Confidence
  |
Assistance Level
  |
Recommended Actions


## Limitations

This project should be understood as a **machine-learning demonstration and decision-support prototype**, rather than a validated emergency-management system.

### Real-world use

The recommendations generated by this prototype should not replace:

* Professional emergency procedures
* Crew judgement
* Accessibility assessments
* Safety regulations
* Real-time situational information


## Project Purpose

The primary purpose of this project is to demonstrate how a machine-learning classification model can be integrated into an interactive decision-support application.

It combines:

Machine Learning -> Prediction -> Explainability -> Decision Support -> User Interface
