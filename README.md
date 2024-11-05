# 🎧Exploratory Data Analysis (EDA) on  Spotify's Most Streamed Songs of 2023🎵🎶

## What is this Project About? 🤔
* This project performs an exploratory data analysis on the Most Streamed Spotify Songs of 2023 Dataset. The goal of this project is to analyze, visualize, and interpret data to gain insights about the most popular music of the year 2023.

## What are the Steps I Did to Accomplish the Project? 👣
* I began by familiarizing myself with the dataset’s structure, checking for missing values and identifying data types. This initial examination in Python helped me understand the features available and prepare for further analysis.

* To uncover trends and patterns, I used a variety of visualization tools such as bar charts, line plots, histograms, heatmaps, and scatter plots, ensuring each was well-labeled for easy interpretation. I also analyzed correlations between variables to provide deeper insights into potential relationships within the data.

* Finally, based on my analysis, I offered insights and recommendations regarding popular tracks, artists, and musical trends, helping to highlight factors that contribute to a track’s popularity.

## How Exactly Did I Code? 😎
* To accomplish this project, I followed a systematic approach, in which I addressed each aspect of the exploratory data analysis (EDA) step by step. Below are the questions I answered, a detailed coding procedure I undertook, and a short analysis of the data's results:
  
### Preliminary Procedures📝
 * The first step to do when coding is to always import Python's Built-in libraries that will be needed.
```python
#Import Python Libraries needed for the data analysis and visualization
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

* Load the Spotify 2023 Dataset file⏳
```python
#Load csv file containing the Spotify 2023 Dataset
#Use ISO-8559-1 encoding to handle some of the special characters that might cause issues in UTF-8.
df = pd.read_csv('spotify-2023.csv', encoding='ISO-8859-1')
df
```

##### Spotify 2023 Dataset
![image](https://github.com/user-attachments/assets/746167f5-f955-4c45-bf8a-759c0260dc7b)

---

 ### Overview of Dataset: 🔍
* How many rows and columns does the dataset contain?
```python
#Determine number of rows and columns of the dataset using 'shape' attribute from panda
shape = df.shape
row, col = shape
print('Rows:', row)
print('Columns:', col)
```
##### Rows and Columns
###### The output will show that the table has 953 rows and 24 columns
![image](https://github.com/user-attachments/assets/1c8c4aea-5c09-4a10-b0a5-2deb8c4a3d9e)

* What are the data types of each column? Are there any missing values?
  ```python
  #Determine the datatypes of each column using 'dtypes' attribute
  datatypes = df.dtypes
  print(datatypes)
  ```
  ```python
  #Find out if there are any missing values in each columns
  #Use .isnull().sum() attribute to determine the number of missing values
  missing = df.isnull().sum()
  print(missing)
  ```
  
##### Datatypes and Missing Values
###### The table shows that the dataset contains 64-bit signed integer and object data types, and that the in_shazam_charts and key columns have 50 and 95 missing values, respectively
![image](https://github.com/user-attachments/assets/c1f5f779-a237-455b-b01d-05dddc8c52a3) ![image](https://github.com/user-attachments/assets/4238d019-38b1-4a27-8407-4172f1496a87)

---

### Basic Descriptive Statistics📌
* What are the mean, median, and standard deviation of the streams column?
```python
#Convert non-numeric values in the 'streams' column  to numeric to avoid errors
df['streams'] = pd.to_numeric(df['streams'], errors='coerce')

#Use the mean attribute to determine the streams' mean value
s_mean = df['streams'].mean()

#Use the mean attribute to compute for its median
s_median = df['streams'].median()

#Determine its standard deviation using std attribute
s_std = df['streams'].std()

#Print output
print('Mean:', s_mean)
print('Median:', s_median)
print('Standard Deviation:', s_std)
```
##### Mean, Median, Standard Deviation 💹
###### The output shows that the number of "streams' have a Mean of 514,137,424.93907565, a Median of 290,530,915.0, and a Standard Deviation of 566,856,949.0388832
![image](https://github.com/user-attachments/assets/109a8ef7-9c50-4046-8375-de36be1a4b96)

* What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?
```python
#Create subplots with 1 row and 2 columns for comparison
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(12, 4))

#Create the histogram for released_year
sns.histplot(data=df, x='released_year', color='yellow', ax=axes[0])  # Use the axes parameter to specify the 1st subplot 
axes[0].set_title('Release Year Distribution', fontsize=14)
axes[0].set_xlabel('Year of Release', fontsize=12)
axes[0].set_ylabel('Frequency', fontsize=12)

