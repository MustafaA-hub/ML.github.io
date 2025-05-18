# Set Up
````Python

plt.figure(figsize=(14,6)) # Set the width and height of the figure
plt.title("Daily Global Streams of Popular Songs in 2017-2018") # Add title
plt.xlabel("Date") # Add label for horizontal axis
````

Line charts
````Python
# Line chart showing daily global streams of 'Shape of You'
sns.lineplot(data=spotify_data['Shape of You'], label="Shape of You")
````

Bar charts
````Python
# Bar chart showing average arrival delay for Spirit Airlines flights by month
sns.barplot(x=flight_data.index, y=flight_data['NK'])
````

Heat Map
````Python
# Heatmap showing average arrival delay for each airline by month
sns.heatmap(data=flight_data, annot=True)
````
![image](https://github.com/user-attachments/assets/4ba452d0-a56f-47cc-9928-616e6e672e49)

Scatterplot
````Python
sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'])
````
![image](https://github.com/user-attachments/assets/2e572c94-93e4-40a2-a27f-72b91442e213)

Scatterplot + regression line
````Python
sns.regplot(x=insurance_data['bmi'], y=insurance_data['charges'])
````
![image](https://github.com/user-attachments/assets/a36bb55b-74eb-4024-82d0-0915282794bd)

Scatterplot that compares three variables
````Python
sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'], hue=insurance_data['smoker'])
````
![image](https://github.com/user-attachments/assets/a655c6b6-9da0-4098-a10b-8db7ac2f309e)

Scatterplot that compares three variables + regression line
````Python
sns.lmplot(x="bmi", y="charges", hue="smoker", data=insurance_data)
````
![image](https://github.com/user-attachments/assets/48d38991-94e4-4944-a25e-0692c69cb295)

Scatterplot when a categorical variable needs to be on the main axis
````Python
sns.swarmplot(x=insurance_data['smoker'], y=insurance_data['charges'])
````
![image](https://github.com/user-attachments/assets/d311d077-4ef0-4965-bdba-b84ff0798eca)

Histograms
````Python
sns.histplot(iris_data['Petal Length (cm)'])
````
![image](https://github.com/user-attachments/assets/6a68cad6-a1fa-469e-b3bb-15a775b21447)

Histogram color coded to split the data
hue = sets the column we'll use to split the data into different histograms
````Python
# Histograms for each species
sns.histplot(data=iris_data, x='Petal Length (cm)', hue='Species')
````
![image](https://github.com/user-attachments/assets/d2114e05-43c4-47f5-ba91-9ea84734413a)


Density plots = Kernal Density Estimates(kde)
```Pyhon
# KDE plot 
sns.kdeplot(data=iris_data['Petal Length (cm)'], shade=True)
````
![image](https://github.com/user-attachments/assets/e89fec86-7b36-463c-9c3f-a6ba782cc489)

2D KDE Plot
````Python
# 2D KDE plot
sns.jointplot(x=iris_data['Petal Length (cm)'], y=iris_data['Sepal Width (cm)'], kind="kde")
````
![image](https://github.com/user-attachments/assets/18565fc2-543d-4fac-ad6b-3fcf8deeffa8)

KDE Plot color coded to split the data
hue = sets the column we'll use to split the data into different histograms
````Python
# KDE plots for each species
sns.kdeplot(data=iris_data, x='Petal Length (cm)', hue='Species', shade=True)
````
![image](https://github.com/user-attachments/assets/d199519e-e733-4db0-ad66-0eda228c4cf3)

