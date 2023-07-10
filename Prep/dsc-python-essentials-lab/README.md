# Python Essentials - Cumulative Lab

## Introduction

Congratulations, you made it through the new content for the first section of the prework! This cumulative lab will help you review and practice everything you've learned in this section — "putting it all together" into an analysis with real-world data.

## Objectives
You will be able to:

 - Recall the data types covered so far
 - Practice extracting information from a nested dataset
 - Practice generating insights with conditional logic

## Your Task: Analyze Amazon Review Data

For this lab we are going to be working with data collected by Computer Science researchers at the University of California, San Diego. Their full paper citation is here:
> **Justifying recommendations using distantly-labeled reviews and fined-grained aspects**
Jianmo Ni, Jiacheng Li, Julian McAuley
Empirical Methods in Natural Language Processing (EMNLP), 2019
[pdf](http://cseweb.ucsd.edu/~jmcauley/pdfs/emnlp19a.pdf)

We are using a cleaned-up sample version of their [full dataset](https://nijianmo.github.io/amazon/index.html), which contains over 200 million reviews of products on Amazon.com. Specifically, a subset of reviews from the Home and Kitchen category about coffee-related products.

![coffee preparation](images/coffee.jpg)

<span>Photo by <a href="https://unsplash.com/@kfred?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Karl Fredrickson</a> on <a href="https://unsplash.com/?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>

### Requirements

#### 1. Data Summary
Write code that describes the number of records (dictionaries) in the dataset, as well as the features (keys) contained in each record.

#### 2. Review Selection
Create a variable `review_index` that can be changed, so that your code will select any review from the collection in order to print out information.

#### 3. Review Summary

##### a. Positive, Negative, or Neutral
Print out information describing whether a review's rating is positive, negative, or neutral.

##### b. Review Year
Extract just the year from the review date

##### c. BONUS: Image
Use Jupyter Notebook functionality to display the first image from the review

## Data Summary

In the cell below, we've opened up the dataset and loaded it into a list of dictionaries called `reviews`.


```python
# Run this cell without changes
import json
with open("coffee_product_reviews.json") as f:
    reviews = json.load(f)
type(reviews)
```

In the cell below, delete `None` and replace it with appropriate code so the info printout is correct

(In other words: when you're done, you should have code to find the number of entries in the `reviews` list, i.e. the size or length of the list)


```python
# Replace None with appropriate code
num_reviews = None
```


```python
# Run this cell without changes
print("The coffee product review dataset contains {} reviews".format(num_reviews))
```

Ok, so now we know how many records we are working with! Let's investigate what each record looks like. In the cell below, replace `None` with appropriate code to select the first review


```python
# Replace None with appropriate code
first_review = None
first_review
```

Now we can check out the keys:


```python
# Run this cell without changes
first_review.keys()
```

Before looking at the answer below, try to identify: **what data type are all of these keys?**

.

.

.

*Answer: They are all strings. We can tell because they are surrounded by single quotes, e.g. `'rating'`)*

Now let's look at the values:


```python
# Run this cell without changes
first_review.values()
```

Before looking at the answer below, try to identify: **what data type are all of these values?**

.

.

.

*Answer: We have a mix of values* 
 - *The first one, `5.0`, is a float (no quotes or brackets, decimal place at the end)*
 - *The next four are strings*
 - *The fifth is a list. We can tell because it's surrounded by square brackets `[]`. Inside that list is a string.*
 - *The last one is a dictionary. We can tell because it's surrounded by curly braces `{}` and colons indicating key-value pairs. All of the keys and values are strings in this nested dictionary.*
 

Finally, let's look at the first five reviews, all at once:


```python
# Run this cell without changes
for index in range(5):
    print(reviews[index])
```

It looks like each review has the same structure as the first one.

Edit the string below to describe what we've learned about the dataset so far:


```python
# Replace <None> with an appropriate explanation
"""
For this analysis, we are using a dataset collected from <None> by <None>

Each record represents a <None>

There are a total of <None> records

Each record has <None> keys, all of which are type <None>

The values associated with these keys have mixed types: <None>, <None>, <None>, and <None>
"""
```

## Review Selection

Now that we have a general sense of what is contained in our dataset, let's implement a system for a user to be able to query for an individual record. For now, assume that the user can edit the value of a variable in this Jupyter Notebook.

In the cell below, create a variable called `review_index` and set it to the value of `2`

(Why are we bothering to use a variable, if we're just "hard-coding" it to 2? Because it's helpful to practice *parameterizing* our code, i.e. using variables that can have their values substituted rather than using the values directly.)


```python
# Your code here
```

Now let's use that review index to create a variable `selected_review` that extracts the relevant review dictionary from the list of review dictionaries


```python
# Replace None with appropriate code
selected_review = None
selected_review
```

## Review Summary

So far we have investigated the structure of our data, and written reusable code to extract a single review from the list. This allowed us to practice identifying data types and extracting information from nested lists and dictionaries.

Now it's time to practice two other key skills: **conditionals** and **string parsing** (and optionally, learn how to display images with Python code in a Jupyter Notebook).

We'll do this by **writing code to summarize a given review dictionary** in a more user-friendly way than the original raw dictionary format, practicing some data cleaning along the way.

### Positive, Negative, or Neutral

Using conditionals, let's display whether a given review is positive, negative, or neutral based on the value associated with the `rating` key. We'll use the following definitions:

 - Positive: `rating` value of 4 or 5 (out of 5)
 - Neutral: `rating` value of 3 (out of 5)
 - Negative: `rating` value of 1 or 2 (out of 5)

Once you've found that value, print out: `This is a <blank> review` where `<blank>` is replaced with either `positive`, `negative`, or `neutral`.

For example, with the current selection, the rating is 5.0, so we should print `This is a positive review`.

First, let's extract the rating from the `selected_review` variable:


```python
# Replace None with appropriate code
selected_rating = None
selected_rating
```

Now, in the cell below, write code using `selected_rating`, `if`, `elif` and `else` so that when `selected_rating` changes value, it will print out the right `This is a <blank> review` statement.

(Again, since the current value of `selected_rating` == 5.0, your code should print out `This is a positive review`, but your code should be able to print different statements when `selected_rating` changes value!)


```python
# Your code here
```

Ok, now that this worked for a single example, let's try it out on a few others.


```python
# Run this cell without changes
review_index = 4
selected_review = reviews[review_index]
selected_rating = selected_review["rating"]
```

Paste your code from above to analyze the new selection. This one should say it's a negative review.


```python
# Your code here (pasted from above)
```

Let's try one more, which should say it's a neutral review.


```python
# Run this cell without changes
review_index = 47
selected_review = reviews[review_index]
selected_rating = selected_review["rating"]
```


```python
# Your code here (pasted from above)
```

Great! We just practiced using conditionals to make a more user-friendly summary

### Review Year

While it may be less exciting than building machine learning models, a significant part of data science is data cleaning. Lets start to practice some data cleaning skills with the `review_time` key-value pairs.

For the rest of this lab, we'll go ahead and set up three variables to represent the positive, negative, and neutral examples above.

(Don't worry too much about this syntax; it uses "unpacking" and "list comprehensions", which we haven't covered yet.)


```python
# Run this cell without changes

selected_review_indices = (2, 4, 47)
positive_review, negative_review, neutral_review = [reviews[i] for i in selected_review_indices]
```

Now let's extract the `review_time` value from the positive review:


```python
# Run this cell without changes
positive_review_time = positive_review["review_time"]
positive_review_time
```

Ok, it looks like this is is a string showing the month, the day, and then the year that the review was written. Write code to extract the last 4 characters of the string, then convert it into an integer


```python
# Replace None with appropriate code
positive_review_year = None
positive_review_year
```


```python
# Run this cell without changes
# This should show `int`
type(positive_review_year)
```

Repeat the same logic for the negative review and the neutral review


```python
# Your code here for the negative review
```


```python
# Your code here for the neutral review
```

### Bonus: Images

(You can skip past this section if you want — this content will not be assessed.)

One of the reasons Jupyter Notebooks are such a powerful data science tool is that they allow you to do a bit of web development without learning a new language beyond Python and Markdown. This entire notebook is just a complicated web page, and the information you've been printing out so far means you are creating dynamic web elements with your code!

In addition to displaying the output of cells as strings of data, we can actually use Python to display images. We'll use the `Image` class from the `display` submodule of the `IPython` library, which is kind of like using the built-in `print` function to write text. There are a lot of other options in the `display` submodule that we won't cover, but you can read about them [here](https://ipython.readthedocs.io/en/stable/api/generated/IPython.display.html).


```python
# Run this cell without changes
from IPython.display import Image
```

Here is an example of using the `Image` class with a hard-coded image:


```python
# Run this cell without changes
Image('https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png')
```

Recall that our data contains links to images:


```python
# Run this cell without changes
positive_review
```

The image link is a string, contained in a list, associated with the key `images`, so we'll extract it like this:


```python
# Run this cell without changes
positive_review_image_url = positive_review['images'][0]
positive_review_image_url
```

Now we can plug that into the `Image` tool:


```python
# Run this cell without changes
Image(positive_review_image_url)
```

The same goes for the negative and neutral reviews:


```python
# Run this cell without changes
negative_review_image_url = negative_review['images'][0]
Image(negative_review_image_url)
```


```python
# Run this cell without changes
neutral_review_image_url = neutral_review['images'][0]
Image(neutral_review_image_url)
```

### Bringing It All Together

Now that we have individually extracted all of the relevant pieces, let's display a complete review summary based on a specified `review_index`

We'll use index `2` (the positive review) as an example, although someone using your notebook should be able to change just the value of `review_index` and the rest should automatically update.


```python
# Run this cell without changes
review_index = 2
```

The complete summary for index `2` should look like this:

```
"Bialetti is the Best!"
This was a positive review written by Karen in 2017. 
```

Optionally, it can also show the first associated image.


```python
# Your code here
```

## Conclusion

In this cumulative lab, you practiced some of the skills you've learned so far using real-world data. Starting from a nested list of dictionaries (which also contained other lists and dictionaries), you were able to extract and transform data into a new format.
