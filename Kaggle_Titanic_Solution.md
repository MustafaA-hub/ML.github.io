The train data set contains 891 indiviual each with a unique name. However, most names contain a common title that can be used for categorizing data and training the model. The below code extracts the name title from each name.

````Python
Name_Title = []
for name in train_data['Name']:    
    start_index = name.find(', ')
    stop_index = name.find('.')
    Name_Title.append(name[start_index+2:stop_index])
````
