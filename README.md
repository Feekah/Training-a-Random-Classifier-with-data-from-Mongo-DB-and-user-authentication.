This user guide aims to explain the processes involved in training a random classifier to predict data. This would be demonstrated using a sample dataset gotten from Kaggle. The link to this data set is https://www.kaggle.com/competitions/titanic/data. We’ll be starting with a deeper overview of what the user guide aims to achieve, describe the program design and structure, then move on to explain how each function is implemented and how to use the program.

Bonus: In addition to the above, I’ll be implementing a GUI for the user to provide authentication to access the program. This would be done independently of the data preprocessing pipeline and is optional. The implementation is left till the end (Section 4)

Section 1: User guide overview
A) The data.

While I aim to guide the reader through training a random forest classifier, it is important to understand the dataset that would be used in training the model. Understanding includes what the model aims to predict, the nature of the data, how much cleaning needs to be done on the data, and how sufficient it is to train the model extensively; sufficient in this context means how many data instances the model has access to be trained on.

B) What needs to be predicted

The dataset to be used speaks to predicting whether a passenger survived the titanic shipwreck or not. It uses data such as gender, passenger class, age, and fares to train a random classifier on whether a passenger chosen at random survived or not. This is a classification problem which is why we intend to train a random classifier.

C) Process overview

As a process of training the random classifier, we’ll eventually create a python pipeline, detailing the process from downloading the sample data, feeding it into mongo DB, extracting it again, converting it to a data frame to eventually feeding the refined data into the model.

Section 2: Program Design and Architecture
The style used to write this program is the Object-Oriented Programing (OOP) approach, where each variable, function, and process is treated as an object. A better way to have a broad understanding of the OOP structure of this program is to use a Unified Modelling Language (UML) diagram which is seen below:


Figure 2: A Unified Modelling Diagram of the Object-Oriented architecture for the program
A) Libraries:

The libraries that we would be using throughout this process are listed in the format below:


Figure 3: Libraries needed for the program
B) Classes:

i) The program consists of one class: DataModelling, in which the __init__ method and other functional methods are housed. This is depicted in the UML diagram in figure 2.

ii) The attributes and methods of the class are accessed by the program via calling on the main function.

iii) The main function, not embedded in the class, is eventually called in the main program.

iv) All functions called by the main function eventually feedback their return values into the main function as depicted in the flow diagram below (Figure 6)

C) Attributes:

The attributes declared in the class DataModelling are outlined and described in the diagram below:


Figure 4: Defining the class attributes
D) Methods:

The methods (also known as functions) are defined within the class, and each attribute from the class is accessed using the self.<attribute name>. Each method within the class will eventually be called by the main function for it to be activated. A function can only be made active via a call. The methods of the DataModelling class are as below:


Figure 5: Methods of the class
E) Program flow:


Figure 6: The flow diagram describing the program components and process
i) The program is run

ii) The main class is called

iii) In the main class, a client object that connects with the mongo dB server is created.

iv) In the main, a collection for the train and test data is created in the mongo DB.

v) The main also loads the test and train data as CSV and converts them to JSON format to be loaded into the collection created in step (iv)

vi) In the main, an instance of the data modeling class is created and called

vii) Once the class is instantiated, we can proceed to call the respective methods of the class

viii) The create_database function is called, which loads the JSON data into the pre-created collections. In the future, the database and its collections could also have been created in the create_database function.

ix) The import_collection method is called, to load the JSON data back into the program

x) The convert_collection_to_dataframe method is called to convert the imported JSON data in step (ix) into pandas’ data frames

xi) The data_gathering_and_understanding function is called to print info about the test and train data frames for understanding purposes.

xii) The exploring_data_and_preparing_for_analysis method is called to explore the data, merge the test and train data, prepare the data by filling in missing values, convert categorical data to numerical data, re-splits the data into test and train, as well as separate the target variable from the train data, then returns the resulting data to the main function.

xiii) The data visualization method is called to visualize a count plot of the target variables we intend to predict; in our case, the number of people who survived and did not survive the titanic shipwreck.

xiv) The model_fitting method is called to further split the data, for model fitting purposes, then fits the train data into the Random classifier model. It also uses the resulting test data to test the dataset, predict the probability of the target variable being 1, and returns these outcomes to the main function.

xv) The model_evaluation function is called to evaluate the accuracy, F1 score, and roc_auc score of the trained model. They make use of the predicted values for the test data and compare them with the actual values. The accuracy measures how many values, both positive and negative were correctly classified. The F1 score is the harmonic mean of precision and recall.

xvi) The print_results function is called to print the model evaluation results gotten in step (xv)

The video of my program can be viewed by clicking the link below or Here

Google Drive: Sign-in
Access Google Drive with a Google account (for personal use) or Google Workspace account (for business use).
drive.google.com

Section3: Program Implementation:
The main function contains the code below:


a) Creating the database, and collections: This steps assume that mongo DB is already set up and running on the computer. If not, Here is a link to the mongo DB official site to set those up. After this, I proceed to create a client object that would connect to the database, create a database itself, then create a collection to store the test and train data:


b) Import the test and train CSV data into a data frame:


c) Convert the data frames to JSON format so they can be read into the mongo DB collections:


d) Insert the JSON data into the collections created in (a):


e) Import the collections from the DB back into the program:


f) Convert the imported data to data frames:


g) Now that we have our data frames back, we now move to data cleaning and preparation as seen below:


h) Now that we have cleaned our data, we can now feed it into the classifier:


i) We can evaluate our model and print out the results:


j) i) This step is just to print out the results of the steps outlined above in the model evaluation phase:


Results:

Accuracy: 0.7653631284916201

F1 Score: 0.7123287671232876

ROC AUC Score: 0.8418987341772153

In the future, we aim to improve accuracy by trying out other methods of replacing missing values, encoding, using more features, etc.

Section 4: GUI Implementation
The GUI implementation is dependent on what we want the user to see; so I sketched how I wanted the GUI to be designed:


From above, we see that the GUI has four frames, minus the heading. This explains how many frames we would be constructing, and the kind of widgets to be used. I’ll be posting the code for each frame alongside the comments to explain what each line of code does.

Note: The implementation follows OOP as well, so we’d be having a class, and three methods:

A): Creating the class, main window, and setting the GUI title:


B): Creating the widgets for each frame:


C): Packing the widgets:


D): Packing the Frames:


E): Entering the main loop of the Tkinter for execution:


F): Creating the function to check if the username and password are correct: In this case, we want the main function to execute.


G): Creating the Reset function to reset user input to zero when the “Continue” or “Reset” button is clicked:


H): Instantiating the class:


After running the program, this is how the GUI should look like:


The code above can be used to protect your code from being accessed.

Thanks.