#Create the histogram for artist_count
sns.histplot(data=df, x='artist_count', color='green', ax=axes[1])  # Use axes parameter to specify the 2nd subplot
axes[1].set_title('Artist Count Distribution', fontsize=14)
axes[1].set_xlabel('Artist Count', fontsize=12)
axes[1].set_ylabel('Frequency', fontsize=12)

#Adjust the layout of the 2 subplots
plt.tight_layout()

#Show the combined plots
plt.show()
```
##### Released Year & Artist Count Distribution
###### Based on the 1st graph, the latest tracks are amongst the most popular on the Spotify 2023 Dataset,  while the 2nd graph shows that solo artists are prominent.
![image](https://github.com/user-attachments/assets/593f7f1f-abbe-4391-8aa1-74b670d91a3a)

##### Trend and Outliers (Scatterplot correlation)
###### The scatterplot suggest that there is little to no correlation between year of releases and artist counts.
![image](https://github.com/user-attachments/assets/7de83316-6d09-4eec-92c7-bc5732cec70e)

---

### Top Performers🌟

* Which track has the highest number of streams? Display the top 5 most streamed tracks.
```python
#Sort the DataFrame by streams in descending order
top_streams = df.sort_values(by='streams', ascending=False).head()

#Use head attribute to show top 5
top_streams.head()
```
##### Top 5 Most Streamed tracks
###### Blinding Lights by The Weeknd is the most streamed track, followed by Shape of You, then Someone You Loved	 by Lewis Capaldi. With Dance Monkey by Tones and I as fourth and lastly, Sunflower by	Post Malone
![image](https://github.com/user-attachments/assets/d59bee07-e787-4858-a95d-623bcfb61453)

* Who are the top 5 most frequent artists based on the number of tracks in the dataset?
```python
#Count the frequency of each artist and get the top 5
artist_freq = df['artist(s)_name'].value_counts().head()
print(artist_freq)

#Plot the data directly without converting it to a DataFrame
sns.barplot(hue=artist_freq.index, y=artist_freq.values, legend=True, palette='viridis')

#Label the parameters of the bar chart
plt.xlabel('Artist')
plt.ylabel('Frequency')
plt.title('Top 5 Most Frequent Artists')
plt.show()
```

##### Top 5 Most Frequent Artists👨‍🎤👩‍🎤
###### 
![image](https://github.com/user-attachments/assets/57d79e91-19cd-4372-b234-bbfeb98d19b4) ![image](https://github.com/user-attachments/assets/a4ce4718-b61d-44ca-97c5-2a67b6038b6a)

---

### Temporal Trends📉
* Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.
  ```python
  #Count the number of tracks released per year in the dataframe
  yearly_tracks = df['released_year'].value_counts().sort_index()
  print(yearly_tracks)

  #Create a barplot and set the parameters
  plt.figure(figsize=(15, 8))
  sns.lineplot(x=yearly_tracks.index, y=yearly_tracks.values, color='cyan',marker='o', markersize=6, linewidth=1.5)

  #Label each axes
  plt.title('Number of Tracks Released Per Year', fontsize=15)
  plt.xlabel('Release Year', fontsize=14)
  plt.ylabel('Number of Tracks', fontsize=14)
  plt.xticks(ticks=range(yearly_tracks.index.min(), yearly_tracks.index.max() + 1,3),rotation=45, fontsize=7)
  plt.yticks(fontsize=10)
  plt.show()
  ```
  
  ###### Number of Tracks Released per Year🎤
  #######

  ![image](https://github.com/user-attachments/assets/cb8a58ee-a65a-4fdf-9b6b-6b689144f97e)

* Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?
```python
#Count the number of tracks released per year in the dataframe
monthly_tracks = df['released_month'].value_counts().sort_index()
print(monthly_tracks)

#Create a list of the names of the months
month_name = ['January','February','March','April','May','June','July','August','September','October','November','December']

#Create a barplot and set the parameters
plt.figure(figsize=(15, 8)) 
sns.barplot(x=month_name,hue=month_name, y=monthly_tracks.values, palette='dark:brown')

#Label each axes
plt.title('Number of Tracks Released Per Month', fontsize=15) 
plt.xlabel('Release Month', fontsize=14)  
plt.ylabel('Number of Tracks', fontsize=14)  
plt.xticks(fontsize=12)  
plt.yticks(fontsize=12)  
plt.show()
```
##### Number of Tracks Released per Month📀
######
![image](https://github.com/user-attachments/assets/bf5020bc-01d6-4e13-8b14-13e62e245cad)


---

### Genre and Music Characteristics🎸
* Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?
```python
#Find the correlation between streams and music attributes
stream_music_correl = df[['streams','bpm','danceability_%','valence_%','energy_%','acousticness_%',
                          'instrumentalness_%','liveness_%','speechiness_%']].corr()

