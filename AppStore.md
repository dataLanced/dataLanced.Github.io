 # What Makes a "Killer App"?
![Image](https://i.imgur.com/wxc4mct.png)

The aim of this project is to build a free app for our customers that will allow us to attract the most possible users, hence maximizing our revenue. To do this, we will take a look at existing apps on both the Apple App Store and the Google Play Store, analyze, interpret and synthesize the data and use the results to influence how we go about building our app.

Before we get further though, let's present a bit of background on the data. As of September 2018 (the time when this data was taken), there were 2 million iOS apps on the Apple App Store and 2.1 million Android Apps on the Google Play Store.

Because analyzing data for 4 million apps would cause a significant amount of money, we'd be better served if we can find a much smaller but still relevant portion of it at no further costs to us. 

Doing some research, I was able to find some relevant datasets at the popular dataset repository site known as [Kaggle](https://www.kaggle.com/).

* The [Google Dataset](https://www.kaggle.com/lava18/google-play-store-apps) and the [direct spreadsheet download](https://dq-content.s3.amazonaws.com/350/googleplaystore.csv)
* The [Apple Dataset](https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps) and the [direct spreadsheet download](https://dq-content.s3.amazonaws.com/350/AppleStore.csv)


## Exploring the Data
In the next cell, we are going to write code that opens up both of our datasets so we can start exploring.


```python
"""Open the file, import 'reader' function from the csv module, read it in and
transform it into a list"""

opened_file1 = open('AppleStore.csv') # Apple Store App data
opened_file2 = open('googleplaystore.csv') # Google Play Store App data
from csv import reader
read_file1 = reader(opened_file1)
read_file2 = reader(opened_file2)

# Convert to a lists of lists
apple_alldata = list(read_file1) # Apple App Store lists of lists w/header row
google_alldata = list(read_file2) # Google Play store lists of lists w/header row

# Our App Store dataset divide

apple_dataset = apple_alldata[1:] # all of the apps
apple_header = apple_alldata[0] # header row

# Our Google dataset divided 

google_dataset = google_alldata[1:]
google_header = google_alldata[0]

# making a function that prints the Google Play store column names
def printgoogle_header():
    print(google_header)
    print('\n')

# making a function that prints the Apple App Store column names
def printapple_header():
    print(apple_header)
    print('\n')

# Create a function that allows us to see the index number and length of any set of rows that we specify
def explore_data(dataset, start, end, rows_and_columns=False, index_and_length=True):
    dataset_slice = dataset[start:end]
    index_num = start # Here we set 'index_num' to the same value as the 'start' parameter/variable
    
    ### This if block of code automatically prints out the corresponding header row of the dataset that we use
    if dataset == google_dataset:
        printgoogle_header()
        
    elif dataset == apple_dataset:
        printapple_header()
    
    else:
        pass
    
    for row in dataset_slice:
        
            print(row)
            if index_and_length:
                print('Index number: ' + str(index_num))  
                print('The length of this row is ' + str(len(row)))
                print('\n') # adds a new (empty) line after each row
                index_num += 1
            else:
                print('\n')
        
    if rows_and_columns:
        print('Number of rows:', len(dataset))
        print('Number of columns:', len(dataset[0]))
```

For the App Store and the Google Play store, we need to identify the important columns that will facilitate our analysis. First, we'll print out the header for our Google dataset along with its first 3 rows of app data.


```python
explore_data(google_dataset, 0, 4, True, True)
```

    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver']
    
    
    ['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']
    Index number: 0
    The length of this row is 13
    
    
    ['Coloring book moana', 'ART_AND_DESIGN', '3.9', '967', '14M', '500,000+', 'Free', '0', 'Everyone', 'Art & Design;Pretend Play', 'January 15, 2018', '2.0.0', '4.0.3 and up']
    Index number: 1
    The length of this row is 13
    
    
    ['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']
    Index number: 2
    The length of this row is 13
    
    
    ['Sketch - Draw & Paint', 'ART_AND_DESIGN', '4.5', '215644', '25M', '50,000,000+', 'Free', '0', 'Teen', 'Art & Design', 'June 8, 2018', 'Varies with device', '4.2 and up']
    Index number: 3
    The length of this row is 13
    
    
    Number of rows: 10841
    Number of columns: 13


As we've seen from our output, the most important column names for the Google Play store appear to be: 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres'. Next we'll look at the App Store.


```python
explore_data(apple_dataset, 0, 3, True)
```

    ['id', 'track_name', 'size_bytes', 'currency', 'price', 'rating_count_tot', 'rating_count_ver', 'user_rating', 'user_rating_ver', 'ver', 'cont_rating', 'prime_genre', 'sup_devices.num', 'ipadSc_urls.num', 'lang.num', 'vpp_lic']
    
    
    ['284882215', 'Facebook', '389879808', 'USD', '0.0', '2974676', '212', '3.5', '3.5', '95.0', '4+', 'Social Networking', '37', '1', '29', '1']
    Index number: 0
    The length of this row is 16
    
    
    ['389801252', 'Instagram', '113954816', 'USD', '0.0', '2161558', '1289', '4.5', '4.0', '10.23', '12+', 'Photo & Video', '37', '0', '29', '1']
    Index number: 1
    The length of this row is 16
    
    
    ['529479190', 'Clash of Clans', '116476928', 'USD', '0.0', '2130805', '579', '4.5', '4.5', '9.24.12', '9+', 'Games', '38', '5', '18', '1']
    Index number: 2
    The length of this row is 16
    
    
    Number of rows: 7197
    Number of columns: 16


Above we do the same thing with the App Store apps as we did with the Google Play apps and we notice that column names for the header are quite different. However, we still manage to identify the most useful columns for our analysis.

From the App Store some of these important columns include: 'prime_genre', 'rating_count_tot', 'user_rating', 'cont_rating'.

Just in case you'd like to take another look the dataset:

* [Google Play Store](https://www.kaggle.com/lava18/google-play-store-apps)
* [App Store](https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps)

## Search and Deleting Bad Data

When we're working from a dataset curated from a public space like Kaggle, it is important to check the discussion forums to make sure that the integrity of the data is intact. The advantage of having datasets on a site like Kaggle is in most cases, that we are not the first users to have interacted with a dataset. Regarding the Google Play dataset, I came across one such instance where users stated that a specific row had a missing value in its 'Category' column. 

According to the users, the index number of the row is 10472. So we'll use our `explore_data()` function to see if it finds anything off.


```python
# Searching for a suspicious piece of data
explore_data(google_dataset, 10470, 10481, True )
```

    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver']
    
    
    ['Jazz Wi-Fi', 'COMMUNICATION', '3.4', '49', '4.0M', '10,000+', 'Free', '0', 'Everyone', 'Communication', 'February 10, 2017', '0.1', '2.3 and up']
    Index number: 10470
    The length of this row is 13
    
    
    ['Xposed Wi-Fi-Pwd', 'PERSONALIZATION', '3.5', '1042', '404k', '100,000+', 'Free', '0', 'Everyone', 'Personalization', 'August 5, 2014', '3.0.0', '4.0.3 and up']
    Index number: 10471
    The length of this row is 13
    
    
    ['Life Made WI-Fi Touchscreen Photo Frame', '1.9', '19', '3.0M', '1,000+', 'Free', '0', 'Everyone', '', 'February 11, 2018', '1.0.19', '4.0 and up']
    Index number: 10472
    The length of this row is 12
    
    
    ['osmino Wi-Fi: free WiFi', 'TOOLS', '4.2', '134203', '4.1M', '10,000,000+', 'Free', '0', 'Everyone', 'Tools', 'August 7, 2018', '6.06.14', '4.4 and up']
    Index number: 10473
    The length of this row is 13
    
    
    ['Sat-Fi Voice', 'COMMUNICATION', '3.4', '37', '14M', '1,000+', 'Free', '0', 'Everyone', 'Communication', 'November 21, 2014', '2.2.1.5', '2.2 and up']
    Index number: 10474
    The length of this row is 13
    
    
    ['Wi-Fi Visualizer', 'TOOLS', '3.9', '132', '2.6M', '50,000+', 'Free', '0', 'Everyone', 'Tools', 'May 17, 2017', '0.0.9', '2.3 and up']
    Index number: 10475
    The length of this row is 13
    
    
    ['Lennox iComfort Wi-Fi', 'LIFESTYLE', '3.0', '552', '7.6M', '50,000+', 'Free', '0', 'Everyone', 'Lifestyle', 'March 22, 2017', '2.0.15', '2.3.3 and up']
    Index number: 10476
    The length of this row is 13
    
    
    ['Sci-Fi Sounds and Ringtones', 'PERSONALIZATION', '3.6', '128', '11M', '10,000+', 'Free', '0', 'Everyone', 'Personalization', 'September 27, 2017', '4.0', '4.0 and up']
    Index number: 10477
    The length of this row is 13
    
    
    ['Sci Fi Sounds', 'FAMILY', '3.2', '4', '8.0M', '1,000+', 'Free', '0', 'Everyone', 'Entertainment', 'November 2, 2017', '1.0', '4.0 and up']
    Index number: 10478
    The length of this row is 13
    
    
    ['Free Wi-fi HotspoT', 'COMMUNICATION', '4.1', '382', '2.3M', '50,000+', 'Free', '0', 'Everyone', 'Communication', 'July 20, 2018', '2.5', '4.0 and up']
    Index number: 10479
    The length of this row is 13
    
    
    ['FJ 4x4 Cruiser Offroad Driving', 'FAMILY', '4.1', '3543', '49M', '500,000+', 'Free', '0', 'Everyone', 'Simulation', 'January 4, 2017', '1.1', '2.3 and up']
    Index number: 10480
    The length of this row is 13
    
    
    Number of rows: 10841
    Number of columns: 13


After doing our testing, row index 10472 returned a length of 12 as opposed to the expected 13. This meant that a value was missing and looking through the row, I noticed that the `Genres` value just had `''` for a value.

Now that we know which row is the culprit. We are going to run the `del` command to get rid of it in the next cell!



```python
### DON'T RUN THIS CELL AGAIN!!!! ###
del google_dataset[10472]
explore_data(google_dataset, 10470, 10481, True )
```

    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver']
    
    
    ['Jazz Wi-Fi', 'COMMUNICATION', '3.4', '49', '4.0M', '10,000+', 'Free', '0', 'Everyone', 'Communication', 'February 10, 2017', '0.1', '2.3 and up']
    Index number: 10470
    The length of this row is 13
    
    
    ['Xposed Wi-Fi-Pwd', 'PERSONALIZATION', '3.5', '1042', '404k', '100,000+', 'Free', '0', 'Everyone', 'Personalization', 'August 5, 2014', '3.0.0', '4.0.3 and up']
    Index number: 10471
    The length of this row is 13
    
    
    ['osmino Wi-Fi: free WiFi', 'TOOLS', '4.2', '134203', '4.1M', '10,000,000+', 'Free', '0', 'Everyone', 'Tools', 'August 7, 2018', '6.06.14', '4.4 and up']
    Index number: 10472
    The length of this row is 13
    
    
    ['Sat-Fi Voice', 'COMMUNICATION', '3.4', '37', '14M', '1,000+', 'Free', '0', 'Everyone', 'Communication', 'November 21, 2014', '2.2.1.5', '2.2 and up']
    Index number: 10473
    The length of this row is 13
    
    
    ['Wi-Fi Visualizer', 'TOOLS', '3.9', '132', '2.6M', '50,000+', 'Free', '0', 'Everyone', 'Tools', 'May 17, 2017', '0.0.9', '2.3 and up']
    Index number: 10474
    The length of this row is 13
    
    
    ['Lennox iComfort Wi-Fi', 'LIFESTYLE', '3.0', '552', '7.6M', '50,000+', 'Free', '0', 'Everyone', 'Lifestyle', 'March 22, 2017', '2.0.15', '2.3.3 and up']
    Index number: 10475
    The length of this row is 13
    
    
    ['Sci-Fi Sounds and Ringtones', 'PERSONALIZATION', '3.6', '128', '11M', '10,000+', 'Free', '0', 'Everyone', 'Personalization', 'September 27, 2017', '4.0', '4.0 and up']
    Index number: 10476
    The length of this row is 13
    
    
    ['Sci Fi Sounds', 'FAMILY', '3.2', '4', '8.0M', '1,000+', 'Free', '0', 'Everyone', 'Entertainment', 'November 2, 2017', '1.0', '4.0 and up']
    Index number: 10477
    The length of this row is 13
    
    
    ['Free Wi-fi HotspoT', 'COMMUNICATION', '4.1', '382', '2.3M', '50,000+', 'Free', '0', 'Everyone', 'Communication', 'July 20, 2018', '2.5', '4.0 and up']
    Index number: 10478
    The length of this row is 13
    
    
    ['FJ 4x4 Cruiser Offroad Driving', 'FAMILY', '4.1', '3543', '49M', '500,000+', 'Free', '0', 'Everyone', 'Simulation', 'January 4, 2017', '1.1', '2.3 and up']
    Index number: 10479
    The length of this row is 13
    
    
    ['FJ 4x4 Cruiser Snow Driving', 'FAMILY', '4.2', '1619', '43M', '500,000+', 'Free', '0', 'Everyone', 'Simulation', 'June 4, 2018', '1.3', '4.0 and up']
    Index number: 10480
    The length of this row is 13
    
    
    Number of rows: 10840
    Number of columns: 13



```python
for app in google_dataset:
    app_name = app[0]
    if app_name == 'Coloring book moana':
        print(app)
```

    ['Coloring book moana', 'ART_AND_DESIGN', '3.9', '967', '14M', '500,000+', 'Free', '0', 'Everyone', 'Art & Design;Pretend Play', 'January 15, 2018', '2.0.0', '4.0.3 and up']
    ['Coloring book moana', 'FAMILY', '3.9', '974', '14M', '500,000+', 'Free', '0', 'Everyone', 'Art & Design;Pretend Play', 'January 15, 2018', '2.0.0', '4.0.3 and up']


In this example, we use the 'Instagram' app to illustrate issues with duplicates that can arise and from what we see, it has multiple duplicate entries in this set. In the following lines, we're going to see just how many duplicates that we're working with exactly by looping over the Google dataset, using the 'in' operator to weed the duplicates out.


```python
duplicate_apps = []
unique_apps = []

for app in google_dataset:
    app_name = app[0]
    if app_name in unique_apps:
        duplicate_apps.append(app_name)
    else:
        unique_apps.append(app_name)

print('Number of duplicate apps: ', len(duplicate_apps))
print('\n')
print('Examples of duplicate apps:', duplicate_apps[:15])
      
```

    Number of duplicate apps:  1181
    
    
    Examples of duplicate apps: ['Quick PDF Scanner + OCR FREE', 'Box', 'Google My Business', 'ZOOM Cloud Meetings', 'join.me - Simple Meetings', 'Box', 'Zenefits', 'Google Ads', 'Google My Business', 'Slack', 'FreshBooks Classic', 'Insightly CRM', 'QuickBooks Accounting: Invoicing & Expenses', 'HipChat - Chat Built for Teams', 'Xero Accounting Software']


After our work above, we were able to determine that this Google dataset has 1181 instances where a duplicate occurs. Continuing on, our objective is to properly remove these duplicates before we can work with this data. Once again, using our 'Instagram' example a few cells above, we're not going to randomly delete all the duplicates until only one is left, instead we will keep the instance that is the most recent piece of data. This should be evidenced by the number of reviews that the app has; the one with the highest amount of reviews should be the most recent version. Alternatively, we can also check the 'Last Updated', 'Current Ver' and 'Android Ver' columns


```python
print('Expected length: ', len(google_dataset) - len(duplicate_apps))
```

    Expected length:  9659



```python
reviews_max = {}

for app in google_dataset:
    name = app[0]
    n_reviews = float(app[3])
    
   
    
    if name in reviews_max and reviews_max[name] < n_reviews:
        reviews_max[name] = n_reviews
    
    elif name not in reviews_max:
        reviews_max[name] = n_reviews

print(len(reviews_max))    
print('\n')

```

    9659
    
    



```python
android_clean = []
already_added = []

for app in google_dataset:
    name = app[0]
    n_reviews = float(app[3])
    
    if (reviews_max[name] == n_reviews) and (name not in already_added):
        android_clean.append(app)
        already_added.append(name)
               
print(len(android_clean))
```

    9659


In the first of the two above cells, we first created an empty dictionary called `reviews_max` and looped through the App Store dataset. The purpose of this dictionary was to weed out the duplicates by pairing unique app names as keys with the highest instance of reviews for this app. To do this, we set a condition that `if name in reviews_max and reviews_max[name] < n_reviews:`, `reviews_max`'s key would be updated to the higher number of reviews found in `n_reviews`. Or we could create a new dictionary key-pair entry if `name` was not yet in our `reviews_max` dictionary. These two conditionals are responsible for populating our dictionary and getting rid of our duplicates. So to ensure that we were on the right track, we made sure that our expected length of cleaned up data, 9659 rows, matched that of our actual length. So from here we used `len(reviews_max)`, to check the length of our dictionary table and just like with our estimation, our actual length was 9659 rows.

In the second cell, we initialized two empty lists, `android_clean` and `already_added`. We once again looped through `google_dataset` focusing on isolating the app name and the number of reviews and check to see if `n_reviews == reviews_max[name]` (in other words, check to see if the current row of the number of reviews is equal to the dictionary value in our `reviews_max` video, which is determined by the value of our name of our current row). The second part of this `if` statement, ` and (name not in already_added)`, is necessary because some duplicate apps have multiple entries where the highest number of reviews is the same, meaning that the duplicates would still go through without this condition.



```python
print(apple_dataset[813][1])
print(apple_dataset[6731][1])

print(android_clean[4412][0])
print(android_clean[7940][0])
```

    爱奇艺PPS -《欢乐颂2》电视剧热播
    【脱出ゲーム】絶対に最後までプレイしないで 〜謎解き＆ブロックパズル〜
    中国語 AQリスニング
    لعبة تقدر تربح DZ



```python
def isolate_english(string):
    
    false_counter = 0
    
    for character in string:
        code = ord(character)
        
        if code > 127:
            false_counter += 1
        
        
    if false_counter > 3:
        return False
            
    return True

android_english = []
apple_english = []

for apps in android_clean:
    name = apps[0]
    
    if isolate_english(name):
        android_english.append(apps)


for apps in apple_dataset:
    name = apps[1]
    
    if isolate_english(name):
        apple_english.append(apps)

printgoogle_header()        
explore_data(android_english, 0, 3, True, True)
printapple_header()
explore_data(apple_english, 0, 3, True, True)

```

    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver']
    
    
    ['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']
    Index number: 0
    The length of this row is 13
    
    
    ['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']
    Index number: 1
    The length of this row is 13
    
    
    ['Sketch - Draw & Paint', 'ART_AND_DESIGN', '4.5', '215644', '25M', '50,000,000+', 'Free', '0', 'Teen', 'Art & Design', 'June 8, 2018', 'Varies with device', '4.2 and up']
    Index number: 2
    The length of this row is 13
    
    
    Number of rows: 9614
    Number of columns: 13
    ['id', 'track_name', 'size_bytes', 'currency', 'price', 'rating_count_tot', 'rating_count_ver', 'user_rating', 'user_rating_ver', 'ver', 'cont_rating', 'prime_genre', 'sup_devices.num', 'ipadSc_urls.num', 'lang.num', 'vpp_lic']
    
    
    ['284882215', 'Facebook', '389879808', 'USD', '0.0', '2974676', '212', '3.5', '3.5', '95.0', '4+', 'Social Networking', '37', '1', '29', '1']
    Index number: 0
    The length of this row is 16
    
    
    ['389801252', 'Instagram', '113954816', 'USD', '0.0', '2161558', '1289', '4.5', '4.0', '10.23', '12+', 'Photo & Video', '37', '0', '29', '1']
    Index number: 1
    The length of this row is 16
    
    
    ['529479190', 'Clash of Clans', '116476928', 'USD', '0.0', '2130805', '579', '4.5', '4.5', '9.24.12', '9+', 'Games', '38', '5', '18', '1']
    Index number: 2
    The length of this row is 16
    
    
    Number of rows: 6183
    Number of columns: 16


In our newly cleaned data:

* App Store: 6183 rows remaining
* Google Play: 9614 rows remaining

## Separating the Free Apps

As we mentioned in the first paragraph, we're focusing only on free apps, so we're going to append only the apps where `price == '0.0'` or `price == '0'` in both of our datasets


```python
android_final = []
apple_final = []

for app in apple_english:
    price = app[4]
    if price == '0.0':
        apple_final.append(app)
    

for app in android_english:
    price = app[7]
    if price == '0':
        android_final.append(app)
        
print(len(android_final))
print(len(apple_final))
    

```

    8864
    3222


In the final length for our dataset, we have 8864 apps remaining for the Google Play Store and 3222 apps for the App Store

## Most Common Apps by Genre

We want to find an app profile that fits both the App Store and Google Play in order to maximize our revenue and profit. This is our validation strategy: 

1. Build a minimal Android version of the app, and add it to Google Play.
2. If the app has a good response from users, we develop it further.
3. If the app is profitable after six months, we build an iOS version of the app and add it to the App Store.

Because our end goal is to add the app on both Google Play and the App Store, we need to find app profiles that are successful in both markets. For instance, a profile that works well for both markets might be a productivity app that makes use of gamification.

We'll build our frequency tables based on `Genres` and `Category` for the Google Play store and for the App Store we'll be using the `prime_genre` column. 


```python
def freq_table(dataset, index):

    frequency_table = {}
    total = 0

    for rows in dataset:
        total += 1
        column = rows[index]
        if column in frequency_table:
            frequency_table[column] += 1
        else:
            frequency_table[column] = 1
            
    freq_percentages = {}    
    
    for key in frequency_table:
        percentage = (frequency_table[key] / total) * 100
        freq_percentages[key] = percentage
    
    return freq_percentages

def display_table(dataset, index):
    table = freq_table(dataset, index)
    table_display = []
    for key in table:
        key_val_as_tuple = (table[key], key)
        table_display.append(key_val_as_tuple)

    table_sorted = sorted(table_display, reverse = True)
    for entry in table_sorted:
        print(entry[1], ':', entry[0])

display_table(apple_final, -5) # Apple App Store- Prime Genres
print('\n')
display_table(android_final, -4) # Google Play Store- Genres
print('\n')
display_table(android_final, 1) #Google Play Store- Category
        
```

    Games : 58.16263190564867
    Entertainment : 7.883302296710118
    Photo & Video : 4.9658597144630665
    Education : 3.662321539416512
    Social Networking : 3.2898820608317814
    Shopping : 2.60707635009311
    Utilities : 2.5139664804469275
    Sports : 2.1415270018621975
    Music : 2.0484171322160147
    Health & Fitness : 2.0173805090006205
    Productivity : 1.7380509000620732
    Lifestyle : 1.5828677839851024
    News : 1.3345747982619491
    Travel : 1.2414649286157666
    Finance : 1.1173184357541899
    Weather : 0.8690254500310366
    Food & Drink : 0.8069522036002483
    Reference : 0.5586592178770949
    Business : 0.5276225946617008
    Book : 0.4345127250155183
    Navigation : 0.186219739292365
    Medical : 0.186219739292365
    Catalogs : 0.12414649286157665
    
    
    Tools : 8.449909747292418
    Entertainment : 6.069494584837545
    Education : 5.347472924187725
    Business : 4.591606498194946
    Productivity : 3.892148014440433
    Lifestyle : 3.892148014440433
    Finance : 3.7003610108303246
    Medical : 3.531137184115524
    Sports : 3.463447653429603
    Personalization : 3.3167870036101084
    Communication : 3.2378158844765346
    Action : 3.1024368231046933
    Health & Fitness : 3.0798736462093865
    Photography : 2.944494584837545
    News & Magazines : 2.7978339350180503
    Social : 2.6624548736462095
    Travel & Local : 2.3240072202166067
    Shopping : 2.2450361010830324
    Books & Reference : 2.1435018050541514
    Simulation : 2.0419675090252705
    Dating : 1.861462093862816
    Arcade : 1.8501805054151623
    Video Players & Editors : 1.7712093862815883
    Casual : 1.7599277978339352
    Maps & Navigation : 1.3989169675090252
    Food & Drink : 1.2409747292418771
    Puzzle : 1.128158844765343
    Racing : 0.9927797833935018
    Role Playing : 0.9363718411552346
    Libraries & Demo : 0.9363718411552346
    Auto & Vehicles : 0.9250902527075812
    Strategy : 0.9138086642599278
    House & Home : 0.8235559566787004
    Weather : 0.8009927797833934
    Events : 0.7107400722021661
    Adventure : 0.6768953068592057
    Comics : 0.6092057761732852
    Beauty : 0.5979241877256317
    Art & Design : 0.5979241877256317
    Parenting : 0.4963898916967509
    Card : 0.45126353790613716
    Casino : 0.42870036101083037
    Trivia : 0.41741877256317694
    Educational;Education : 0.39485559566787
    Board : 0.3835740072202166
    Educational : 0.3722924187725632
    Education;Education : 0.33844765342960287
    Word : 0.2594765342960289
    Casual;Pretend Play : 0.236913357400722
    Music : 0.2030685920577617
    Racing;Action & Adventure : 0.16922382671480143
    Puzzle;Brain Games : 0.16922382671480143
    Entertainment;Music & Video : 0.16922382671480143
    Casual;Brain Games : 0.13537906137184114
    Casual;Action & Adventure : 0.13537906137184114
    Arcade;Action & Adventure : 0.12409747292418773
    Action;Action & Adventure : 0.10153429602888085
    Educational;Pretend Play : 0.09025270758122744
    Simulation;Action & Adventure : 0.078971119133574
    Parenting;Education : 0.078971119133574
    Entertainment;Brain Games : 0.078971119133574
    Board;Brain Games : 0.078971119133574
    Parenting;Music & Video : 0.06768953068592057
    Educational;Brain Games : 0.06768953068592057
    Casual;Creativity : 0.06768953068592057
    Art & Design;Creativity : 0.06768953068592057
    Education;Pretend Play : 0.056407942238267145
    Role Playing;Pretend Play : 0.04512635379061372
    Education;Creativity : 0.04512635379061372
    Role Playing;Action & Adventure : 0.033844765342960284
    Puzzle;Action & Adventure : 0.033844765342960284
    Entertainment;Creativity : 0.033844765342960284
    Entertainment;Action & Adventure : 0.033844765342960284
    Educational;Creativity : 0.033844765342960284
    Educational;Action & Adventure : 0.033844765342960284
    Education;Music & Video : 0.033844765342960284
    Education;Brain Games : 0.033844765342960284
    Education;Action & Adventure : 0.033844765342960284
    Adventure;Action & Adventure : 0.033844765342960284
    Video Players & Editors;Music & Video : 0.02256317689530686
    Sports;Action & Adventure : 0.02256317689530686
    Simulation;Pretend Play : 0.02256317689530686
    Puzzle;Creativity : 0.02256317689530686
    Music;Music & Video : 0.02256317689530686
    Entertainment;Pretend Play : 0.02256317689530686
    Casual;Education : 0.02256317689530686
    Board;Action & Adventure : 0.02256317689530686
    Video Players & Editors;Creativity : 0.01128158844765343
    Trivia;Education : 0.01128158844765343
    Travel & Local;Action & Adventure : 0.01128158844765343
    Tools;Education : 0.01128158844765343
    Strategy;Education : 0.01128158844765343
    Strategy;Creativity : 0.01128158844765343
    Strategy;Action & Adventure : 0.01128158844765343
    Simulation;Education : 0.01128158844765343
    Role Playing;Brain Games : 0.01128158844765343
    Racing;Pretend Play : 0.01128158844765343
    Puzzle;Education : 0.01128158844765343
    Parenting;Brain Games : 0.01128158844765343
    Music & Audio;Music & Video : 0.01128158844765343
    Lifestyle;Pretend Play : 0.01128158844765343
    Lifestyle;Education : 0.01128158844765343
    Health & Fitness;Education : 0.01128158844765343
    Health & Fitness;Action & Adventure : 0.01128158844765343
    Entertainment;Education : 0.01128158844765343
    Communication;Creativity : 0.01128158844765343
    Comics;Creativity : 0.01128158844765343
    Casual;Music & Video : 0.01128158844765343
    Card;Action & Adventure : 0.01128158844765343
    Books & Reference;Education : 0.01128158844765343
    Art & Design;Pretend Play : 0.01128158844765343
    Art & Design;Action & Adventure : 0.01128158844765343
    Arcade;Pretend Play : 0.01128158844765343
    Adventure;Education : 0.01128158844765343
    
    
    FAMILY : 18.907942238267147
    GAME : 9.724729241877256
    TOOLS : 8.461191335740072
    BUSINESS : 4.591606498194946
    LIFESTYLE : 3.9034296028880866
    PRODUCTIVITY : 3.892148014440433
    FINANCE : 3.7003610108303246
    MEDICAL : 3.531137184115524
    SPORTS : 3.395758122743682
    PERSONALIZATION : 3.3167870036101084
    COMMUNICATION : 3.2378158844765346
    HEALTH_AND_FITNESS : 3.0798736462093865
    PHOTOGRAPHY : 2.944494584837545
    NEWS_AND_MAGAZINES : 2.7978339350180503
    SOCIAL : 2.6624548736462095
    TRAVEL_AND_LOCAL : 2.33528880866426
    SHOPPING : 2.2450361010830324
    BOOKS_AND_REFERENCE : 2.1435018050541514
    DATING : 1.861462093862816
    VIDEO_PLAYERS : 1.7937725631768955
    MAPS_AND_NAVIGATION : 1.3989169675090252
    FOOD_AND_DRINK : 1.2409747292418771
    EDUCATION : 1.1620036101083033
    ENTERTAINMENT : 0.9589350180505415
    LIBRARIES_AND_DEMO : 0.9363718411552346
    AUTO_AND_VEHICLES : 0.9250902527075812
    HOUSE_AND_HOME : 0.8235559566787004
    WEATHER : 0.8009927797833934
    EVENTS : 0.7107400722021661
    PARENTING : 0.6543321299638989
    ART_AND_DESIGN : 0.6430505415162455
    COMICS : 0.6204873646209386
    BEAUTY : 0.5979241877256317


For our Apple Dataset, our most common genre is games. The next highest is entertainment. Education is only around 3.7 percent which is much lower than I expected. Entertainment related apps in general seem to have a higher level of engagement compared to other categories.

For our Android Dataset, the most popular apps appear to be tools, family apps, and more practical apps rather than games.


## Most Popular Apps on the App Store (By Genre)

Next we're going to create a frequency table that will calculate the number of ratings per genre, so that we can get an idea of how popular an app is.


```python
genres_os = freq_table(apple_final, -5)

for genre in genres_os:
    
    total = 0
    len_genre = 0
    
    for row in apple_final:
        
        genre_app = row[-5]
        if genre == genre_app:
            ratings = float(row[5])
            total += ratings
            len_genre += 1

    avg_number = total / len_genre 
    print(genre, ':', avg_number)
            
```

    Social Networking : 71548.34905660378
    Photo & Video : 28441.54375
    Games : 22788.6696905016
    Music : 57326.530303030304
    Reference : 74942.11111111111
    Health & Fitness : 23298.015384615384
    Weather : 52279.892857142855
    Utilities : 18684.456790123455
    Travel : 28243.8
    Shopping : 26919.690476190477
    News : 21248.023255813954
    Navigation : 86090.33333333333
    Lifestyle : 16485.764705882353
    Entertainment : 14029.830708661417
    Food & Drink : 33333.92307692308
    Sports : 23008.898550724636
    Book : 39758.5
    Finance : 31467.944444444445
    Education : 7003.983050847458
    Productivity : 21028.410714285714
    Business : 7491.117647058823
    Catalogs : 4004.0
    Medical : 612.0


For our Apple Store results, we can see that our most popular genre is most likely navigation apps. But it probably isn't accurate because it's being influenced largely by Google Maps and Waze. This same trend would also apply to 'Social Networking' apps, where a the amount of ratings will be skewed towards a few big apps like Facebook, Pinterest, Skype, etc. 


```python
for app in apple_final:
    genre = app[-5]
    if genre == 'Navigation':
        print(app[1], ':', app[5])
```

    Waze - GPS Navigation, Maps & Real-time Traffic : 345046
    Google Maps - Navigation & Transit : 154911
    Geocaching® : 12811
    CoPilot GPS – Car Navigation & Offline Maps : 3582
    ImmobilienScout24: Real Estate Search in Germany : 187
    Railway Route Search : 5


As we expected, the skewing here is very heavy and I don't see an opportunity for us to slip in and make our mark here

Let's try another category that is a bit more niche, like the "Reference" category.


```python
for app in apple_final:
    if app[-5] == 'Reference':
        print(app[1], ':', app[5])
```

    Bible : 985920
    Dictionary.com Dictionary & Thesaurus : 200047
    Dictionary.com Dictionary & Thesaurus for iPad : 54175
    Google Translate : 26786
    Muslim Pro: Ramadan 2017 Prayer Times, Azan, Quran : 18418
    New Furniture Mods - Pocket Wiki & Game Tools for Minecraft PC Edition : 17588
    Merriam-Webster Dictionary : 16849
    Night Sky : 12122
    City Maps for Minecraft PE - The Best Maps for Minecraft Pocket Edition (MCPE) : 8535
    LUCKY BLOCK MOD ™ for Minecraft PC Edition - The Best Pocket Wiki & Mods Installer Tools : 4693
    GUNS MODS for Minecraft PC Edition - Mods Tools : 1497
    Guides for Pokémon GO - Pokemon GO News and Cheats : 826
    WWDC : 762
    Horror Maps for Minecraft PE - Download The Scariest Maps for Minecraft Pocket Edition (MCPE) Free : 718
    VPN Express : 14
    Real Bike Traffic Rider Virtual Reality Glasses : 8
    教えて!goo : 0
    Jishokun-Japanese English Dictionary & Translator : 0


Even with a bit of top-heaviness, this genre is still something that we can entertain finding a niche in. We can do something like take a popular book and soup it up a bit (I'll explain this in more detail later). And we can also make a guide for a popular game like "Minecraft" (in the output above), Fortnite or perhaps even other games!

We know that since our app is going to be free, these types of app ideas can provide great ad revenue as well as in-app purchase potential for monetization.

The book genre is also something that seems to overlap a bit with the reference genre and meshes well with our app ideas as well.

The other popular app genres aren't quite as inviting because there will naturally be either a lot more infrastructure needed(Food & Drink) or users don't spend enough time there (Weather), so monetizing them will be difficult.


## Most Popular Apps on the Play Store (By # of Installs).

For the Google Play Store apps, we actually have info about the number of installs, unlike our Apple Data.


```python
display_table(android_final, 5) # the Installs columns
```

    1,000,000+ : 15.726534296028879
    100,000+ : 11.552346570397113
    10,000,000+ : 10.548285198555957
    10,000+ : 10.198555956678701
    1,000+ : 8.393501805054152
    100+ : 6.915613718411552
    5,000,000+ : 6.825361010830325
    500,000+ : 5.561823104693141
    50,000+ : 4.7721119133574
    5,000+ : 4.512635379061372
    10+ : 3.5424187725631766
    500+ : 3.2490974729241873
    50,000,000+ : 2.3014440433213
    100,000,000+ : 2.1322202166064983
    50+ : 1.917870036101083
    5+ : 0.78971119133574
    1+ : 0.5076714801444043
    500,000,000+ : 0.2707581227436823
    1,000,000,000+ : 0.22563176895306858
    0+ : 0.04512635379061372
    0 : 0.01128158844765343


Next, we would like to perform computations and to do that, we are going to have to eliminate any '+' and ',' characters. So in our next cell, we will generate a frequency table for our Play Store dataset, replace the superfluous characters and organize all of the genres by their average number of installs.


```python
genres_android = freq_table(android_final, 1)

for category in genres_android:
    total = 0
    len_category = 0
    
    for app in android_final:
        category_app = app[1]
        if category_app == category:
            n_installs = app[5]
            n_installs = n_installs.replace('+', '')
            n_installs = n_installs.replace(',', '')
            total += float(n_installs)
            len_category += 1
    
    avg_n_installs = total / len_category
    print(category, ':', avg_n_installs )
            
      
```

    ART_AND_DESIGN : 1986335.0877192982
    AUTO_AND_VEHICLES : 647317.8170731707
    BEAUTY : 513151.88679245283
    BOOKS_AND_REFERENCE : 8767811.894736841
    BUSINESS : 1712290.1474201474
    COMICS : 817657.2727272727
    COMMUNICATION : 38456119.167247385
    DATING : 854028.8303030303
    EDUCATION : 1833495.145631068
    ENTERTAINMENT : 11640705.88235294
    EVENTS : 253542.22222222222
    FINANCE : 1387692.475609756
    FOOD_AND_DRINK : 1924897.7363636363
    HEALTH_AND_FITNESS : 4188821.9853479853
    HOUSE_AND_HOME : 1331540.5616438356
    LIBRARIES_AND_DEMO : 638503.734939759
    LIFESTYLE : 1437816.2687861272
    GAME : 15588015.603248259
    FAMILY : 3695641.8198090694
    MEDICAL : 120550.61980830671
    SOCIAL : 23253652.127118643
    SHOPPING : 7036877.311557789
    PHOTOGRAPHY : 17840110.40229885
    SPORTS : 3638640.1428571427
    TRAVEL_AND_LOCAL : 13984077.710144928
    TOOLS : 10801391.298666667
    PERSONALIZATION : 5201482.6122448975
    PRODUCTIVITY : 16787331.344927534
    PARENTING : 542603.6206896552
    WEATHER : 5074486.197183099
    VIDEO_PLAYERS : 24727872.452830188
    NEWS_AND_MAGAZINES : 9549178.467741935
    MAPS_AND_NAVIGATION : 4056941.7741935486


It seems that communication apps have the most amount of installs on average, at arount 38456119 installs. But is that information actually useful to us? Let's try something in the next cell.


```python
for app in android_final:
    if app[1] == 'COMMUNICATION' and (app[5] == '1,000,000,000+'
                                      or app[5] == '500,000,000+'
                                      or app[5] == '100,000,000+'):
        print(app[0], ':', app[5])
```

    WhatsApp Messenger : 1,000,000,000+
    imo beta free calls and text : 100,000,000+
    Android Messages : 100,000,000+
    Google Duo - High Quality Video Calls : 500,000,000+
    Messenger – Text and Video Chat for Free : 1,000,000,000+
    imo free video calls and chat : 500,000,000+
    Skype - free IM & video calls : 1,000,000,000+
    Who : 100,000,000+
    GO SMS Pro - Messenger, Free Themes, Emoji : 100,000,000+
    LINE: Free Calls & Messages : 500,000,000+
    Google Chrome: Fast & Secure : 1,000,000,000+
    Firefox Browser fast & private : 100,000,000+
    UC Browser - Fast Download Private & Secure : 500,000,000+
    Gmail : 1,000,000,000+
    Hangouts : 1,000,000,000+
    Messenger Lite: Free Calls & Messages : 100,000,000+
    Kik : 100,000,000+
    KakaoTalk: Free Calls & Text : 100,000,000+
    Opera Mini - fast web browser : 100,000,000+
    Opera Browser: Fast and Secure : 100,000,000+
    Telegram : 100,000,000+
    Truecaller: Caller ID, SMS spam blocking & Dialer : 100,000,000+
    UC Browser Mini -Tiny Fast Private & Secure : 100,000,000+
    Viber Messenger : 500,000,000+
    WeChat : 100,000,000+
    Yahoo Mail – Stay Organized : 100,000,000+
    BBM - Free Calls & Messages : 100,000,000+


Once again, the problem is that there are a lot of huge apps that make up the bulk of these bloated install numbers. If we were to remove these apps, the average for the communication category will plunge sharply.

We should try another category like books and reference. Perhaps we won't once again run into the phenomenon of niches that are dominated by disproportionately huge apps.


```python
for app in android_final:
    if app[1] == 'BOOKS_AND_REFERENCE':
        print(app[0], ':', app[5])
```

    E-Book Read - Read Book for free : 50,000+
    Download free book with green book : 100,000+
    Wikipedia : 10,000,000+
    Cool Reader : 10,000,000+
    Free Panda Radio Music : 100,000+
    Book store : 1,000,000+
    FBReader: Favorite Book Reader : 10,000,000+
    English Grammar Complete Handbook : 500,000+
    Free Books - Spirit Fanfiction and Stories : 1,000,000+
    Google Play Books : 1,000,000,000+
    AlReader -any text book reader : 5,000,000+
    Offline English Dictionary : 100,000+
    Offline: English to Tagalog Dictionary : 500,000+
    FamilySearch Tree : 1,000,000+
    Cloud of Books : 1,000,000+
    Recipes of Prophetic Medicine for free : 500,000+
    ReadEra – free ebook reader : 1,000,000+
    Anonymous caller detection : 10,000+
    Ebook Reader : 5,000,000+
    Litnet - E-books : 100,000+
    Read books online : 5,000,000+
    English to Urdu Dictionary : 500,000+
    eBoox: book reader fb2 epub zip : 1,000,000+
    English Persian Dictionary : 500,000+
    Flybook : 500,000+
    All Maths Formulas : 1,000,000+
    Ancestry : 5,000,000+
    HTC Help : 10,000,000+
    English translation from Bengali : 100,000+
    Pdf Book Download - Read Pdf Book : 100,000+
    Free Book Reader : 100,000+
    eBoox new: Reader for fb2 epub zip books : 50,000+
    Only 30 days in English, the guideline is guaranteed : 500,000+
    Moon+ Reader : 10,000,000+
    SH-02J Owner's Manual (Android 8.0) : 50,000+
    English-Myanmar Dictionary : 1,000,000+
    Golden Dictionary (EN-AR) : 1,000,000+
    All Language Translator Free : 1,000,000+
    Azpen eReader : 500,000+
    URBANO V 02 instruction manual : 100,000+
    Bible : 100,000,000+
    C Programs and Reference : 50,000+
    C Offline Tutorial : 1,000+
    C Programs Handbook : 50,000+
    Amazon Kindle : 100,000,000+
    Aab e Hayat Full Novel : 100,000+
    Aldiko Book Reader : 10,000,000+
    Google I/O 2018 : 500,000+
    R Language Reference Guide : 10,000+
    Learn R Programming Full : 5,000+
    R Programing Offline Tutorial : 1,000+
    Guide for R Programming : 5+
    Learn R Programming : 10+
    R Quick Reference Big Data : 1,000+
    V Made : 100,000+
    Wattpad 📖 Free Books : 100,000,000+
    Dictionary - WordWeb : 5,000,000+
    Guide (for X-MEN) : 100,000+
    AC Air condition Troubleshoot,Repair,Maintenance : 5,000+
    AE Bulletins : 1,000+
    Ae Allah na Dai (Rasa) : 10,000+
    50000 Free eBooks & Free AudioBooks : 5,000,000+
    Ag PhD Field Guide : 10,000+
    Ag PhD Deficiencies : 10,000+
    Ag PhD Planting Population Calculator : 1,000+
    Ag PhD Soybean Diseases : 1,000+
    Fertilizer Removal By Crop : 50,000+
    A-J Media Vault : 50+
    Al-Quran (Free) : 10,000,000+
    Al Quran (Tafsir & by Word) : 500,000+
    Al Quran Indonesia : 10,000,000+
    Al'Quran Bahasa Indonesia : 10,000,000+
    Al Quran Al karim : 1,000,000+
    Al-Muhaffiz : 50,000+
    Al Quran : EAlim - Translations & MP3 Offline : 5,000,000+
    Al-Quran 30 Juz free copies : 500,000+
    Koran Read &MP3 30 Juz Offline : 1,000,000+
    Hafizi Quran 15 lines per page : 1,000,000+
    Quran for Android : 10,000,000+
    Surah Al-Waqiah : 100,000+
    Hisnul Al Muslim - Hisn Invocations & Adhkaar : 100,000+
    Satellite AR : 1,000,000+
    Audiobooks from Audible : 100,000,000+
    Kinot & Eichah for Tisha B'Av : 10,000+
    AW Tozer Devotionals - Daily : 5,000+
    Tozer Devotional -Series 1 : 1,000+
    The Pursuit of God : 1,000+
    AY Sing : 5,000+
    Ay Hasnain k Nana Milad Naat : 10,000+
    Ay Mohabbat Teri Khatir Novel : 10,000+
    Arizona Statutes, ARS (AZ Law) : 1,000+
    Oxford A-Z of English Usage : 1,000,000+
    BD Fishpedia : 1,000+
    BD All Sim Offer : 10,000+
    Youboox - Livres, BD et magazines : 500,000+
    B&H Kids AR : 10,000+
    B y H Niños ES : 5,000+
    Dictionary.com: Find Definitions for English Words : 10,000,000+
    English Dictionary - Offline : 10,000,000+
    Bible KJV : 5,000,000+
    Borneo Bible, BM Bible : 10,000+
    MOD Black for BM : 100+
    BM Box : 1,000+
    Anime Mod for BM : 100+
    NOOK: Read eBooks & Magazines : 10,000,000+
    NOOK Audiobooks : 500,000+
    NOOK App for NOOK Devices : 500,000+
    Browsery by Barnes & Noble : 5,000+
    bp e-store : 1,000+
    Brilliant Quotes: Life, Love, Family & Motivation : 1,000,000+
    BR Ambedkar Biography & Quotes : 10,000+
    BU Alsace : 100+
    Catholic La Bu Zo Kam : 500+
    Khrifa Hla Bu (Solfa) : 10+
    Kristian Hla Bu : 10,000+
    SA HLA BU : 1,000+
    Learn SAP BW : 500+
    Learn SAP BW on HANA : 500+
    CA Laws 2018 (California Laws and Codes) : 5,000+
    Bootable Methods(USB-CD-DVD) : 10,000+
    cloudLibrary : 100,000+
    SDA Collegiate Quarterly : 500+
    Sabbath School : 100,000+
    Cypress College Library : 100+
    Stats Royale for Clash Royale : 1,000,000+
    GATE 21 years CS Papers(2011-2018 Solved) : 50+
    Learn CT Scan Of Head : 5,000+
    Easy Cv maker 2018 : 10,000+
    How to Write CV : 100,000+
    CW Nuclear : 1,000+
    CY Spray nozzle : 10+
    BibleRead En Cy Zh Yue : 5+
    CZ-Help : 5+
    Modlitební knížka CZ : 500+
    Guide for DB Xenoverse : 10,000+
    Guide for DB Xenoverse 2 : 10,000+
    Guide for IMS DB : 10+
    DC HSEMA : 5,000+
    DC Public Library : 1,000+
    Painting Lulu DC Super Friends : 1,000+
    Dictionary : 10,000,000+
    Fix Error Google Playstore : 1,000+
    D. H. Lawrence Poems FREE : 1,000+
    Bilingual Dictionary Audio App : 5,000+
    DM Screen : 10,000+
    wikiHow: how to do anything : 1,000,000+
    Dr. Doug's Tips : 1,000+
    Bible du Semeur-BDS (French) : 50,000+
    La citadelle du musulman : 50,000+
    DV 2019 Entry Guide : 10,000+
    DV 2019 - EDV Photo & Form : 50,000+
    DV 2018 Winners Guide : 1,000+
    EB Annual Meetings : 1,000+
    EC - AP & Telangana : 5,000+
    TN Patta Citta & EC : 10,000+
    AP Stamps and Registration : 10,000+
    CompactiMa EC pH Calibration : 100+
    EGW Writings 2 : 100,000+
    EGW Writings : 1,000,000+
    Bible with EGW Comments : 100,000+
    My Little Pony AR Guide : 1,000,000+
    SDA Sabbath School Quarterly : 500,000+
    Duaa Ek Ibaadat : 5,000+
    Spanish English Translator : 10,000,000+
    Dictionary - Merriam-Webster : 10,000,000+
    JW Library : 10,000,000+
    Oxford Dictionary of English : Free : 10,000,000+
    English Hindi Dictionary : 10,000,000+
    English to Hindi Dictionary : 5,000,000+
    EP Research Service : 1,000+
    Hymnes et Louanges : 100,000+
    EU Charter : 1,000+
    EU Data Protection : 1,000+
    EU IP Codes : 100+
    EW PDF : 5+
    BakaReader EX : 100,000+
    EZ Quran : 50,000+
    FA Part 1 & 2 Past Papers Solved Free – Offline : 5,000+
    La Fe de Jesus : 1,000+
    La Fe de Jesús : 500+
    Le Fe de Jesus : 500+
    Florida - Pocket Brainbook : 1,000+
    Florida Statutes (FL Code) : 1,000+
    English To Shona Dictionary : 10,000+
    Greek Bible FP (Audio) : 1,000+
    Golden Dictionary (FR-AR) : 500,000+
    Fanfic-FR : 5,000+
    Bulgarian French Dictionary Fr : 10,000+
    Chemin (fr) : 1,000+
    The SCP Foundation DB fr nn5n : 1,000+


From these results, we can see that the book and reference has a variety of apps such as:
* eBooks
* Dictionaries
* Language Guides
* Video Game Guides
* Religious Texts
* Libraries/Compilations of readings
* Programming Texts
* And more...

However, there are still a few dominant apps in this genre that we have to account for. In the next cell, we are going to see how many of those dominant apps we have to deal with exactly.


```python
for app in android_final:
    if app[1] == 'BOOKS_AND_REFERENCE' and (app[5] == '1,000,000,000+'
                                            or app[5] == '500,000,000+'
                                            or app[5] == '100,000,000+'):
        print(app[0], ':', app[5])
```

    Google Play Books : 1,000,000,000+
    Bible : 100,000,000+
    Amazon Kindle : 100,000,000+
    Wattpad 📖 Free Books : 100,000,000+
    Audiobooks from Audible : 100,000,000+


There are only a few super dominant apps, so maybe we still have a chance to get some traction within this genre. Let's try to get ideas from the apps that are in the 1,000,000 to the 100,000,000 range!


```python
for app in android_final:
    if app[1] == 'BOOKS_AND_REFERENCE' and (app[5] == '1,000,000+'
                                            or app[5] == '5,000,000+'
                                            or app[5] == '10,000,000+'
                                            or app[5] == '50,000,000+'):
        print(app[0], ':', app[5])
```

    Wikipedia : 10,000,000+
    Cool Reader : 10,000,000+
    Book store : 1,000,000+
    FBReader: Favorite Book Reader : 10,000,000+
    Free Books - Spirit Fanfiction and Stories : 1,000,000+
    AlReader -any text book reader : 5,000,000+
    FamilySearch Tree : 1,000,000+
    Cloud of Books : 1,000,000+
    ReadEra – free ebook reader : 1,000,000+
    Ebook Reader : 5,000,000+
    Read books online : 5,000,000+
    eBoox: book reader fb2 epub zip : 1,000,000+
    All Maths Formulas : 1,000,000+
    Ancestry : 5,000,000+
    HTC Help : 10,000,000+
    Moon+ Reader : 10,000,000+
    English-Myanmar Dictionary : 1,000,000+
    Golden Dictionary (EN-AR) : 1,000,000+
    All Language Translator Free : 1,000,000+
    Aldiko Book Reader : 10,000,000+
    Dictionary - WordWeb : 5,000,000+
    50000 Free eBooks & Free AudioBooks : 5,000,000+
    Al-Quran (Free) : 10,000,000+
    Al Quran Indonesia : 10,000,000+
    Al'Quran Bahasa Indonesia : 10,000,000+
    Al Quran Al karim : 1,000,000+
    Al Quran : EAlim - Translations & MP3 Offline : 5,000,000+
    Koran Read &MP3 30 Juz Offline : 1,000,000+
    Hafizi Quran 15 lines per page : 1,000,000+
    Quran for Android : 10,000,000+
    Satellite AR : 1,000,000+
    Oxford A-Z of English Usage : 1,000,000+
    Dictionary.com: Find Definitions for English Words : 10,000,000+
    English Dictionary - Offline : 10,000,000+
    Bible KJV : 5,000,000+
    NOOK: Read eBooks & Magazines : 10,000,000+
    Brilliant Quotes: Life, Love, Family & Motivation : 1,000,000+
    Stats Royale for Clash Royale : 1,000,000+
    Dictionary : 10,000,000+
    wikiHow: how to do anything : 1,000,000+
    EGW Writings : 1,000,000+
    My Little Pony AR Guide : 1,000,000+
    Spanish English Translator : 10,000,000+
    Dictionary - Merriam-Webster : 10,000,000+
    JW Library : 10,000,000+
    Oxford Dictionary of English : Free : 10,000,000+
    English Hindi Dictionary : 10,000,000+
    English to Hindi Dictionary : 5,000,000+


Within this range of installs for the app, there seems to be a lot of libraries, ebook readers, dictionaries and religious texts. So as long as we avoid specifically these kinds of apps, we can probably carve out a niche for ourselves in the books and reference genre(category).

Although the idea of building an app around the Bible or the Quran is a niche that has already sailed (due to oversaturation), the concept itself is still something that we can apply to our own app construction. As mentioned with the App Store "Reference" genre, we can use this concept to build an app around a popular book like say "Harry Potter", "Game of Thrones", "The Witcher'', or others for example and maybe add enhanced features like audio, pop-up facts, additional lore, community interaction and more. And going by the "Stats Royale for Clash Royale '', which  features over 1,000,000 installs, we can also build an app that serves as a companion guide or stat tracker for a popular game.


### Recap/Conclusion

For this project, we came into it with the purpose of analyzing two discrete datasets from the Apple App Store and Google's Play Store with the idea of desigining our own free app profile that could be popular on both markets.

After cleaning up the data, generating frequency tables and performing analysis on our cleaned data, we concluded that the best app profile that we could recommend would be once that be a book. We could use one of these approaches:
1. Build an app for a popular book that provides a lot of extra features like trivia, audio, community interaction, etc.
2. Build an app that serves as a companion guide or stat tracker for a popular game

If we do this, I am confident that avoid clashing with the giants of the genre and carve out our own niche with a unique base of customers.
