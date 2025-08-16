---
layout: post
title: Calculating the volume of the planets in our solar system
image: "/posts/edu-solar-system-large.png"
tags: [Python, Numpy]
---

In this post I'm going to run through Numpy in Python to quickly find all the volumes of the planets in our solar system.  I will then show that this can be done for 1,000,000 hypethetical planents in sub-second performance.  The performance for 1,000,000 planets is about the same as for 8 planets. Incredible!

The volume of an object can be calculated using the radius of the object with a simple formula.
volume = 4/3 * pi * radius cubed

Let's get into it!

---

First let's start by setting up a numpy 1-d array to hold the radii of all 8 planets. This will act as the basis for a simulateous calculation of volume. Volumes were collected from a google search.

```python
import numpy as np
# radii of all planets in order from mercury to neptune in km.
radii = np.array([2439.7, 6051.8, 6371, 3389.7, 69911, 58232, 25362, 24622])
```


Instead of using a loop we are going to do this in one smooth line of code that will make use of the amazing performance and capability of the C code under the hood of Numpy.

```python
# using real volumes of 8 planets.
start_time = time.time()
volumes = 4/3 * np.pi * radii**3
end_time = time.time()
print("Processing (seconds): ", end_time - start_time)
print(volumes)
>>> Processing (seconds):  0.0017011165618896484
>>> [6.08272087e+10 9.28415346e+11 1.08320692e+12 1.63144486e+11
 1.43128181e+15 8.27129915e+14 6.83343557e+13 6.25257040e+13]
```

Ok, pretty cool, but what if we had 1,000,000 planets.  Will Numpy perform just as well?

```python
radii = np.random.randint(1, 1000, 1000000)
start_time = time.time()
volumes = 4/3 * np.pi * radii**3
end_time = time.time()
print("Processing (seconds): ", end_time - start_time)
print(volumes)
>>> Processing (seconds):  0.00448298454284668
>>> [1.02265386e+09 9.63408343e+06 1.48658033e+09 ... 2.30956488e+09
 1.06747173e+09 1.95432196e+05]
```

Amazing! Numpy is incredibly fast. 1,000,000 calculations using floats done in 0.00044 seconds.  Wow

Let's talk about why this Numpy performs so well.  We could have done this a few different ways including using other data structures.  However, making use of Numpy arrays performs better because they can only hold one data type where as lists or tuples can hold multiple data types.  This difference is important because Numpy is able to send the entire task to the highly optimized C code that Numpy is built upon.  The result is a largest boost in computation speed versus a normal Python for loop in conjunction with a list where each element would need to be checked first for it's data type.

In conclusion, when you are in the situation of using large sets of a single data type, and performance is important then making use of Numpy is an excellent choice.






