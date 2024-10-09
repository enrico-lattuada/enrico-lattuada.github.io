---
title: Protecting NumPy arrays in dataclasses
date: 2024-10-09
math: true
# image:
#   placement: 2
#  caption: 'Image credit: [**John Moeses Bauan**](https://unsplash.com/photos/OGZtQF8iC0g)'
---

Picture this situation: you have a scientific Python software and you want to store your results and data as NumPy arrays in a dataclass.
You might want to keep it under lock and key to prevent meddling hands from messing with it.
But how do you truly protect your array from prying eyes and rogue modifications?

{{% callout note %}}
I here you. We are All Consenting Adults in Python. But you might want to prevent involuntary modifications of the array. In the end, however, if the users really wants to change the data, there is nothing you can do to stop them. So, don't be overly protective unless you see a strong reason to.
{{% /callout %}}

## The Dilemma

So here's the scoop: you've got your `dataclass` with a NumPy array snugly nested inside.

```python
from dataclasses import dataclass
import numpy as np

@dataclass
class SuperDuperResults:
    my_array: np.ndarray

# long and tedious calculations...
my_superduper_results = SuperDuperResults(
    my_array=np.array([1, 2, 3, 4, 5])
    )

print(my_superduper_results.my_array)

>>> array([1, 2, 3, 4, 5])
```

By default, the `my_array` property of the `SuperDuperResults` data class is accessible and modifiable by external code, which can lead to unintended changes and potentially break the encapsulation of the class.

```python
# a less interesting result
my_superduper_results.my_array = np.zeros(5)
print(my_superduper_results.my_array)

>>> array([0., 0., 0., 0., 0.])
```

You chose... poorly.

## Fortifying your fortress

Fear not, valiant coder! Using Python's property sorcery you can shield your NumPy array from unwanted meddling and keep it as snug as a bug in a rug within your data class confines.

```python
@dataclass
class SuperDuperResults:
    _my_array: np.ndarray

    @property
    def my_array(self):
        return self._my_array

# again, some long and tedious calculations...
my_superduper_results = SuperDuperResults(
    my_array=np.array([1, 2, 3, 4, 5])
    )
```

This nifty trick makes your array read-only from the outside, lending it an air of exclusivity that mere mortals dare not breach.
In fact, if a user tries to overwrite the array, an exception will be raised.

```python
my_superduper_results.my_array = np.zeros(5)

>>> AttributeError: property 'my_array' of 'SuperDuperResults' object has no setter
```

But hey, there's a catch - direct modification of the array's elements is still fair game.
Sneaky, right?

```python
my_superduper_results.my_array[0] = 100

>>> array([100, 2, 3, 4, 5])
```

## Locking down write access

To truly lock the gates and preventing any unauthorized scribbling on the array, wield the `writeable` flag like a mighty sword.
By setting it to `False`, any attempts to write to the array will be met with a ersounding _"Thou shalt not pass!"_ in the form of a `ValueError`.

```python
@dataclass
class SuperDuperResults:
    _my_array: np.ndarray

    @property
    def my_array(self):
        array_view = self._my_array.view()
        array_view.flags.writeable = False
        return array_view

# once more, some long and tedious calculations...
my_superduper_results = SuperDuperResults(
    my_array=np.array([1, 2, 3, 4, 5])
    )

# sneaky user trying to touch what should not be touched
my_superduper_results.my_array[0] = 100

>>> ValueError: assignment destination is read-only
```

## A cautionary tale

Before you ride off into the sunset, remember: the quest for privacy and encapsulation isn't limited to NumPy arrays alone.
Lists and other modifiable sequence objects also crave the protection you so valiantly provide.

So go forth, brave coder, and may your data remain forever secure!
