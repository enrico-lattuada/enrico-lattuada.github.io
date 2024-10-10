---
title: Protecting NumPy arrays within dataclasses
subtitle: Guarding your data with Python sorcery

summary: Explore how to fortify NumPy arrays within dataclasses using Python's property sorcery to prevent unauthorized modifications and maintain data integrity

projects: []

date: '2024-10-10T00:00:00Z'

lastmod: '2024-10-10T00:00:00Z'

draft: true

featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
# image:
#   caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
#   focal_point: ''
#   placement: 2
#   preview_only: false

url_slides: ''

authors:
  - admin
  
tags:
  - Python

categories:
  - tutorials

commentable: true
---

Imagine this scenario: you're a Python adept working on a scientific application where safeguarding data, stored as NumPy arrays within dataclasses, is paramount.
How can you ensure the sanctity of your data from potential meddling and unwarranted modifications?

{{% callout note %}}
I here you. We are All Consenting Adults in Python. While Python embodies transparency, defenses can be erected to discourage inadvertent array alterations. However, if the users really wants to change the data, there is nothing you can do to stop them. So tread the line of protection judiciously.
{{% /callout %}}

## The conundrum

Here's the situation: nested snugly within your `dataclass` lies a NumPy array.
Consider the risk this presents:

```python
from dataclasses import dataclass
import numpy as np

@dataclass
class SuperDuperResults:
    my_array: np.ndarray

# Extensive calculations unfold...
my_superduper_results = SuperDuperResults(
    np.array([1, 2, 3, 4, 5])
)

print(my_superduper_results.my_array)

>>> array([1, 2, 3, 4, 5])
```

By default, the `my_array` attribute of the `SuperDuperResults` dataclass is vulnerable to external modifications, potentionally jeopardizing the class' encapsulation.

```python
# A less favourable outcome emerges
my_superduper_results.my_array = np.zeros(5)
print(my_superduper_results.my_array)

>>> array([0., 0., 0., 0., 0.])
```

A decision misjudged.

## Enhancing your defence

Fear not, intrepid developer! Employing Python's property sorcery, you can fortify your NumPy array against unwarranted meddling, maintaining its integrity within the dataclass.

```python
@dataclass
class SuperDuperResults:
    _my_array: np.ndarray

    @property
    def my_array(self):
        return self._my_array

# Again, extensive calculations...
my_superduper_results = SuperDuperResults(
    np.array([1, 2, 3, 4, 5])
)
```

This nifty trick renders your array impervious to external alterations, lending it an air of exclusivity that mere mortals dare not breach.
Any attempt to overwrite the array will thus trigger an exception.

```python
my_superduper_results.my_array = np.zeros(5)

>>> AttributeError: property 'my_array' of 'SuperDuperResults' object has no setter
```

Yet, a caveat remains - direct element modifications still elude absolute protection.

```python
my_superduper_results.my_array[0] = 100

>>> array([100, 2, 3, 4, 5])
```

## Securing write access

For impervious fortification against unauthorized alterations, wield the `writeable` flag as a potent safeguard. Setting this flag to `False` erects an impenetrable barrier, thwarting any attempts at unauthorized array modifications.

```python
@dataclass
class SuperDuperResults:
    _my_array: np.ndarray

    @property
    def my_array(self):
        array_view = self._my_array.view()
        array_view.flags.writeable = False
        return array_view

# Once more, into the computing abyss...
my_superduper_results = SuperDuperResults(
    np.array([1, 2, 3, 4, 5])
)

# A sly user endeavors to tamper with the untamperable
my_superduper_results.my_array[0] = 100

>>> ValueError: assignment destination is read-only
```

## A final thought

Before steering into the horizon, ponder over this: the pursuit of privacy and encapsulation extends beyond NumPy arrays. Lists and other mutable sequence objects, too, covet the shield you valiantly provide.

So march forward, intrepid coder, and may your data remain eternally safeguarded!
