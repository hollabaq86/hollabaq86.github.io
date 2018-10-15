---
author: xoxo Holla
---

_Formatting Noisy Data_

# Overview

A key factor in the success of any machine learning(ML) project includes formatting your data so that the algorithm you choose has "good" data to work with. What do I mean?

- The data is accurate,
- Features that are quantitative are scaled if needed,
- Features that are qualitative are classified if needed.

For my current project, I'm trying to identify the selling price of recipes you can create in the Nintendo game _Zelda: Breath of the Wild_. Unfortunately there isn't a publicly available database of all ingredients and possible recipes, so I did some googling to see what online resources had data that could be scraped the most easily.

My source information does have several tables of recipes to use! That said, not all tables have the same fields or columns, and some values for these columns contain information that not easy for a program to read without some help:

_Example 1- this table looks like it'd be easy to convert_

![Source table showing ok data](../img/source1.png)

_Example 2- this table has information that is contextual and may need some work_

![Source table showing nuanced notes](../img/source2.png)

To achieve this, we can use some old school command line tricks, a little script work, as well as hot encoding and scaling techniques so that my training and test data is in a format that's easier for my ML project to read.

## Command line tips

Tools I used- [csvkit](https://csvkit.readthedocs.io/en/1.0.3/#), [tail](http://man7.org/linux/man-pages/man1/tail.1.html)

### csvkit

csvkit is a set of command line tools (written in python!) that help you work with CSVs. Since I use this set of tools at work regularly, I felt comfortable using `csvcut` to extract specific columns from my source data

## Scripting for specific use cases

using python csv:
	DictReader and DictWriter
	manually creating ingredient counts based on existing columns from the source
	manually hot encoding recipe and health effects 

## Hot Encoding

Using pandas to hot encode a list of items to separate columns/fields
	- why didn't I use this technique for some items I manually hot encoded in my script file?

## Scaling

using pandas to scale duration, sell price, and health effect details
dropping and concating your work