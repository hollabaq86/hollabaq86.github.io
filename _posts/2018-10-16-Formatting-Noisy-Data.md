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

csvkit is a set of command line tools (written in python!) that help you work with CSVs. Since I use this set of tools at work regularly, I felt comfortable using `csvcut` to extract specific columns from my source data. Once I had all the tables of possible dishes from my internet resource source saved to CSV files, I used the command:

```
$ csvcut -n FILE
```

To quickly examine columns and see how much work would be needed to condense all files into one large resource.

_Example output_

![a list of columns generated from a csvcut command](../img/source3.png)

Then, once I had established a list of columns I would need to add or remove from each source table, I could use `csvcut` again to select either a specific column(s) or extract all but a few column(s) as my output:

```
$ csvcut -c 5 dishes_defense.csv > just_notes.csv 
// this gives me just the notes column from the CSV

$ csvcut -C 5 dishes_defense.csv > trimmed_defense.csv
// this gives me all columns except the notes columne
```

Once I had all the columns/fields in my source CSV files in the same order, I could use the tail command to dump all contents of my CSVs starting at a specific row (like row 2, so that I'm not copying headers) into a condensed file:

```
$ tail -n +2 dishes_defense.csv > all_dishes.csv
```

Now I have one large file of data! That said, there's still some work that I need to do so that my data is in a format a ML algorithm can read and use.


## Scripting for specific use cases


So, I now have one CSV file containing all source data, but there's some features that I'd like to add using some of this information:

1. Looking over the names of recipes, the first word in a recipe's name _could_ indicate its value or not:

```
Recipe Name
Chilly Simmered Fruit
Mighty Crab Risotto
Mighty Porgy Meunière
```

1. The source data also indicates whether an ingredient can be used in a recipe more than once (For reference, you can submit up to five ingredients to create a recipe in _Zelda: Breath of the Wild_), but it's written in a format that's great for humans, but not so great for a machine:

```
Recipe Name, Ingredients
Mighty Herb Sautè,"Mighty Porgy x2,Mighty Thistle,Bird Egg,Goron Spice"
Mighty Porgy Meunière,"Tabantha Wheat,Goat Butter,Mighty Porgy x3"
//ingredients are a string and some ingredients have x3 indicating multiples
``` 

I _could_ use the pandas library to hot encode _some_ of this information (more on this further down in my post), but it might be more practical to just write a script that does this for me.

### Using `csv`
Python's [CSV library](https://docs.python.org/3/library/csv.html) has some great features that make it easy to work with complex data structures. For example, using `DictReader` and `DictWriter` you can treat CSV rows as if they are dictionaries, making it more legible to extract data from specific columns (provided your source data and an output file have headers):

```
with open('raw_data.csv',) as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
    	# do all the things!
```

This proved especially useful writing my formatted data to an output csv. Assuming I had a dictionary of `recipes` from my input file I could iteratively work through each `recipe` and its values, creating a `formatted_row` dictionary that could be written to my output CSV using DictWriter.

```
for recipe in recipes:
	# work through the values for all columns, performing additional formatting as needed
	formatted_row['Sell Price'] = recipe['Sell Price'] 

	# write this information to a dictionary I can then reference efficiently when creating my output CSV
	write_to_output[recipe['Recipe Name']] = formatted_row 

with open('output.csv', 'w') as csvfile:
    WRITER = csv.DictWriter(csvfile, fieldnames=HEADERS)
    WRITER.writeheader()
    for formatted_recipe in write_to_output: 
        WRITER.writerow(formatted_recipe) 

```

### Extracting Recipe Names


using python csv:
	manually creating ingredient counts based on existing columns from the source
	manually hot encoding recipe and health effects 

## Hot Encoding

Using pandas to hot encode a list of items to separate columns/fields
	- why didn't I use this technique for some items I manually hot encoded in my script file?

## Scaling

using pandas to scale duration, sell price, and health effect details
dropping and concating your work