# Statistics
Implementations of important measures and algorithms from scratch. 

The motivation for the implementations from scratch is that these are great ways to describe large amounts of data, and implementing them by hand is the best way to understand how they work. 

These functions can also be found in my python module `statistics.py`, and can be imported for any project. 

# Central Tendencies

Usually want some measure of where the data is centered. We can use...

## Mean
- average, good first glace at central tendency. 
- depends on every single point, sensitive to outliers. 
- sum of data divided by amount of data points:
```python
def mean(data: List[float]) -> float:
    # sum() and len() well defined since we have a list of floats. 
    return sum(data)/len(data)

mean(data) # returns mean of list of data. 
```

## Median
- less sensitive to extreme outliers, since it measures the halfway point of the data. 
- different functions for even and odd cases:
  - code includes underscore notation for *private* functions in python (only means to be called by our internal median function, not other users):
    - [discussion on "privacy" in python](https://stackoverflow.com/questions/1547145/defining-private-module-functions-in-python)
    - [more information on private methods](https://www.geeksforgeeks.org/private-methods-in-python/)

- my implementation of median: 
```python
def _median_even_case(data: list[float])-> float:
    # average of two middle elements in list:
    middle = int((len(data) / 2) - 1)
    low_mid = data[middle]
    high_mid = data[middle + 1]
    return (low_mid + high_mid)/2

def _median_odd_case(data: list[float])-> float:
    # just the middle of the data:
    middle = (len(data) / 2) - 1  # indexing starts at 0
    #print(middle)
    true_mid = data[math.ceil(middle)]
    #print(true_mid)
    return true_mid


def median(data):
    # TODO - validate that the list is sorted
    if len(data)%2 == 0:
        return _median_even_case(data)
    else:
        return _median_odd_case(data)
    return "invalid input! check the list"
```
- issue with this implementation is that it can only take in sorted input, so future additions must only allow sorted input or sort the input.

- TODO: add sorting sub-function to statistics package. 

### Quantiles

Generalization of the median
- median is the "half" quantile. it is the value under which $50%$ of the data lies. 

implementation of quantiles:

```python
"""
quantile:

input - a percent value, ex: 0.10 = 10%, which markes the percentile value, must be a sorted list!
output - the percentile in the dataset
"""

def quantile(data:list[float], p: float) -> float:
    # TODO - validate that the list is sorted
    p_index = int(p*len(data)) # get the interger marking the percentile in the data

    return data[p_index]


```
- as with the median, the list needs to be sorted, but we can implement this at a later time. 

## Mode

- less common but still useful
- counts the most common values in the dataset
- the output should be a list to account for the fact that two or more values could be tied for highest frequency. 


ideas for implementation number 1:

```mermaid

graph LR
    create_space --> add_to_bucket; 
    get_max_of_bucket; 

```

My first implementation of mode:

```python

def mode(data: list[float]) -> list[float]:
    modes = []
    value_frequencies = {}

    # keep the count in a dictionary
    for x in data:
        value_frequencies[x] = 0
        print(value_frequencies[x])
    
    for x in data:
        value_frequencies[x] += 1
        print(value_frequencies) # eureka!
    
    #print(max(value_frequencies.values())) # ok but how do i get its key

    for key in value_frequencies:
        if value_frequencies[key] == max(value_frequencies.values()):
            modes.append(key)
    print(modes, "are modes")
        
    return modes
```

Using `counter` I can write a cleaner version of the mode function:

```python
from collections import Counter

# TODO: implement Counter version
```

# Dispersion
- dispersion measures how spread out the data is
    - values near 0 mean data is not spread out at all, and large values signift it's very spread out. 

### Range
- simplest measure of dispersion is the range, here is my implementation of it:

```python

def data_range(data: list[float]) -> float:
    return (max(data) - min(data))
```
- range is like median in the way that the particular values of a dataset do not change it too much. 
- for example, a data set of all 0's and a data set of all 100's willl have the same range, they are both as undispersed as possible, despite having vastly different values. 
- also a data set like `{0,50,50,100}` has the same range as `{0,0,0,0,100}`, even though we think that the first set should be more dispersed. 

### Variance

another good measure of dispersion is variance

to implement it, we need the `sum_of_squares` function (TODO: can I implement this from scratch?)

```python
from linear_algebra.s
```