#Print the correlation table
print("Correlation Table:")
print(stream_music_correl)

#Plot the correlation between streams and music attribute using heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(stream_music_correl, annot=True, cmap='Reds', fmt='.2f', square=True)
plt.title('Correlation between Streams and Musical Attributes')
plt.xticks(rotation=45)
plt.show()
```

##### Correlation between Streams and Musical Attributes 📊
###### 
![image](https://github.com/user-attachments/assets/d5aa186e-bd54-4f87-a428-abeb88099f3b) ![image](https://github.com/user-attachments/assets/c28ecbd1-618f-491f-9bb7-9f25d51c2c78)

* Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?
```python
#Create subplots with 1 row and 2 columns for comparison
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(12, 6))

#Create scatterplot for dance and energy and specify the parameters 
sns.scatterplot(data = df, x='danceability_%',y='energy_%', alpha = 0.5, color='green',ax=axes[0] )
axes[0].set_title('Correlation between Danceability% and Energy%')
axes[0].set_xlabel('Danceability%')
axes[0].set_ylabel('Energy%')

#Create scatterplot for dance and energy and specify the parameters 
sns.scatterplot(data = df, x='valence_%',y='acousticness_%', alpha = 0.5, color='blue',ax=axes[1] )
axes[1].set_title('Correlation between Valence% and Acousticness%')
axes[1].set_xlabel('Valence%')
axes[1].set_ylabel('Acousticness%')

#Adjust and show the layout of the 2 subplots
plt.tight_layout()
plt.show()

#Show values of correlation
dance_energy = df[['danceability_%', 'energy_%']].corr()
print("\nThe correlation between Danceability% and Energy% is")
print(dance_energy,'\n')

valence_acoustic = df[['valence_%', 'acousticness_%']].corr()
print("\nThe correlation between Valence% and Acousticness% is")
print(valence_acoustic,'\n')
```

##### Correlation between Danceability% and Energy%, Valence% and Acousticness%💃
######
![image](https://github.com/user-attachments/assets/758213d8-fe6d-4507-83f0-377bb0c7bffb)
![image](https://github.com/user-attachments/assets/b717c3ff-5943-48d1-8966-5875abf01a98)

---

### Platform Popularity🌐
* How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare?
```python
#Store variabe columns to ensure columns are correct
platform = ['in_spotify_playlists', 'in_spotify_charts', 'in_apple_playlists',
                   'in_apple_charts', 'in_deezer_playlists', 'in_deezer_charts',
                   'in_shazam_charts']

#Convert non-numeric values in columns to numeric(to NaN)
for column in platform:
    df[column] = pd.to_numeric(df[column], errors='coerce') 

#Compute for the total of each platform
total = {'in_spotify_playlists': df['in_spotify_playlists'].sum(),'in_spotify_charts': df['in_spotify_charts'].sum(),
    'in_apple_playlists': df['in_apple_playlists'].sum(),'in_apple_charts': df['in_apple_charts'].sum(),
    'in_deezer_playlists': df['in_deezer_playlists'].sum(),'in_deezer_charts': df['in_deezer_charts'].sum(),
    'in_shazam_charts': df['in_shazam_charts'].sum()}

#Create a summary DataFrame
sum_table = pd.DataFrame({'Platform': total.keys(),'Total Track Count': total.values()})

#Display values of the summary
print(sum_table)

#Create the bar plot to compare the number of tracks
plt.figure(figsize=(12, 6))
sns.barplot(data=sum_table, y='Platform',hue='Platform',x ='Total Track Count', palette='rocket')

#Label each parameter and set y-axis to logarithmic scale to compress the range of values
plt.title('Comparison of Number of Tracks between Different Platforms (Log Scale)', fontsize=16)
plt.ylabel('Platform', fontsize=14)
plt.xlabel('Number of Tracks (Log Scale)', fontsize=14)
plt.xscale('log')

#Display plot
plt.tight_layout()
plt.show()
```

##### Comparison between Number of Tracks in Different Platforms🎶
######
![image](https://github.com/user-attachments/assets/7d1e34b6-1bf4-435c-9dc3-85b0e97af125)
![image](https://github.com/user-attachments/assets/7ba566a1-685d-4d04-99d5-196a023e190e)

 Which platform seems to favor the most popular tracks?
```python
#Sort DataFrame by streams in descending order and get the top 10 tracks
top_tracks = df.sort_values(by='streams', ascending=False).head(10)

