---
layout: post
title: Calculating the Volume of the Planets in Our Solar System
image: "/posts/edu-solar-system-large.png"
tags: [Python, Numpy]
---
In this post I'm going to run through NumPy in Python to quickly find all the volumes of the planets in our solar system. I will then show that this can be done for 1,000,000 hypothetical planets in sub-second performance. The performance for 1,000,000 planets is about the same as for 8 planets. Incredible!

The volume of an object can be calculated using the radius of the object with a simple formula:

volume = 4/3 * π * radius³

Let's get into it!

---

First, let's start by setting up a NumPy 1-d array to hold the radii of all 8 planets. This will act as the basis for a simultaneous calculation of volume. Radius values were collected from a Google search.

```python
import numpy as np
# Radii of all planets in order from Mercury to Neptune in km.
radii = np.array([2439.7, 6051.8, 6371, 3389.7, 69911, 58232, 25362, 24622])
