# Numpy lab

## Introduction

Numpy is one of the main libraries for performing scientific computing in Python. Using Numpy, you can create high-performance multi-dimensional arrays, and several tools to work with these arrays. 

A numpy array can store a grid of values. All the values must be of the same type. numpy arrays are n-dimensional, and the number of dimensions is denoted the *rank* of the numpy array. The shape of an array is a tuple of integers which hold the size of the array along each of the dimensions.

For more information on numpy, we refer to http://www.numpy.org/.


## Objectives

You will be able to:
* Create a Numpy array  
* Understand Subsetting  
* Understand Higher Dimensional Numpy Arrays 

To work with numpy arrays, you should import `numpy` first. The naming convention for `numpy` is to import it as `np`.

## Numpy array creation and basic operations


```python
None
```

Now, create your first numpy array. Often, one would create a list and then convert it to a numpy array. We will create a first numpy array containing the population of the 5 biggest american cities (in millions). The numbers are 8.6, 3.9, 2.7, 2.1 and 1.6 respectively. Store it in `city_pop`.

For your information, these cities are NYC, LA, Chicago, Houston and Philadelphia respectively.


```python
city_pop = None
city_pop
```

Look at the type of `city_pop` and confirm that it is a list.


```python
None
```




    list



now, convert `city_pop` to a numpy array and store it in `city_pop_np`


```python
city_pop_np = None
```

confirm the data type again


```python
None
```




    numpy.ndarray



Now we want to make the numpy array in a way that it reflects the population to the actual unit. You can easily do this by multiplying your entire array with 1000000. 


```python
city_pop_m_np= None
city_pop_m_np
```




    array([8600000., 3900000., 2700000., 2100000., 1600000.])



This was easy! Now let's look at another numpy array which stores the surface area of these five cities (in square miles). 


```python
city_size_np= None
city_size_np
```




    array([468, 503, 234, 627, 142])



We're interested in finding the population density for the four cities. This is one of the perks of numpy arrays: you simply divide the two arrays by each other!


```python
city_density_np = None
city_density_np
```




    array([18376.06837607,  7753.47912525, 11538.46153846,  3349.28229665,
           11267.6056338 ])



It is no surprise that NYC is very densely populated where the population density of Houston is much lower.

## Numpy array subsetting

Imagine you want to select certain elements from a numpy array. This can easily be done using square brackets. Now, go ahead and select the fourth element in the `city_density_np` array.


```python
density_houston_np = None
density_houston_np
```




    3349.282296650718



Similarly, you can use colons to select a range of items. Use a colon to select the first three densities.


```python
first_three_np = None
first_three_np 
```




    array([18376.06837607,  7753.47912525, 11538.46153846])



Next, we want to select the densities that are higher than 10000 and store them in the object `high_density_np`


```python
high = None
high_density_np = None
high_density_np
```




    array([18376.06837607, 11538.46153846, 11267.6056338 ])



great!

## Higher dimensional numpy arrays

`city_pop_m_np`, `city_size_np`, and `city_density_np` are one-dimensional numpy arrays. This is pretty straightforward, but can be verified by using the attribute `.shape`. 


```python
None
```




    (5,)



This indicates that we have a 1-dimensional numpy array with 5 elements. Now, let's group our three arrays together (population, then size, then density) and see what happens if we call `.shape` again.


```python
cities_np = None
cities_np
```




    array([[8.60000000e+06, 3.90000000e+06, 2.70000000e+06, 2.10000000e+06,
            1.60000000e+06],
           [4.68000000e+02, 5.03000000e+02, 2.34000000e+02, 6.27000000e+02,
            1.42000000e+02],
           [1.83760684e+04, 7.75347913e+03, 1.15384615e+04, 3.34928230e+03,
            1.12676056e+04]])




```python
None
```




    (3, 5)



This numpy array has 3 rows and 5 columns!

## Subsetting in higher dimensional numpy arrays

In higher dimensional numpy arrays, you can use subsetting as well. However, simply using square brackets with one entry will simply select rows. Let's see how it works.


```python
first_row = None
first_row
```




    array([8600000., 3900000., 2700000., 2100000., 1600000.])



Now how can we select a single element or a range of elements? There are two ways:
- you can either use two consecutive pairs of brackets, first one for row, second one for column
- you can also use a single pair of brackets and a comma as a seperator [row, column]

Now use these two methods consecutively to select the third element in the second row!


```python
None
```




    234.0




```python
None
```




    234.0



To select a full column, on the other hand, you can use a colon to denote that you want every element in the column. Select the population, size and density for the second city in the list (LA)


```python
la_all = None
la_all
```




    array([3.90000000e+06, 5.03000000e+02, 7.75347913e+03])



# Sources

http://cs231n.github.io/python-numpy-tutorial/#numpy

http://www.numpy.org/

https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-1-python-basics?ex=1