#Use loc to select different columns to be displayed
top_tracks_table = top_tracks.loc[:, ['track_name', 'streams', 'in_spotify_playlists', 'in_spotify_charts','in_apple_playlists',
                                      'in_apple_charts', 'in_deezer_playlists','in_deezer_charts', 'in_shazam_charts']]

#Display the top tracks table
top_tracks_table
```
##### Most Popular Tracks and Different Platforms
######
![image](https://github.com/user-attachments/assets/fb4ed387-0d73-4c65-b2ba-902c18f8141c)

---

### Advanced Analysis📊
* Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?
```python
#Convert columns with non-numeric values to numeric
numeric_columns = ['streams']
df[numeric_columns] = df[numeric_columns].apply(pd.to_numeric, errors='coerce')

#Group by key and mode and calculate total streams
keymode_sum = df.groupby(['key', 'mode']).agg(
    total_streams=('streams', 'sum')
).reset_index()

#Sort the summary by total streams in descending order
keymode_sum = keymode_sum.sort_values(by='total_streams', ascending=False)

#Display the sorted sum
print(keymode_sum)

#Visualize Barplot for Total Streams by Key and Mode
plt.figure(figsize=(12, 6))
sns.barplot(data=keymode_sum, x='key', y='total_streams', hue='mode', palette='rocket')

#Label the plot's parameters
plt.title('Total Streams by Key and Mode', fontsize=16)
plt.xlabel('Key', fontsize=14)
plt.ylabel('Total Streams', fontsize=14)
plt.legend(title='Mode')
plt.xticks(rotation=45)
plt.tight_layout()

#Show the plot
plt.show()
```

##### Comparison Among Tracks with the Same Key or Mode (Major vs. Minor)🎹
![image](https://github.com/user-attachments/assets/6112ee45-d486-4323-89fb-a26062e48109)

* Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.
```python
#Create DataFrame to count occurrences of each artist in different playlists and charts
artist_total = df.groupby('artist(s)_name').agg(
    spotify_playlists=('in_spotify_playlists', 'sum'),
    spotify_charts=('in_spotify_charts', 'sum'),
    apple_playlists=('in_apple_playlists', 'sum'),
    apple_charts=('in_apple_charts', 'sum'),
    deezer_playlists=('in_deezer_playlists', 'sum'),
    deezer_charts=('in_deezer_charts', 'sum'),
    shazam_charts=('in_shazam_charts', 'sum')).reset_index()

# Add a total column for the overall appearance in playlists and charts
artist_total['total_appearance'] = artist_total[['spotify_playlists', 'spotify_charts', 'apple_playlists', 'apple_charts', 
                                                       'deezer_playlists', 'deezer_charts', 'shazam_charts']].sum(axis=1)

# Sort by total appearances in descending order
artist_total = artist_total.sort_values(by='total_appearance', ascending=False)

# Display the summary of artists
print(artist_total.head(10))

# Visualization: Bar Plot for Artist Appearances
plt.figure(figsize=(12, 6))
top_artists = artist_total.head(10)  # Select top 10 artists for visualization
sns.barplot(data=top_artists, y='total_appearance', x='artist(s)_name', hue='artist(s)_name', palette='icefire')

# Label the plot
plt.title('Most Frequently Appearing Artists in Playlists and Charts', fontsize=16)
plt.ylabel('Total Appearances', fontsize=14)
plt.xlabel('Artist Name', fontsize=14)
plt.tight_layout()

# Show the plot
plt.show()
```

##### Most Frequently Appearing Artists in Playlists or Charts📅📈
######
![image](https://github.com/user-attachments/assets/0654caec-dc85-4d19-989f-7ca43de30e94)

## Summary of Insights and Recommendations🔍📋

## Coder's Corner 💻👨‍💻
### Medenilla, Jose Anton M.
* A 2nd Year Electronics Engineering at UST as of repository creation

## Reference Material/s:
* ECE 2112 Lecture Materials by Engr. Ma. Madecheen S. Pangaliman,
* Matplotlib: https://matplotlib.org/3.5.3/api/_as_gen/matplotlib.pyplot.html
* Seaborn: https://seaborn.pydata.org/tutorial/categorical.html
* ChatGPT

# That's all. Thanks a bunch! 🙌
