# TensorFlow and TensorBoard with Evaluation



## Purpose

The purpose of this lab is twofold.  

1.   to review using `TensorFlow` for modeling and evaluation with neural networks
2.   to learn about [`TensorBoard`](https://www.tensorflow.org/tensorboard)

`TensorBoard` is `TensorFlow`'s visualization toolkit, so it is a dashboard that provides visualization and tooling that is needed for machine learning experimentation. 

We'll be using the canonical [Titanic Data Set](https://www.kaggle.com/competitions/titanic/overview).

## The Titanic

### The Titanic and it's data



RMS Titanic was a British passenger liner built by Harland and Wolf and operated by the White Star Line. It sank in the North Atlantic Ocean in the early morning hours of 15 April 1912, after striking an iceberg during her maiden voyage from Southampton, England to New York City, USA.

Of the estimated 2,224 passengers and crew aboard, more than 1,500 died, making the sinking one of modern history's deadliest peacetime commercial marine disasters. 

Though there were about 2,224 passengers and crew members, we are given data of about 1,300 passengers. Out of these 1,300 passengers details, about 900 data is used for training purpose and remaining 400 is used for test purpose. The test data has had the survived column removed and we'll use neural networks to predict whether the passengers in the test data survived or not. Both training and test data are not perfectly clean as we'll see.

Below is a picture of the Titanic Museum in Belfast, Northern Ireland.


```python
from IPython.display import Image
from IPython.core.display import HTML 
Image(url= "https://upload.wikimedia.org/wikipedia/commons/c/c0/Titanic_Belfast_HDR.jpg", width=400, height=400)
```




<img src="https://upload.wikimedia.org/wikipedia/commons/c/c0/Titanic_Belfast_HDR.jpg" width="400" height="400"/>



### Data Dictionary

*   *Survival* : 0 = No, 1 = Yes
*   *Pclass* : A proxy for socio-economic status (SES)
  *   1st = Upper
  *   2nd = Middle
  *   3rd = Lower
*   *sibsp* : The number of siblings / spouses aboard the Titanic
  *   Sibling = brother, sister, stepbrother, stepsister
  *   Spouse = husband, wife (mistresses and fiancés were ignored)
*   *parch* : The # of parents / children aboard the Titanic
  *   Parent = mother, father
  *   Child = daughter, son, stepdaughter, stepson
  *   Some children travelled only with a nanny, therefore *parch*=0 for them.
*   *Ticket* : Ticket number
*   *Fare* : Passenger fare (British pounds)
*   *Cabin* : Cabin number embarked
*   *Embarked* : Port of Embarkation
  *   C = Cherbourg (now Cherbourg-en-Cotentin), France
  *   Q = Queenstown (now Cobh), Ireland
  *   S = Southampton, England
*   *Name*, *Sex*, *Age* (years) are all self-explanatory

## Libraries and the Data



### Importing libraries


```python
# Load the germane libraries

import pandas as pd
import numpy as np
import seaborn as sns 
from pandas._libs.tslibs import timestamps
import matplotlib.pyplot as plt
%matplotlib inline

from sklearn.preprocessing import StandardScaler

import tensorflow as tf
import keras 
from keras import models
from keras.layers import Dense
from keras.models import Sequential
from keras.losses import binary_crossentropy
from keras.wrappers.scikit_learn import KerasClassifier

# Load the TensorBoard notebook extension and related libraries
%load_ext tensorboard
import datetime
```

### Loading the data


```python
# Load the data

train = pd.read_csv('train.csv')
test = pd.read_csv('test.csv')

# We need to do this for when we mamke our predictions from the test data at the end
ids = test[['PassengerId']]
```

## EDA and Preprocessing

### Exploratory Data Analysis

It is your choice how much or how little EDA that you perform. But you should do enough EDA that you feel comfortable with the data and what you'll need to do to make it so that you can run a neural network on it.

It is prudent to investigate the attributes of the data frames, create visualizations, and perform data analysis.

### Preprocessing


```python
# Print the first rows of the train data

```


```python
# Look at the information regarding the train data

```


```python
# Print the first rows of the test data

```


```python
# Look at the information regarding the test data

```


```python
# Print the number of rows and columns in each data set

```

We notice that the total number of columns in the training data (12) is one more tha test data (11). The former has the "survived" column whereas the latter does not since that is what we want the neural network to be able to predict.

#### Visualizations

There are a number of plots that we could do. Here are a few with brief comments about each.


```python
# Histogram with survival and sex
sns.histplot(x='Survived', hue = 'Sex', stat = 'percent', data = train)
plt.show()
```


    
![png](index_files/index_26_0.png)
    


Since '0' represents not surviving and '1' represents surviving, then we can see that females were much more likely to survice than males.

And now let's look at survival by class (first, second, or third).


```python
# Histogram with survival and class
sns.histplot(x="Survived", hue = 'Pclass', stat = 'percent',  data = train)
plt.show()
```


    
![png](index_files/index_28_0.png)
    


While the differences between second and third class doesn't seem very diffrent, those in third class seem more likely to die.

We can see this more clealry in the next graph.


```python
# FaceGrid of Class and Survived with Age
grid = sns.FacetGrid(train, col='Survived', row='Pclass', height=2.2, aspect=1.6)
grid.map(plt.hist, 'Age', alpha=.5, bins=20)
grid.add_legend()
plt.show()
```


    
![png](index_files/index_30_0.png)
    


What conclusions can you draw from the above grid?

Finally, let's look at a heatmap to see which columns are correlated.


```python
# Heatmap
corr_train = train.corr(numeric_only=True)
sns.heatmap(corr_train)
plt.show()
```


    
![png](index_files/index_32_0.png)
    


What columns are correlated? Does this surprise you? Which columns are not correlated? Does this surprise you?

#### Data Analysis

Again there are a myriad of data analysis that we can do, but let's show some examples of what we may want to look it. Again, do as many as you think are appropriate and you should interpret the results explicitly.


```python
# Surival rate by sex 
((train.groupby(['Sex','Survived']).Survived.count() * 100) / train.groupby('Sex').Survived.count())
```

Females had about 74% chance of survival where as men had only about a 19%.

Now let's do the same, but with class as well.


```python
# Survival rate by class
(train.groupby(['Pclass','Survived', 'Sex']).Survived.count() * 100) / train.groupby('Pclass').Survived.count()
```

We can see that as the class increases, the likelihood of survivial increases; and again females are more likely to survive then males.

### Preprocessing

#### Missing Data

In order for our neural network to run properly, we need to see if we have any missing data... and if so, we need to deal with it.


```python
# Check for nulls in the train set

```


```python
# Check for nulls in the test set

```

So we have a decent amount missing data for *Age* in both the train and tests sets. There are also a couple from *Embarked* from the train set and one in *Fare* from the test set.


```python
# Performing preprocessing on the train and test data will be more effecient if we combine the two date sets.
# run this cell with no changes
combined = pd.concat([train, test], axis=0, sort=False)
```

There are different ways to deal with missing data, which we'll turn to next.

#### Combining numeric features and converting categorical feasture

One possibility for dealing with the missing data is to
*    fill the nan values for *Age* and *Fare* with the median of each respective column
*   the embarked column with the most frequent value, which is *S* for Southampton

Once we clean up *Age* we can create a variable from it called *Child*, that allows us to look at the data as adults or children.


```python
# run this cell with no changes
#Age column
combined['Age'].fillna(combined['Age'].median(),inplace=True) # Age

# Embarked column
combined['Embarked'].fillna(combined['Embarked'].value_counts().index[0], inplace=True) # Embarked
combined['Fare'].fillna(combined['Fare'].median(),inplace=True)

# Class column
d = {1:'1st',2:'2nd',3:'3rd'} #Pclass
combined['Pclass'] = combined['Pclass'].map(d) #Pclass

# Making Age into adult (1) and child (0)
combined['Child'] = combined['Age'].apply(lambda age: 1 if age>=18 else 0) 
```


```python
# view the current status of the combined dataframe

```

We have two categorical features, viz. *Sex* and *Embarked*. We need to make these numeric.

For *Sex*, let
*   Male = 0
*   Female = 1

For *Embarked*, let
*   Q = 0 (Queenstown)
*   S = 1 (Southampton)
*   C = 2 (Cherbourg)

If you did the heatmap above, you can see that there are some correlations between variables. You can choose modify the data set if you like. For the purposes of this exercise, we won't.

While the names of the individual passengers is not germane to our neural network model, the titles of the passengers may be worthwhile.


```python
# run this cell with no changes
# Break up the string that has the title and names
combined['Title'] = combined['Name'].str.split('.').str.get(0)  # output : 'Futrelle, Mrs'
combined['Title'] = combined['Title'].str.split(',').str.get(1) # output : 'Mrs '
combined['Title'] = combined['Title'].str.strip()               # output : 'Mrs'
combined.groupby('Title').count()

# Replace the French titles with Enlgish
french_titles = ['Don', 'Dona', 'Mme', 'Ms', 'Mra','Mlle']
english_titles = ['Mr', 'Mrs','Mrs','Mrs','Mrs','Miss']
for i in range(len(french_titles)):
    for j in range(len(english_titles)):
        if i == j:
            combined['Title'] = combined['Title'].str.replace(french_titles[i],english_titles[j])

# Separate the titles into "major" and "others", the latter would be, e.g., Reverend
major_titles = ['Mr','Mrs','Miss','Master']
combined['Title'] = combined['Title'].apply(lambda title: title if title in major_titles else 'Others')
```

Finally, we ned to drop the feature columns that we do not need for our model (`PassengerID`, `Name`, `Ticket`, and `Cabin`).


```python
#Dropping the Irrelevant Columns
combined.drop(['PassengerId','Name','Ticket','Cabin'], axis=1, inplace=True)

# Getting Dummy Variables and Dropping the Original Categorical Variables
categorical_vars = combined[['Pclass','Sex','Embarked','Title','Child']] # Get Dummies of Categorical Variables 
dummies = pd.get_dummies(categorical_vars,drop_first=True)
combined = combined.drop(['Pclass','Sex','Embarked','Title','Child'],axis=1)
combined = pd.concat([combined, dummies],axis=1)
```

#### Resplitting the data and scaling the data.

We need to split our data back into the training and test sets now that we have done all but one aspect of the preprocessing.


```python
# Separate the data back into train and test sets
test = None
train = None
```

We need to get the training data into the predictors and the predicted variables, and scale the data.


```python
# Training
X_train = train.drop(['Survived'],axis=1)
y_train = train['Survived']

# Scaling
sc = StandardScaler()
X_train = sc.fit_transform(X_train)
test = sc.fit_transform(test)
```

## Neural Network Model

### Building the model

#### Define the model as a pipeline

Let's use the data science pipeline for our neural network model.


```python
# It will help to define our model in terms of a pipeline
def build_classifier(optimizer):
    classifier = Sequential()
    # use classifer.add() to add layers
    # 
    # ... 
    #
    # use classifer.compile() as your last line of the definition; use loss='binary_crossentropy',metrics=['accuracy']
    return classifier

# Note: Do not use regularization methods or GridSearch. Those will be for next time!
```

#### Fitting the optimal model and evaluating with `TensorBoard`

#### `TensorBoard`

`TensorBoard` is `TensorFlow`'s visualization toolkit. It is a dashboard that provides visualization and tooling that is needed for machine learning experimentation. The code immediately below will allow us to use TensorBoard.

N.B. When we loaded the libraries, we loaded the TensorBoard notebook extension. (It is the last line of code in the first code chunk.)


```python
# Clear out any prior log data.
!rm -rf logs
# Be careful not to run this command if already have trained your model and you want to use TensorBoard.

# Sets up a timestamped log directory
log_dir = "logs/fit/" + datetime.datetime.now().strftime("%Y%m%d-%H%M%S")

# Creates a file writer for the log directory.
file_writer = tf.summary.create_file_writer(log_dir)


# The callback function, which will be called in the fit()
tensorboard_callback = tf.keras.callbacks.TensorBoard(log_dir=log_dir, histogram_freq=1)
```

    2023-06-06 22:34:46.172842: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  SSE4.1 SSE4.2 AVX AVX2 AVX512F FMA
    To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.


#### Fitting the optimal model and evaluating with `TensorBoard`


```python
# Using KerasClassifier

classifier = KerasClassifier(build_fn = build_classifier,
                             optimizer='Adam',
                             batch_size=10,
                             epochs=16)

# Fit the model with the tensorboard_callback
classifier.fit(X_train,
               y_train,
               verbose=1,
               callbacks=[tensorboard_callback])


# Warning: If verbose = 0 (silent) or 2 (one line per epoch), then on TensorBoard's Graphs tab there will be an error.
# The other tabs in TensorBoard will still be function, but if you want the graphs then verbose needs to be 1 (progress bar).
```

    Epoch 1/16


    /tmp/ipykernel_592/3357939647.py:3: DeprecationWarning: KerasClassifier is deprecated, use Sci-Keras (https://github.com/adriangb/scikeras) instead. See https://www.adriangb.com/scikeras/stable/migration.html for help migrating.
      classifier = KerasClassifier(build_fn = build_classifier,


    90/90 [==============================] - 1s 2ms/step - loss: 0.6158 - accuracy: 0.7093
    Epoch 2/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.4528 - accuracy: 0.8137
    Epoch 3/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.4232 - accuracy: 0.8238
    Epoch 4/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.4131 - accuracy: 0.8249
    Epoch 5/16
    90/90 [==============================] - 0s 2ms/step - loss: 0.4069 - accuracy: 0.8272
    Epoch 6/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.4027 - accuracy: 0.8316
    Epoch 7/16
    90/90 [==============================] - 0s 2ms/step - loss: 0.3998 - accuracy: 0.8350
    Epoch 8/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.3979 - accuracy: 0.8316
    Epoch 9/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.3943 - accuracy: 0.8406
    Epoch 10/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.3927 - accuracy: 0.8418
    Epoch 11/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.3913 - accuracy: 0.8350
    Epoch 12/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.3896 - accuracy: 0.8406
    Epoch 13/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.3873 - accuracy: 0.8440
    Epoch 14/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.3901 - accuracy: 0.8418
    Epoch 15/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.3878 - accuracy: 0.8440
    Epoch 16/16
    90/90 [==============================] - 0s 1ms/step - loss: 0.3846 - accuracy: 0.8429





    <keras.callbacks.History at 0x7fe4a61a2f80>




```python
# Call TensorBoard
import os
print(f"https://{os.getenv('SATURN_JUPYTER_BASE_DOMAIN')}/proxy/8000/")
%tensorboard --logdir logs/fit --port 8000 --bind_all     
```

#### Results and Predictions


```python
# results
preds = classifier.predict(test)
results = ids.assign(Survived=preds)
results['Survived'] = results['Survived'].apply(lambda row: 1 if row > 0.5 else 0)
results.to_csv('titanic_submission.csv',index=False)
results.head(20)
```

Continue to tweak your model until you are happy with the results based on model evaluation.

## Conclusion

Now that you have the `TensorBoard` to help you look at your model, you can better understand how to tweak your model.

We'll continue with this for the next lesson when we learn about model regularization.
