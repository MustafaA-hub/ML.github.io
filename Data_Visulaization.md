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
