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

