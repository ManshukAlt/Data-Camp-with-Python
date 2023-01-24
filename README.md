# Data-Camp-with-Python
# Investigating Netflix Movies and Guest Stars in The Office

## 1. Loading your friends data into a dictionary

#### Create the years and durations lists
years = [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020]
durations = [103, 101, 99, 100, 100, 95, 95, 96, 93, 90]

#### Create a dictionary with the two lists
movie_dict = {
    "years" : years,
    "durations": durations
}
 
#### Print the dictionary
print(movie_dict)

#### Output
{'years': [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020],

 'durations': [103, 101, 99, 100, 100, 95, 95, 96, 93, 90]}
## 2. Creating a DataFrame from a dictionary

#### Import pandas under its usual alias
import pandas as pd

#### Create a DataFrame from the dictionary
durations_df = pd.DataFrame(movie_dict)

#### Print the DataFrame
print(durations_df.head)
#### Output
![image](https://user-images.githubusercontent.com/108233181/214242607-20e4bb1a-25eb-42d5-811e-9aaecc37114e.png)
## 3. A visual inspection of our data

#### Import matplotlib.pyplot under its usual alias and create a figure
import matplotlib.pyplot as plt
fig = plt.figure()

#### Draw a line plot of release_years and durations
plt.plot(durations_df["years"],durations_df["durations"])
plt.xlabel("Release Years")
plt.ylabel("Durations")

#### Create a title
plt.title("Netflix Movie Durations 2011-2020")

#### Show the plot
plt.show()

#### Output
![image](https://user-images.githubusercontent.com/108233181/214242722-e3761a51-be0c-4b49-939e-6cf3d596ac69.png)
## 4. Loading the rest of the data from a CSV

#### Read in the CSV as a DataFrame
netflix_df = pd.read_csv("datasets/netflix_data.csv")

#### Print the first five rows of the DataFrame
print(netflix_df.head(5))

#### Output 
![image](https://user-images.githubusercontent.com/108233181/214244060-ee1ed3cd-d64e-4b2d-8ff3-99870b71cb83.png)

## 5. Filtering for movies
#### Subset the DataFrame for type "Movie"
netflix_df_movies_only = netflix_df[netflix_df["type"]=="Movie"]

#### Select only the columns of interest
netflix_movies_col_subset = netflix_df_movies_only[["title", "country", "genre", "release_year","duration"]]

#### Print the first five rows of the new DataFrame
print(netflix_movies_col_subset.head(5))

#### Output
![image](https://user-images.githubusercontent.com/108233181/214244349-aa06b246-860e-46c2-87bc-dd36894b8c4e.png)

## 6. Creating a scatter plot

#### Create a figure and increase the figure size
fig = plt.figure(figsize=(12,8))

#### Create a scatter plot of duration versus year
plt.scatter(netflix_movies_col_subset["release_year"],netflix_movies_col_subset["duration"])
plt.xlabel("Release Year")
plt.ylabel("Duration")
#### Create a title
plt.title("Movie Duration by Year of Release")

#### Show the plot
plt.show()

![image](https://user-images.githubusercontent.com/108233181/214244959-57393c1c-33db-4b97-95eb-9821eac0d6f8.png)

## 7. Digging deeper

#### Filter for durations shorter than 60 minutes
short_movies = netflix_movies_col_subset[netflix_movies_col_subset["duration"] < 60]

#### Print the first 20 rows of short_movies
print(short_movies.head(20))

#### Output
![image](https://user-images.githubusercontent.com/108233181/214249394-936bce41-c62f-4b26-853c-7050c9b86a25.png)
![image](https://user-images.githubusercontent.com/108233181/214249445-fd0f2270-2ec0-408c-b1f5-d1c36da35162.png)
## 8. Marking non-feature films
#### Define an empty list
colors = []

#### Iterate over rows of netflix_movies_col_subset
for lab, row in netflix_movies_col_subset.iterrows() :
    if row['genre']=="Children" :
        colors.append("red")
    elif row['genre']=="Documentaries" :
        colors.append("blue")
    elif row['genre']=="Stand-Up":
        colors.append("green")
    else:
        colors.append("black")
        
#### Inspect the first 10 values in your list        
print(colors[:11])

#### Output
['black', 'black', 'black', 'black', 'black', 'black', 'black', 'black', 'black', 'blue', 'black']

## 9. Plotting with Color!
#### Set the figure style and initalize a new figure
plt.style.use('fivethirtyeight')
fig = plt.figure(figsize=(12,8))
#### Create a scatter plot of duration versus release_year
plt.scatter(netflix_movies_col_subset["release_year"],netflix_movies_col_subset["duration"], c=colors)
#### Create a title and axis labels
plt.title("Movie duration by year of release")
plt.xlabel("Release Year")
plt.ylabel("Duration (min)")
#### Show the plot
plt.show()

#### Output
![image](https://user-images.githubusercontent.com/108233181/214251596-8d5352a7-8ef0-4fe0-a266-372c848aae31.png)
