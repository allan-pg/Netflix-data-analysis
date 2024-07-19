# Data Analysis With Python - Netflix
![q](https://github.com/allan-pg/Netflix-data-analysis/assets/62595869/d1717927-9853-4055-9eb8-7713e7c288a8)


**Data obtained from kaggle.com**
The dataset is also included in the repository. 

<p>Topics covered:

* Programming in Python 
* Numpy
* Pandas
* Matplotlib
* seaborn

## Introduction
I imported all the necessary libraries in pyton i will need for this project: 

![q](https://github.com/allan-pg/Netflix-data-analysis/assets/62595869/da69aedd-d9b4-435d-be56-4e9a569563d5)

load your csv file from kaggle to your jupyter notebook 
syntax
> df = pd.read_csv('data.csv')

>  ![q](https://github.com/allan-pg/Netflix-data-analysis/assets/62595869/655255c3-a2ef-422c-9476-16239caaf19d)

To see your csv dataframe the first 5 rows and the last 5 rows on your notebook  

> ![q](https://github.com/allan-pg/Netflix-data-analysis/assets/62595869/10d16344-f5af-427d-aaba-86ea816d6130)

- The df. shape method provides information about the number of rows and columns in a DataFrame quickly and easily.
 ```
data.shape
```
- data.size shows total no. of values in the dataset
```
data.size
```
- data.columns  show the columns in the dataframe in form of a list
```
data.columns
```
- data.dtypes show the data types in each colmns
```
data.dtypes
```
> are there any duplicates in the record if yes remove the duplicate  
> find the duplicated columns using
```
data[data.duplicated()]
```
- delete the duplicated columns
```
data.drop_duplicates(inplace=True)
```
- to show th sum of all null values in a column
```
data.isnull().sum()
```
> Visualize the null values in a heat map
- Is there any null values in the data set? show with a heatmap
```
sns.heatmap(data.isnull())
plt.show()
 #from the heatmap analysis there are no null values
```
### Analyse your data now  
Questions  
- 1.0 for 'House of Cards' what is the show id and who is the director?
```
filt = (data.title == 'House of Cards')
data[filt]['show id']['director']
```
- 2.0 to show a particular record usind isin()
```
data[data['title'].isin(['House of Cards'])]
```
- 3.0 show the same record using str.contains()
```
data[data['title'].str.contains('House of Cards')]
```
- 4.0 In whic year was the highest number of the tv shows and movies released? show with a line graph
```
#incase the release year was an object
pd.to_datetime(data['release_year'])
no_of_show_by_year = data.release_year.value_counts()
data[no_of_show_by_year].plot(kind = line)
```
- 5.0 Show the number of shows using a bar chart
```
sns.countplot(data['type'])
```
- 6.0 show all movies released in 2000
```
filt = (data['type'] == 'Movie') & (data['release_year'] == 2000)
data[filt]
```
- 7.0 show title of only TV shows released in the united states only
```
filt = (data['type'] == 'TV Show') & (data['country'] == 'United States')
data[filt]['title']
```
- 8.0 use a word cloud to show case the countries where movies are produced
```
from wordcloud import WordCloud
plt.subplots(figsize=(25,15))
wordcloud = WordCloud(
                          background_color='Black',
                          width=1920,
                          height=1080
                         ).generate(" ".join(data.country))
plt.imshow(wordcloud)
plt.axis('off')
plt.savefig('country.png')
plt.show()
```
![Capture](https://github.com/user-attachments/assets/498de54c-8f73-4799-ae10-76cdfad6fb6f)  

- 9.0 use a pie chart to visualize the no. of shows per rating
```
data['rating'].value_counts().plot.pie(autopct='%1.1f%%',shadow=True,figsize=(10,8))
plt.show()
```
![Capture](https://github.com/user-attachments/assets/90fb6b08-267e-49ac-9d5c-40182739e13d)  

- 10.0 relationship between type and rating
```
plt.figure(figsize=(10,8))
sns.countplot(x='rating',hue='type',data=data)
plt.title('Relation between Type and Rating')
plt.show()
```
![Capture](https://github.com/user-attachments/assets/9c1d319a-c911-4387-8d09-f47c0a825b2d)

