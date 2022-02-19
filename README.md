# Flask Stroke Predictor

In this application, we are using a Random Forest algorithm (other algorithms were tested as well) from scikit-learn library to help predict stroke based on 10 input features. We will use Flask as it is a very light web framework to handle the POST requests.
##### Input Features:
* gender
* age
* hyper tension
* heart disease
* ever married
* work type
* residence type
* average glucose level
* bmi
* smoking status

The dataset is from [Kaggle Stroke Prediction dataset](https://www.kaggle.com/fedesoriano/stroke-prediction-dataset)

# Architecture

![Image of Application Architecture](./static/images/architecture.jpg)

The above diagram is the cloud architecture of our stroke prediction system. Inside the cloud diagram we have our cloud services. The mongoDb Atlas database stores the cleaned kaggle stroke dataset that is loaded there. MongoDB Atlas retrieves the clean data to build the final model.  The final model file is pushed to Git Hub. We update our GitHub repo by merging the feature branch into the master branch and push up the changes. The changed part of the code of the website or layout will now be updated on GitHub. The 'Cloud Build' is set to manually deploy the code updates into the production flask container. Once this is done the changes will be seen on the website.

# Model
The best fit model was a Random Forest model that was trained and saved to disk. The rf_model_final4.pkl is the model compressed in pickle format.
[More on the modelling processes used.](https://github.com/hiamdebsi/ML-Stroke-Prediction)

# App
app.py has the main function and contains all the required functions for the flask app. In the code, we have created the instance of the Flask() and loaded the model. model.predict() method takes input from the request (once the 'compute' button from index.html is pressed) and converts it into an array. The results are checked for missing values and temporarily saved in a dataframe 'stroke_df'. This dataframe is passed to the model.predict() where the result is rendered back to the user as 'feedback' for the prediction of risk or not at risk.

# Deployment

* Deployment of the application is done through Heroku. Sign up is required. [Guideline](https://realpython.com/flask-by-example-part-1-project-setup/)
* An envrionment was created using conda. 
* Having the model, this application required: Python 3.7, Pandas, scikit-learn, pickle, gunicorn
* A requirements.txt file was created using : conda list -e |cut -d'=' -f1-2 |sed 's/\=/==/g' > requirements.txt
* A Procfile is created : the text shows where to find the app.py file. (gunicorn is needed)
* A runtime.txt file was created : to ensure installation of the correct python version for Heroku.
* Created the app in Heroku (limited space). Followed the instructions to release a github manual update application named https://stroke-predictor.herokuapp.com/
* Heroku will not load until all of the requirement packages are in place and within the storage guidelines.
* Follow any errors and try to reload the application until it is built and released.

Contributors: Hiam Debsi, Meme Guerrini, Sherry Kennedy, Emily Wang.

© 2022  All Rights Reserved.





