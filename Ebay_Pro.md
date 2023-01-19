# German eBar Car Sales Analysis

![image](https://i.imgur.com/GcK6W4U.png)

This dataset introduces the classifieds section of the German eBay website. Our goal is to clean this dataset and analyze the used car listings that are present in the dataset.

## Exploring the Data


```python
# Load all the packages that we
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
autos = pd.read_csv('autos.csv', encoding='latin-1')
%matplotlib inline
```


```python
# Taking a glance at the dataset
autos
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>dateCrawled</th>
      <th>name</th>
      <th>seller</th>
      <th>offerType</th>
      <th>price</th>
      <th>abtest</th>
      <th>vehicleType</th>
      <th>yearOfRegistration</th>
      <th>gearbox</th>
      <th>powerPS</th>
      <th>model</th>
      <th>odometer</th>
      <th>monthOfRegistration</th>
      <th>fuelType</th>
      <th>brand</th>
      <th>notRepairedDamage</th>
      <th>dateCreated</th>
      <th>nrOfPictures</th>
      <th>postalCode</th>
      <th>lastSeen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-03-26 17:47:46</td>
      <td>Peugeot_807_160_NAVTECH_ON_BOARD</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$5,000</td>
      <td>control</td>
      <td>bus</td>
      <td>2004</td>
      <td>manuell</td>
      <td>158</td>
      <td>andere</td>
      <td>150,000km</td>
      <td>3</td>
      <td>lpg</td>
      <td>peugeot</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>79588</td>
      <td>2016-04-06 06:45:54</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-04-04 13:38:56</td>
      <td>BMW_740i_4_4_Liter_HAMANN_UMBAU_Mega_Optik</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,500</td>
      <td>control</td>
      <td>limousine</td>
      <td>1997</td>
      <td>automatik</td>
      <td>286</td>
      <td>7er</td>
      <td>150,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>bmw</td>
      <td>nein</td>
      <td>2016-04-04 00:00:00</td>
      <td>0</td>
      <td>71034</td>
      <td>2016-04-06 14:45:08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-03-26 18:57:24</td>
      <td>Volkswagen_Golf_1.6_United</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,990</td>
      <td>test</td>
      <td>limousine</td>
      <td>2009</td>
      <td>manuell</td>
      <td>102</td>
      <td>golf</td>
      <td>70,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>35394</td>
      <td>2016-04-06 20:15:37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-03-12 16:58:10</td>
      <td>Smart_smart_fortwo_coupe_softouch/F1/Klima/Pan...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$4,350</td>
      <td>control</td>
      <td>kleinwagen</td>
      <td>2007</td>
      <td>automatik</td>
      <td>71</td>
      <td>fortwo</td>
      <td>70,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>smart</td>
      <td>nein</td>
      <td>2016-03-12 00:00:00</td>
      <td>0</td>
      <td>33729</td>
      <td>2016-03-15 03:16:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-04-01 14:38:50</td>
      <td>Ford_Focus_1_6_Benzin_TÜV_neu_ist_sehr_gepfleg...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$1,350</td>
      <td>test</td>
      <td>kombi</td>
      <td>2003</td>
      <td>manuell</td>
      <td>0</td>
      <td>focus</td>
      <td>150,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>ford</td>
      <td>nein</td>
      <td>2016-04-01 00:00:00</td>
      <td>0</td>
      <td>39218</td>
      <td>2016-04-01 14:38:50</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49995</th>
      <td>2016-03-27 14:38:19</td>
      <td>Audi_Q5_3.0_TDI_qu._S_tr.__Navi__Panorama__Xenon</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$24,900</td>
      <td>control</td>
      <td>limousine</td>
      <td>2011</td>
      <td>automatik</td>
      <td>239</td>
      <td>q5</td>
      <td>100,000km</td>
      <td>1</td>
      <td>diesel</td>
      <td>audi</td>
      <td>nein</td>
      <td>2016-03-27 00:00:00</td>
      <td>0</td>
      <td>82131</td>
      <td>2016-04-01 13:47:40</td>
    </tr>
    <tr>
      <th>49996</th>
      <td>2016-03-28 10:50:25</td>
      <td>Opel_Astra_F_Cabrio_Bertone_Edition___TÜV_neu+...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$1,980</td>
      <td>control</td>
      <td>cabrio</td>
      <td>1996</td>
      <td>manuell</td>
      <td>75</td>
      <td>astra</td>
      <td>150,000km</td>
      <td>5</td>
      <td>benzin</td>
      <td>opel</td>
      <td>nein</td>
      <td>2016-03-28 00:00:00</td>
      <td>0</td>
      <td>44807</td>
      <td>2016-04-02 14:18:02</td>
    </tr>
    <tr>
      <th>49997</th>
      <td>2016-04-02 14:44:48</td>
      <td>Fiat_500_C_1.2_Dualogic_Lounge</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$13,200</td>
      <td>test</td>
      <td>cabrio</td>
      <td>2014</td>
      <td>automatik</td>
      <td>69</td>
      <td>500</td>
      <td>5,000km</td>
      <td>11</td>
      <td>benzin</td>
      <td>fiat</td>
      <td>nein</td>
      <td>2016-04-02 00:00:00</td>
      <td>0</td>
      <td>73430</td>
      <td>2016-04-04 11:47:27</td>
    </tr>
    <tr>
      <th>49998</th>
      <td>2016-03-08 19:25:42</td>
      <td>Audi_A3_2.0_TDI_Sportback_Ambition</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$22,900</td>
      <td>control</td>
      <td>kombi</td>
      <td>2013</td>
      <td>manuell</td>
      <td>150</td>
      <td>a3</td>
      <td>40,000km</td>
      <td>11</td>
      <td>diesel</td>
      <td>audi</td>
      <td>nein</td>
      <td>2016-03-08 00:00:00</td>
      <td>0</td>
      <td>35683</td>
      <td>2016-04-05 16:45:07</td>
    </tr>
    <tr>
      <th>49999</th>
      <td>2016-03-14 00:42:12</td>
      <td>Opel_Vectra_1.6_16V</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$1,250</td>
      <td>control</td>
      <td>limousine</td>
      <td>1996</td>
      <td>manuell</td>
      <td>101</td>
      <td>vectra</td>
      <td>150,000km</td>
      <td>1</td>
      <td>benzin</td>
      <td>opel</td>
      <td>nein</td>
      <td>2016-03-13 00:00:00</td>
      <td>0</td>
      <td>45897</td>
      <td>2016-04-06 21:18:48</td>
    </tr>
  </tbody>
</table>
<p>50000 rows × 20 columns</p>
</div>




```python
autos.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 50000 entries, 0 to 49999
    Data columns (total 20 columns):
     #   Column               Non-Null Count  Dtype 
    ---  ------               --------------  ----- 
     0   dateCrawled          50000 non-null  object
     1   name                 50000 non-null  object
     2   seller               50000 non-null  object
     3   offerType            50000 non-null  object
     4   price                50000 non-null  object
     5   abtest               50000 non-null  object
     6   vehicleType          44905 non-null  object
     7   yearOfRegistration   50000 non-null  int64 
     8   gearbox              47320 non-null  object
     9   powerPS              50000 non-null  int64 
     10  model                47242 non-null  object
     11  odometer             50000 non-null  object
     12  monthOfRegistration  50000 non-null  int64 
     13  fuelType             45518 non-null  object
     14  brand                50000 non-null  object
     15  notRepairedDamage    40171 non-null  object
     16  dateCreated          50000 non-null  object
     17  nrOfPictures         50000 non-null  int64 
     18  postalCode           50000 non-null  int64 
     19  lastSeen             50000 non-null  object
    dtypes: int64(5), object(15)
    memory usage: 7.6+ MB



```python
autos.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>dateCrawled</th>
      <th>name</th>
      <th>seller</th>
      <th>offerType</th>
      <th>price</th>
      <th>abtest</th>
      <th>vehicleType</th>
      <th>yearOfRegistration</th>
      <th>gearbox</th>
      <th>powerPS</th>
      <th>model</th>
      <th>odometer</th>
      <th>monthOfRegistration</th>
      <th>fuelType</th>
      <th>brand</th>
      <th>notRepairedDamage</th>
      <th>dateCreated</th>
      <th>nrOfPictures</th>
      <th>postalCode</th>
      <th>lastSeen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-03-26 17:47:46</td>
      <td>Peugeot_807_160_NAVTECH_ON_BOARD</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$5,000</td>
      <td>control</td>
      <td>bus</td>
      <td>2004</td>
      <td>manuell</td>
      <td>158</td>
      <td>andere</td>
      <td>150,000km</td>
      <td>3</td>
      <td>lpg</td>
      <td>peugeot</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>79588</td>
      <td>2016-04-06 06:45:54</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-04-04 13:38:56</td>
      <td>BMW_740i_4_4_Liter_HAMANN_UMBAU_Mega_Optik</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,500</td>
      <td>control</td>
      <td>limousine</td>
      <td>1997</td>
      <td>automatik</td>
      <td>286</td>
      <td>7er</td>
      <td>150,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>bmw</td>
      <td>nein</td>
      <td>2016-04-04 00:00:00</td>
      <td>0</td>
      <td>71034</td>
      <td>2016-04-06 14:45:08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-03-26 18:57:24</td>
      <td>Volkswagen_Golf_1.6_United</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$8,990</td>
      <td>test</td>
      <td>limousine</td>
      <td>2009</td>
      <td>manuell</td>
      <td>102</td>
      <td>golf</td>
      <td>70,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>0</td>
      <td>35394</td>
      <td>2016-04-06 20:15:37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-03-12 16:58:10</td>
      <td>Smart_smart_fortwo_coupe_softouch/F1/Klima/Pan...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$4,350</td>
      <td>control</td>
      <td>kleinwagen</td>
      <td>2007</td>
      <td>automatik</td>
      <td>71</td>
      <td>fortwo</td>
      <td>70,000km</td>
      <td>6</td>
      <td>benzin</td>
      <td>smart</td>
      <td>nein</td>
      <td>2016-03-12 00:00:00</td>
      <td>0</td>
      <td>33729</td>
      <td>2016-03-15 03:16:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-04-01 14:38:50</td>
      <td>Ford_Focus_1_6_Benzin_TÜV_neu_ist_sehr_gepfleg...</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$1,350</td>
      <td>test</td>
      <td>kombi</td>
      <td>2003</td>
      <td>manuell</td>
      <td>0</td>
      <td>focus</td>
      <td>150,000km</td>
      <td>7</td>
      <td>benzin</td>
      <td>ford</td>
      <td>nein</td>
      <td>2016-04-01 00:00:00</td>
      <td>0</td>
      <td>39218</td>
      <td>2016-04-01 14:38:50</td>
    </tr>
  </tbody>
</table>
</div>



From my observations of the data thus far, we have 20 columns in this data set and there are five columns that have null values out of these 20. They are: `vehicleType`, `gearbox`,`model`,`fuelType`,`notRepairedDamage`

Next we're going to check our columns to make sure that they are in an easy-to-work with format in the following cells.


```python
autos.columns 
```




    Index(['dateCrawled', 'name', 'seller', 'offerType', 'price', 'abtest',
           'vehicleType', 'yearOfRegistration', 'gearbox', 'powerPS', 'model',
           'odometer', 'monthOfRegistration', 'fuelType', 'brand',
           'notRepairedDamage', 'dateCreated', 'nrOfPictures', 'postalCode',
           'lastSeen'],
          dtype='object')




```python
snakecase_names = ['date_crawled', 'name', 'seller', 'offer_type', 'price', 'ab_test',
       'vehicle_type', 'registration_year', 'gearbox', 'power_ps', 'model',
       'odometer', 'registration_month', 'fuel_type', 'brand',
       'unrepaired_damage', 'ad_created', 'num_of_pictures', 'postal_code',
       'last_seen']
```


```python
autos.columns = snakecase_names
```


```python
autos.columns
```




    Index(['date_crawled', 'name', 'seller', 'offer_type', 'price', 'ab_test',
           'vehicle_type', 'registration_year', 'gearbox', 'power_ps', 'model',
           'odometer', 'registration_month', 'fuel_type', 'brand',
           'unrepaired_damage', 'ad_created', 'num_of_pictures', 'postal_code',
           'last_seen'],
          dtype='object')



This is what we did in the previous few cells:
* Accessed our columns using the `columns`  to display an array
* Copied the array to `snakecase_names` and changed the index names into snakecase format
* Reassigned `snakecase_names` to `autos.columns`

The work I did here will make our columns easier to read, and if need be, easier to transform!


```python
autos.describe(include='all')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date_crawled</th>
      <th>name</th>
      <th>seller</th>
      <th>offer_type</th>
      <th>price</th>
      <th>ab_test</th>
      <th>vehicle_type</th>
      <th>registration_year</th>
      <th>gearbox</th>
      <th>power_ps</th>
      <th>model</th>
      <th>odometer</th>
      <th>registration_month</th>
      <th>fuel_type</th>
      <th>brand</th>
      <th>unrepaired_damage</th>
      <th>ad_created</th>
      <th>num_of_pictures</th>
      <th>postal_code</th>
      <th>last_seen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>50000</td>
      <td>50000</td>
      <td>50000</td>
      <td>50000</td>
      <td>50000</td>
      <td>50000</td>
      <td>44905</td>
      <td>50000.000000</td>
      <td>47320</td>
      <td>50000.000000</td>
      <td>47242</td>
      <td>50000</td>
      <td>50000.000000</td>
      <td>45518</td>
      <td>50000</td>
      <td>40171</td>
      <td>50000</td>
      <td>50000.0</td>
      <td>50000.000000</td>
      <td>50000</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>48213</td>
      <td>38754</td>
      <td>2</td>
      <td>2</td>
      <td>2357</td>
      <td>2</td>
      <td>8</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>245</td>
      <td>13</td>
      <td>NaN</td>
      <td>7</td>
      <td>40</td>
      <td>2</td>
      <td>76</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>39481</td>
    </tr>
    <tr>
      <th>top</th>
      <td>2016-03-30 19:48:02</td>
      <td>Ford_Fiesta</td>
      <td>privat</td>
      <td>Angebot</td>
      <td>$0</td>
      <td>test</td>
      <td>limousine</td>
      <td>NaN</td>
      <td>manuell</td>
      <td>NaN</td>
      <td>golf</td>
      <td>150,000km</td>
      <td>NaN</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-04-03 00:00:00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-04-07 06:17:27</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>3</td>
      <td>78</td>
      <td>49999</td>
      <td>49999</td>
      <td>1421</td>
      <td>25756</td>
      <td>12859</td>
      <td>NaN</td>
      <td>36993</td>
      <td>NaN</td>
      <td>4024</td>
      <td>32424</td>
      <td>NaN</td>
      <td>30107</td>
      <td>10687</td>
      <td>35232</td>
      <td>1946</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2005.073280</td>
      <td>NaN</td>
      <td>116.355920</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.723360</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50813.627300</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>std</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>105.712813</td>
      <td>NaN</td>
      <td>209.216627</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.711984</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>25779.747957</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1000.000000</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1067.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1999.000000</td>
      <td>NaN</td>
      <td>70.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>30451.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2003.000000</td>
      <td>NaN</td>
      <td>105.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>49577.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2008.000000</td>
      <td>NaN</td>
      <td>150.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>71540.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9999.000000</td>
      <td>NaN</td>
      <td>17700.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>99998.000000</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



After using the `describe` command, this is what I can determine:
* We can definitely drop both the 'seller' and 'offer_type' columns, since they have both have values that occur 49999 (out of a possible 50000) times.
* We can also drop num_of_pictures there's only one unique value of just 0


```python
# Drop seller, offer_type, and num_of_pictures columns
autos = autos.drop(columns=['seller','offer_type', 'num_of_pictures'])
```

Next in two of the colums, `price` and `odometer` we have some characters present that will be a hindrance to us if we want to perform calculations in the near future. Let's clean them up!


```python
autos['price']
```




    0         $5,000
    1         $8,500
    2         $8,990
    3         $4,350
    4         $1,350
              ...   
    49995    $24,900
    49996     $1,980
    49997    $13,200
    49998    $22,900
    49999     $1,250
    Name: price, Length: 50000, dtype: object




```python
autos['odometer']
```




    0        150,000km
    1        150,000km
    2         70,000km
    3         70,000km
    4        150,000km
               ...    
    49995    100,000km
    49996    150,000km
    49997      5,000km
    49998     40,000km
    49999    150,000km
    Name: odometer, Length: 50000, dtype: object




```python
# Remove non-numeric charcters and convert dtypes for price and odometer columns to numeric values

autos['price'] = autos['price'].str.replace('$', '').str.replace(',','')
autos['odometer'] = autos['odometer'].str.replace('km', '').str.replace(',','')
autos['price'] = autos['price'].astype(int)
autos['odometer'] = autos['odometer'].astype(int)

# Lastly we'll rename 'odometer' to odometer_km so that our audience will know that the units are in km
autos = autos.rename(columns={"odometer": "odometer_km"})

```

Check to see whether our conversion of the two columns ```price``` and `odometer` to a numeric dtype were successful as well as our renaming `odometer` to `odometer_km`


```python
autos['price'].value_counts().sort_index(ascending=False).tail(15)
```




    18       1
    17       3
    15       2
    14       1
    13       2
    12       3
    11       2
    10       7
    9        1
    8        1
    5        2
    3        1
    2        3
    1      156
    0     1421
    Name: price, dtype: int64




```python
autos['odometer_km'].value_counts().sort_index(ascending=False)
```




    150000    32424
    125000     5170
    100000     2169
    90000      1757
    80000      1436
    70000      1230
    60000      1164
    50000      1027
    40000       819
    30000       789
    20000       784
    10000       264
    5000        967
    Name: odometer_km, dtype: int64



Our conversion was successful! 

Next we want to get rid of values in `odometer_km` and `prices` that don't seem to be within the scope of realistic expectations that we would have for used vehicles.


```python
# Remove rows with unrealistic prices
autos = autos[autos['price'].between(1000, 1000000)]
```


```python
autos['price'].describe()
```




    count     38629.000000
    mean       7332.474359
    std       13060.890754
    min        1000.000000
    25%        2200.000000
    50%        4350.000000
    75%        8950.000000
    max      999999.000000
    Name: price, dtype: float64



In the above transformations, I didn't make any changes to the `odometer_km` column, because all the values were seen as necessary and realistic. But I did however, make changes to the `price` column because there were a lot of unrealistic prices for cars that were both too low and too high


```python
(autos[['date_crawled', 'last_seen', 'ad_created']].
     sort_values(by=['ad_created'], ascending=True)
     .tail(10)
       
)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date_crawled</th>
      <th>last_seen</th>
      <th>ad_created</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>38743</th>
      <td>2016-04-07 02:36:24</td>
      <td>2016-04-07 02:36:24</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
    <tr>
      <th>47885</th>
      <td>2016-04-07 00:36:33</td>
      <td>2016-04-07 00:36:33</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
    <tr>
      <th>13976</th>
      <td>2016-04-07 10:36:17</td>
      <td>2016-04-07 10:36:17</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
    <tr>
      <th>4378</th>
      <td>2016-04-07 14:36:55</td>
      <td>2016-04-07 14:36:55</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
    <tr>
      <th>37112</th>
      <td>2016-04-07 07:36:24</td>
      <td>2016-04-07 07:36:24</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
    <tr>
      <th>30532</th>
      <td>2016-04-07 01:36:35</td>
      <td>2016-04-07 01:36:35</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
    <tr>
      <th>24853</th>
      <td>2016-04-07 08:25:34</td>
      <td>2016-04-07 09:06:16</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
    <tr>
      <th>29938</th>
      <td>2016-04-07 11:36:23</td>
      <td>2016-04-07 11:36:23</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
    <tr>
      <th>1138</th>
      <td>2016-04-07 01:36:16</td>
      <td>2016-04-07 01:36:16</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
    <tr>
      <th>47588</th>
      <td>2016-04-07 03:36:24</td>
      <td>2016-04-07 03:36:24</td>
      <td>2016-04-07 00:00:00</td>
    </tr>
  </tbody>
</table>
</div>




```python
# autos['date_crawled'] = autos['date_crawled'].str[:10]
# autos['last_seen'] = autos['last_seen'].str[:10]
# autos['ad_created'] = autos['ad_created'].str[:10]    
```


```python
(autos["ad_created"]
        .str[:10]
        .value_counts(normalize=True, dropna=False)
        .sort_index(ascending=True).tail(37)
        )
```




    2016-03-02    0.000129
    2016-03-03    0.000854
    2016-03-04    0.001527
    2016-03-05    0.023040
    2016-03-06    0.015144
    2016-03-07    0.033809
    2016-03-08    0.032566
    2016-03-09    0.032644
    2016-03-10    0.032980
    2016-03-11    0.033058
    2016-03-12    0.037122
    2016-03-13    0.017655
    2016-03-14    0.034974
    2016-03-15    0.033446
    2016-03-16    0.029641
    2016-03-17    0.030185
    2016-03-18    0.013280
    2016-03-19    0.034068
    2016-03-20    0.038261
    2016-03-21    0.037588
    2016-03-22    0.032307
    2016-03-23    0.031945
    2016-03-24    0.029020
    2016-03-25    0.030676
    2016-03-26    0.033213
    2016-03-27    0.031272
    2016-03-28    0.035388
    2016-03-29    0.033990
    2016-03-30    0.032903
    2016-03-31    0.031557
    2016-04-01    0.034456
    2016-04-02    0.035957
    2016-04-03    0.039452
    2016-04-04    0.037278
    2016-04-05    0.011986
    2016-04-06    0.003365
    2016-04-07    0.001320
    Name: ad_created, dtype: float64



There are 74 unique values in our `ad_created` column. This means that we have a wide variety of dates where our listings are created with the oldest being 9 months older than the more recent months


```python
(autos['date_crawled']
     .str[:10]
     .value_counts(normalize=True, dropna=False)
     .sort_index()
)
```




    2016-03-05    0.025551
    2016-03-06    0.013876
    2016-03-07    0.035129
    2016-03-08    0.032618
    2016-03-09    0.032463
    2016-03-10    0.033317
    2016-03-11    0.032799
    2016-03-12    0.037381
    2016-03-13    0.015998
    2016-03-14    0.036631
    2016-03-15    0.033628
    2016-03-16    0.029071
    2016-03-17    0.030495
    2016-03-18    0.012840
    2016-03-19    0.035129
    2016-03-20    0.038158
    2016-03-21    0.037304
    2016-03-22    0.032514
    2016-03-23    0.032204
    2016-03-24    0.029020
    2016-03-25    0.030521
    2016-03-26    0.033110
    2016-03-27    0.031401
    2016-03-28    0.035362
    2016-03-29    0.033990
    2016-03-30    0.033058
    2016-03-31    0.031401
    2016-04-01    0.034611
    2016-04-02    0.036294
    2016-04-03    0.039142
    2016-04-04    0.036863
    2016-04-05    0.013358
    2016-04-06    0.003262
    2016-04-07    0.001501
    Name: date_crawled, dtype: float64



The `date_crawled` column has consecutive dates from early March to April. It also appears to have a pretty solid correlation with the `ad_created` column for the same date, meaning that the date that the ad is first crawled relates strongly to when the ad is first created.

About half of the listings were accessed by the crawler in the last three days that we have on record for our data. And the difference is about 6-10x the previous rates. So it's strange, but since none of our date columns have any value that goes further than `2016-04-07`, we can probably assume that this discrepancy is possibly due to the crawler not pulling any data beyond that point.


```python
(autos['last_seen']
     .str[:10]
     .value_counts(normalize=True, dropna=False)
     .sort_index()
)
```




    2016-03-05    0.001087
    2016-03-06    0.003572
    2016-03-07    0.004556
    2016-03-08    0.006239
    2016-03-09    0.008905
    2016-03-10    0.009811
    2016-03-11    0.011727
    2016-03-12    0.022185
    2016-03-13    0.008387
    2016-03-14    0.011986
    2016-03-15    0.014989
    2016-03-16    0.015455
    2016-03-17    0.026379
    2016-03-18    0.007378
    2016-03-19    0.014600
    2016-03-20    0.019804
    2016-03-21    0.019674
    2016-03-22    0.020787
    2016-03-23    0.017914
    2016-03-24    0.018535
    2016-03-25    0.017759
    2016-03-26    0.016076
    2016-03-27    0.014083
    2016-03-28    0.019441
    2016-03-29    0.020787
    2016-03-30    0.023454
    2016-03-31    0.022729
    2016-04-01    0.023195
    2016-04-02    0.024904
    2016-04-03    0.024438
    2016-04-04    0.023376
    2016-04-05    0.131119
    2016-04-06    0.234694
    2016-04-07    0.139973
    Name: last_seen, dtype: float64




```python
# Print out our registration years
print(autos['registration_year']
     .value_counts(dropna=False)
     .sort_index()
)

print(autos['registration_year'].describe())
```

    1000    1
    1001    1
    1927    1
    1929    1
    1931    1
           ..
    5911    1
    6200    1
    8888    1
    9000    1
    9999    2
    Name: registration_year, Length: 91, dtype: int64
    count    38629.000000
    mean      2005.678713
    std         86.681928
    min       1000.000000
    25%       2001.000000
    50%       2005.000000
    75%       2009.000000
    max       9999.000000
    Name: registration_year, dtype: float64


Looking at the data in `registration_year` column, we can see that there are quite a few oddities in here.


```python
# Filter out anything that is after the year 2016 and before the 1900s
odd_values = autos[(autos['registration_year'] > 2016) | 
                   (autos['registration_year'] < 1900)].index

# Drop them from our table
autos.drop(odd_values, inplace=True)
```

I decided to created a `|` filter that isolated rows with `registration_year` values `> 2016` or `< 1900`. My reasoning for deciding my filter criteria was based on the fact that there definitely could be some vintage vehicles that were registered in the early decades of the 1900s. As for filtering out values on the opposite end of the spectrum, because our data is only supposed to go up to 2016, I also dropped data after this point as it isn't accurate. There were a lot of rows that contained `2017` as a value, but that would be inaccurate as a car can't be registered **after** it has already been posted/seen on eBay.


```python
# Print out registration_year values to get a feel for the data
print((autos['registration_year']
     .value_counts(normalize=True)
     .sort_values(ascending=False)
))
# Print out a small sample of the data—the first 15 values in descending order
sample = autos['registration_year'].value_counts(normalize=True).sort_values(ascending=False).head(15)
print(sample)
print('\n')
# Sum the sample to get the percentage and convert it to a string to print a statment
print("These 15 rows impact " + str(sample.sum() * 100) + "%" " of our data")
```

    2005    0.074847
    2006    0.071246
    2004    0.070091
    2003    0.066570
    2007    0.060711
              ...   
    1929    0.000027
    1927    0.000027
    1943    0.000027
    1953    0.000027
    1952    0.000027
    Name: registration_year, Length: 77, dtype: float64
    2005    0.074847
    2006    0.071246
    2004    0.070091
    2003    0.066570
    2007    0.060711
    2008    0.059233
    2002    0.057379
    2009    0.055820
    2001    0.055497
    2000    0.053777
    1999    0.046333
    2011    0.043457
    2010    0.042570
    2012    0.035099
    1998    0.034481
    Name: registration_year, dtype: float64
    
    
    These 15 rows impact 82.7111720282727% of our data


With our truncated `registration_year` column, it now stands at 77 rows. I took 15 of the highest recurring `registration_year` values in descending order and added them up. The result that I got after adding them together and multiplying by 100 was `82.7111720282727` This indicates that about 83 percent of the cars in our dataset were registered between the years 1998 to 2012. And the years that have that have the highest registration in order are `2005`, `2006`, and `2004`.


```python
# Check to see the top brands that make up the highest percentage of the brand column
autos['brand'].value_counts(normalize=True)
```




    volkswagen        0.210836
    bmw               0.125346
    mercedes_benz     0.111586
    audi              0.097584
    opel              0.089064
    ford              0.058722
    renault           0.037276
    peugeot           0.027896
    fiat              0.021070
    skoda             0.019055
    seat              0.017281
    smart             0.016609
    toyota            0.014620
    mazda             0.014244
    citroen           0.013894
    nissan            0.013626
    mini              0.010884
    hyundai           0.010750
    sonstige_autos    0.010454
    volvo             0.008976
    kia               0.007686
    porsche           0.007471
    honda             0.007337
    mitsubishi        0.006880
    chevrolet         0.006611
    alfa_romeo        0.006235
    suzuki            0.005724
    dacia             0.003279
    chrysler          0.003171
    jeep              0.002768
    land_rover        0.002634
    jaguar            0.001854
    subaru            0.001720
    daihatsu          0.001693
    saab              0.001371
    daewoo            0.000914
    trabant           0.000860
    rover             0.000726
    lancia            0.000672
    lada              0.000618
    Name: brand, dtype: float64



To determine the top brands in our `brand` column, I decided to choose the six most commonly occuring values aka the 'top brands' in that column. In order, it goes: ```volkswagen, bmw, mercedes_benz, audi, opel, ford```.


```python
autos['brand'].value_counts(normalize=True).index
top_brands = ['volkswagen', 'bmw', 'mercedes_benz', 'audi', 'opel', 'ford']

counter = 0 
for brand in top_brands:
    if counter == 0:
        filtered = pd.concat([pd.DataFrame(), autos[autos['brand'] == brand]], axis=0)
    else:
        filtered = pd.concat([filtered, autos[autos['brand'] == brand]], axis=0)
    counter += 1

# Check out our filtered and combined dataframe    
filtered

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date_crawled</th>
      <th>name</th>
      <th>price</th>
      <th>ab_test</th>
      <th>vehicle_type</th>
      <th>registration_year</th>
      <th>gearbox</th>
      <th>power_ps</th>
      <th>model</th>
      <th>odometer_km</th>
      <th>registration_month</th>
      <th>fuel_type</th>
      <th>brand</th>
      <th>unrepaired_damage</th>
      <th>ad_created</th>
      <th>postal_code</th>
      <th>last_seen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>2016-03-26 18:57:24</td>
      <td>Volkswagen_Golf_1.6_United</td>
      <td>8990</td>
      <td>test</td>
      <td>limousine</td>
      <td>2009</td>
      <td>manuell</td>
      <td>102</td>
      <td>golf</td>
      <td>70000</td>
      <td>7</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-26 00:00:00</td>
      <td>35394</td>
      <td>2016-04-06 20:15:37</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2016-03-16 18:55:19</td>
      <td>Golf_IV_1.9_TDI_90PS</td>
      <td>1990</td>
      <td>control</td>
      <td>limousine</td>
      <td>1998</td>
      <td>manuell</td>
      <td>90</td>
      <td>golf</td>
      <td>150000</td>
      <td>12</td>
      <td>diesel</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-16 00:00:00</td>
      <td>53474</td>
      <td>2016-04-07 03:17:32</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2016-03-29 11:46:22</td>
      <td>Volkswagen_Scirocco_2_G60</td>
      <td>5500</td>
      <td>test</td>
      <td>coupe</td>
      <td>1990</td>
      <td>manuell</td>
      <td>205</td>
      <td>scirocco</td>
      <td>150000</td>
      <td>6</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-29 00:00:00</td>
      <td>74821</td>
      <td>2016-04-05 20:46:26</td>
    </tr>
    <tr>
      <th>38</th>
      <td>2016-03-21 15:51:10</td>
      <td>Volkswagen_Golf_1.4_Special</td>
      <td>2850</td>
      <td>control</td>
      <td>limousine</td>
      <td>2002</td>
      <td>manuell</td>
      <td>75</td>
      <td>golf</td>
      <td>125000</td>
      <td>2</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-21 00:00:00</td>
      <td>63674</td>
      <td>2016-03-28 12:16:06</td>
    </tr>
    <tr>
      <th>40</th>
      <td>2016-03-07 14:50:03</td>
      <td>VW_Golf__4_Cabrio_2.0_GTI_16V___Leder_MFA_Alus...</td>
      <td>3500</td>
      <td>control</td>
      <td>cabrio</td>
      <td>1999</td>
      <td>manuell</td>
      <td>150</td>
      <td>golf</td>
      <td>150000</td>
      <td>1</td>
      <td>benzin</td>
      <td>volkswagen</td>
      <td>nein</td>
      <td>2016-03-07 00:00:00</td>
      <td>6780</td>
      <td>2016-03-12 02:15:52</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49815</th>
      <td>2016-03-08 10:06:22</td>
      <td>SUCHE_TIPPS___Ford_Mustang_Shelby_GT_350_500_K...</td>
      <td>130000</td>
      <td>control</td>
      <td>coupe</td>
      <td>1968</td>
      <td>NaN</td>
      <td>0</td>
      <td>mustang</td>
      <td>50000</td>
      <td>7</td>
      <td>benzin</td>
      <td>ford</td>
      <td>NaN</td>
      <td>2016-03-08 00:00:00</td>
      <td>56070</td>
      <td>2016-03-23 23:15:17</td>
    </tr>
    <tr>
      <th>49837</th>
      <td>2016-03-06 00:40:13</td>
      <td>Ford_Focus_Kombi_1_8</td>
      <td>2000</td>
      <td>control</td>
      <td>kombi</td>
      <td>2001</td>
      <td>manuell</td>
      <td>115</td>
      <td>focus</td>
      <td>150000</td>
      <td>0</td>
      <td>benzin</td>
      <td>ford</td>
      <td>NaN</td>
      <td>2016-03-05 00:00:00</td>
      <td>26441</td>
      <td>2016-03-12 18:46:37</td>
    </tr>
    <tr>
      <th>49871</th>
      <td>2016-03-12 19:00:30</td>
      <td>Ford_Fiesta_1_4_TÜV_bis_2018</td>
      <td>1800</td>
      <td>test</td>
      <td>limousine</td>
      <td>2003</td>
      <td>manuell</td>
      <td>0</td>
      <td>fiesta</td>
      <td>150000</td>
      <td>3</td>
      <td>benzin</td>
      <td>ford</td>
      <td>nein</td>
      <td>2016-03-12 00:00:00</td>
      <td>61169</td>
      <td>2016-03-13 17:09:04</td>
    </tr>
    <tr>
      <th>49922</th>
      <td>2016-03-17 10:36:56</td>
      <td>Ford_Focus_2.0_16V_Titanium</td>
      <td>2888</td>
      <td>test</td>
      <td>limousine</td>
      <td>2004</td>
      <td>manuell</td>
      <td>145</td>
      <td>focus</td>
      <td>150000</td>
      <td>12</td>
      <td>benzin</td>
      <td>ford</td>
      <td>nein</td>
      <td>2016-03-17 00:00:00</td>
      <td>45549</td>
      <td>2016-03-19 09:18:37</td>
    </tr>
    <tr>
      <th>49953</th>
      <td>2016-03-30 17:55:21</td>
      <td>Ford_Mustang</td>
      <td>14750</td>
      <td>control</td>
      <td>coupe</td>
      <td>1967</td>
      <td>automatik</td>
      <td>163</td>
      <td>mustang</td>
      <td>125000</td>
      <td>8</td>
      <td>benzin</td>
      <td>ford</td>
      <td>nein</td>
      <td>2016-03-30 00:00:00</td>
      <td>84478</td>
      <td>2016-03-30 17:55:21</td>
    </tr>
  </tbody>
</table>
<p>25791 rows × 17 columns</p>
</div>



In this cell, we chose our 'top brands' as mentioned earlier and then filter them using a for loop, iterating through our `top_brands` list and use the pandas `pd.concat()` function to stack the filtered dataframes on top of each other.


```python
averages = filtered.groupby('brand')['price'].mean().sort_values(ascending=False)

```

I converted our filtered and stacked dataframe, `filtered` into a `groupby` object, where we group by `brand` and aggregate our data by using `mean()` on our `price` column.

From what I can see here from our 'top brands', Audi vehicles seem to have the highest average price while opel's have the lowest. Volkswagen vehicles are substantially cheaper than Audi, Mercedes Benz and BMW vehicles in our dataset, but they're substantially more abundant than Ford vehicles, which have a slightly cheaper price than Volkswagen's.

I then save `filtered` to a new variable called `averages` as I will do another aggregation concerning the mean of `odometer_km`.


```python
brand_mean_prices = {}

for brand in top_brands:
        brand_only = autos[autos["brand"] == brand]
        mean_price = brand_only['price'].mean()
        brand_mean_prices[brand] = mean_price

sorted(brand_mean_prices.items(), key=lambda x:x[1], reverse=True)
```




    [('audi', 10322.269347287249),
     ('mercedes_benz', 9302.614402697494),
     ('bmw', 9119.20218696398),
     ('volkswagen', 6898.376545570427),
     ('ford', 5786.703432494279),
     ('opel', 4219.954737477368)]



This was another more involved method of finding our mean prices. This way involves assigning the brand names and mean prices to a dictionary while also looping through the top brands like for the creation of our `filtered` dataframe a few cells above.


```python
# Turning our series into a dataframe
averages = pd.DataFrame(averages)

# Renaming the column
averages = averages.rename(columns={'price': 'mean_price'})

# Creating another group by series and adding it as a column to our new dataframe
averages['avg_mileage'] = filtered.groupby('brand')['odometer_km'].mean()
```

To make our data easier to work with and transform, I convereted our `averages` series into a DataFrame. I also renamed the `price` column to `mean_price`.

I also performed a `groupby` operation on our `brand` column once again and aggregated `odometer_km` using the `mean()` function, creating a series. We then assigned the series to our new DataFrame `averages` by creating a new column in `averages` called `avg_mileage`.


```python
averages = averages.loc[:, ['avg_mileage', 'mean_price']].sort_values(by='avg_mileage', ascending=False)
averages['avg_mileage_to_price_ratio'] = (averages['avg_mileage'] /averages['mean_price'])
averages
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>avg_mileage</th>
      <th>mean_price</th>
      <th>avg_mileage_to_price_ratio</th>
    </tr>
    <tr>
      <th>brand</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bmw</th>
      <td>132001.500858</td>
      <td>9119.202187</td>
      <td>14.475115</td>
    </tr>
    <tr>
      <th>mercedes_benz</th>
      <td>130062.620424</td>
      <td>9302.614403</td>
      <td>13.981298</td>
    </tr>
    <tr>
      <th>audi</th>
      <td>127491.049298</td>
      <td>10322.269347</td>
      <td>12.351068</td>
    </tr>
    <tr>
      <th>volkswagen</th>
      <td>125771.829191</td>
      <td>6898.376546</td>
      <td>18.232091</td>
    </tr>
    <tr>
      <th>opel</th>
      <td>123952.926976</td>
      <td>4219.954737</td>
      <td>29.373047</td>
    </tr>
    <tr>
      <th>ford</th>
      <td>119622.425629</td>
      <td>5786.703432</td>
      <td>20.671947</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.scatter(averages['mean_price'], averages['avg_mileage'])
plt.show()
```


    
![png](output_52_0.png)
    


I decided to sort out our values based on the `avg_mileage` column and I added another column called `avg_mileage_to_price_ratio`. Based on my observations, our 'big 3' luxury brands (Audi, Mercedes Benz and BMW) seem to have a slight correlation between `avg_mileage` and `mean_price` as the price seems to be higher as the mileage decreases and vice versa. But that link isn't so strong with the other brands, such as comparing the Ford brand to the Volkswagen brand where Ford has a substantially lower `avg_mileage` value than Volkswagen, but it is also quite less expensive.

And for the `avg_mileage_to_price_ratio` column, in the absence of any other factors or features, from a consumer perspective, a higher number indicates a more economic value for the consumer and while a lower number would probably put it in the range of being more of a luxury purchase. If I have more time, I could potentially use this and other metrics to determine whether any given brand is a luxury brand or not.

## Conclusion

This concludes my observations for this dataset for now, but there are still additional transformations and further analysis that can be done with it. We can still do further cleaning such as converting the date columns to a more uniform format and possibly even translating the German words in our categorical data. For analysis, we can do more in-depth dives into our specific vehicle model types, looking at damaged vs. non-damaged vehicles, and so on.

I will continue to periodically come back to this dataset to reiterate and update with more insights, cleaning up and finding newer more efficient ways to expedite old processes! Thank you for your time!
