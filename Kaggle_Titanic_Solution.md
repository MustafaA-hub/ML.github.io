The train data set contains 891 indiviual each with a unique name. However, most names contain a common title that can be used for categorizing data and training the model. The below code extracts the name title from each name.

````Python
Name_Title = []
for name in train_data['Name']:    
    start_index = name.find(', ')
    stop_index = name.find('.')
    Name_Title.append(name[start_index+2:stop_index])
X['Name_Title'] = Name_Title
````

The above titile extraction resulted in 17 unique titles. ![image](https://github.com/user-attachments/assets/068d6fc1-90d3-4040-b22b-c0a4decbce4f)
I decided to group similar titles together into Mr, Mrs, Miss, Master, Officials (Major, Captain, Col, Dr etc), and Royalty
````Python
title_mapping = {
    'Mr': 'Mr',
    'Miss': 'Miss',
    'Mrs': 'Mrs',
    'Master': 'Master',
    'Dr': 'Official',
    'Rev': 'Official',
    'Col': 'Official',
    'Major': 'Official',
    'Mlle': 'Miss',
    'Ms': 'Miss',
    'Mme': 'Mrs',
    'Capt': 'Official',
    'Sir': 'Royalty',
    'Lady': 'Royalty',
    'Don': 'Mr',
    'Dona': 'Miss',
    'Countess': 'Royalty',
    'Jonkheer': 'Royalty'
}
X['Name_Title'] = X['Name_Title'].map(title_mapping)
````
![image](https://github.com/user-attachments/assets/f14f27df-df56-4eaf-97d6-a540c543317b)

