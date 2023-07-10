# Introduction to Variables: Variable Assignment - Lab

## Introduction
Now that we know about variables, we want to put them to use by associating them with some data.  Here, we will be using variables to store information related to a vacation that we would like to go on.

Just as before, we ask you to run the code and ensure that it matches what is commented out.

## Objectives

You will be able to:

* Assign and declare a python variable

## Assigning variables

Assign the string "January" to the variable `travel_month`, as that is the month we would like to travel.


```python
travel_month = None
```

> We start by setting the variable equal to the data type None.  As we know, `None` represents the absence of a value. Now we can take care of assigning the variable to something other than `None`.


```python
travel_month # "January"
```

Now let's assign a variable equal to the number of weeks that we would like to travel, 3. 


```python
number_of_weeks = None
```


```python
number_of_weeks # 3
```

UPDATE: we just learned that we can travel for a longer period of time. So, we need to reassign the `number_of_weeks` variable to 5.


```python
number_of_weeks # 5
```

Now that's more like it.

Finally, let's create a string that uses both of these variables to tell us how many weeks we will be traveling in our travel month. The string should read `"I will be traveling 5 weeks starting in the month of January"`. The process of using one or more variables as placeholders within a larger string is called **string interpolation**.  Interpolate the `num_of_weeks` and `travel_month` to get the correct string.

> **Remember:** We can interpolate strings in the following ways:
* "Start of string" + variable_to_interpolate_1 + "middle" + variable_to_interpolate_2 + "end of string"
* "Start of string {variable_1} middle {variable_2} end of string".format(variable_1=variable_to_interpolate, variable_2=variable_to_interpolate)
* f"Start of string {variable_to_interpolate_1} middle {variable_to_interpolate_2} end of string" 


```python
traveling_schedule = None
```

### Summary

Great! In this lab, we were able to get some more practice with storing information in variables through assignment and reassignment.
