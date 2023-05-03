# Coronavirus twitter analysis

During this project I scanned all geotagged tweets sent in 2020 to monitor for the spread of the coronavirus on social media.

**Learning Objectives:**

1. work with large scale datasets
1. work with multilingual text
1. use the MapReduce divide-and-conquer paradigm to create parallel code

## Background

**About the Data:**

Approximately 500 million tweets are sent everyday.
Of those tweets, about 2% are *geotagged*.
That is, the user's device includes location information about where the tweets were sent from.
The lambda server's `/data/Twitter dataset` folder contains all geotagged tweets that were sent in 2020.
In total, there are about 1.1 billion tweets in this dataset.

**About MapReduce:**

I followed the [MapReduce](https://en.wikipedia.org/wiki/MapReduce) procedure to analyze these tweets.
MapReduce is a famous procedure for large scale parallel processing that is widely used in industry.
It is a 3 step procedure summarized in the following image:

<img src=mapreduce.png width=100% />

## Programming Tasks

**Run the mapper and Reduce**
I used the MapReduce process to filter through these tweets based on a set list of hashtags that were related to Covid. I then combined this data into two files based on language or country of origin using the command below. We then get two files, reduced.lang and reduced.country that we can use for visualizations.

```
$ ./src/reduce.py --input_paths outputs/geoTwitter*.lang --output_path=reduced.lang
```

```
$ ./src/reduce.py --input_paths outputs/geoTwitter*.country --output_path=reduced.country
```

**Visualize**

I modified the `visualize.py` file so that it generates a bar graph of the results and stores the bar graph as a png file.
The horizontal axis of the graph should be the keys of the input file,
and the vertical axis of the graph should be the values of the input file.
The final results should be sorted from low to high including only the top 10 keys.
Below are the commands I ran to create four different types of bar charts.

# Number of Tweets with #coronavirus in 2020 sorted by top 10 countries
<img src=covid_country.png width=100% />
```
$ ./src/visualize.py --input_path=reduced.country --key='#coronavirus'
```

# Number of Tweets with #coronavirus in 2020 sorted by top 10 languages
<img src=covid_lang.png width=100% />
```
$ ./src/visualize.py --input_path=reduced.lang --key='#coronavirus'
```

# Number of Tweets with #코로나바이러스 in 2020 sorted by top 10 countries

<img src=covid_country_korean.png width=100% />

```
$ ./src/visualize.py --input_path=reduced.country --key='#코로나바이러스'
```

# Number of Tweets with #코로나바이러스 in 2020 sorted by top 10 languages

<img src=covid_lang_korean.png width=100% />

**Task 4: Alternative Reduce**

Next, I wrote a shell script that would take a specified number of hashtags as an input (below I use two and three) and output a line graph that demonstrates the usage over 2020. 

# Number of Tweets that mention '#Cough" or '#Sneeze' over 2020
<img src=cough_sneeze.png width=100% />

```
$ ./src/alternative_reduce.py --keys '#cough' '#sneeze'
```
# Number of Tweets that mention '#Cough" or '#Sneeze' over 2020
<img src=cough_sneeze_sick.png width=100% />

```
$ ./src/alternative_reduce.py --keys '#cough' '#sneeze' '#sick'
```

