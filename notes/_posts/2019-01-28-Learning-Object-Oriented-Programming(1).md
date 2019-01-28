---
image:
  teaser: 1920px-Python_logo_and_wordmark.svg.png

layout: article
title: Learning Object Oriented Programming (1)
date: 2019-01-28
categories: notes
author: chunyi_hsiao
tags: [Object-Oriented, Python]
share: true
---

![Diagram](/../images/2019-01-28-Learning-Object-Oriented-Programming(1)_1.jpg){:width="480"}  

In order to build a complete quantitative trading system, I learned code from my talented [friend](https://github.com/Ceruleanacg).

However, I am not a typical CS student and that absolutely not a good excuse to skip this section, and thereby I found some materials to study, something about OOP in Python.

About the OOP in Python, reference gives me a great idea:


|*Class* is a *blueprint* and *Instance* is a copy of the blueprint with *actual* contents.|

In my understanding and to take an example on the dog. 

- I create a blueprint for adopting the dog -> this is create a class
- I create a blueprint for adopting the dog, who aged 6 months, bred of Cavalier, named Elliot. -> this is create a instance

The first sentence could be written as
```python
class dog:
	pass
```

The second one could be defined as:
```python
class dog:
	def __init__(self, name, breed):
		self.name = name
		self.breed = breed
	pass

elliot = dog(name='Elliot', breed='Cavalier')
cheese = dog(name='Cheese', breed='ShihTzu')
```

So, in my opinion the difference between class and instance is that **class is more likly to create a desire, and instance is acted and adopted the dog.**


### *Learned Today*
- **Instance** is further a action than **Class**.


Reference:

- [Object-Oriented Programming (OOP) in Python 3](https://realpython.com/python3-object-oriented-programming/#classes-in-python)
