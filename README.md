# Heroes of Pymoli

![1743780586551](image/ReadMe/1743780586551.jpg)

## 1. Overview of Project

## a. Objective

The objective of this project is to emulate the tasks of a Lead Analyst on an independent gaming company.

The data provided contains demographic and purchasing information about the fictional game **Heroes of Pymoli**. Like many others in its genre, the game is free-to-play, but players are encouraged to purchase optional items that enhance their playing experience.

A Data Analytics report has to be created to break down the game's purchasing data into meaningful insights.

Final report should include each of the following:

#### i .Player Count

* Total Number of Players

#### ii. Purchasing Analysis (Total)

* Number of Unique Items
* Average Purchase Price
* Total Number of Purchases
* Total Revenue

#### iii. Gender Demographics

* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed

#### iv. Purchasing Analysis (Gender)

The below each broken by gender

* Purchase Count
* Average Purchase Price
* Total Purchase Value
* Normalized Totals

#### v. Purchasing Analysis (Age)

The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)

* Purchase Count
* Average Purchase Price
* Total Purchase Value
* Normalized Totals

#### vi. Top Spenders

Identify the the top 5 spenders in the game by total purchase value, then list (in a table):

* SN
* Purchase Count
* Average Purchase Price
* Total Purchase Value

#### vii. Most Popular Items

Identify the 5 most popular items by purchase count, then list (in a table):

* Item ID
* Item Name
* Purchase Count
* Item Price
* Total Purchase Value

#### viii. Most Profitable Items

Identify the 5 most profitable items by total purchase value, then list (in a table):

* Item ID
* Item Name
* Purchase Count
* Item Price
* Total Purchase Value

## 2. Data Source

A JSON file was provided with demographic and purchasing information about Heroes of Pymoli video game.

#### a. Number of Records

779

#### b. Columns

* Age
* Gender
* Item ID
* Item Name
* Item Price
* SN (Screen Name)

## 3. Coding

### a. Import Libraries and Data Source Reading

Pandas and Numpy libraries are imported and a dataframe named **_heroes_df_** is created retrieving the data from the JSON file.

```python
import pandas as pd
import numpy as np
```

```python
json_path = ('purchase_data.json')
heroes_df = pd.read_json(json_path, orient='records')
heroes_df.head()
```

<div>
<p><b>Original DataFrame (First 5 Rows)</b></p>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>

### b. Total Players Dataframe

To obtain the total number of players, a dataframe named **_tot_plyr_df_** is created by following below steps:

1. Filter **_heroes_df_** dataframe requesting the number of unique values present in **SN** column.
2. The number of unique values is stored in a dictionary.
3. Dataframe **_tot_plyr_df_** is created from the dictionary.

```python
#Total Players
total_players = heroes_df["SN"].nunique()
tot_players_dict={"Total Players":[total_players]}
tot_plyr_df = pd.DataFrame.from_dict(tot_players_dict, orient='columns')
tot_plyr_df
```

<div>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>

### c. Purchasing Analysis (Total) Dataframe

To obtain the purchasing analysis information, the first step is to calculate all the elements required using **_heroes_df_** dataframe as source table:

* **Number of Unique Items**:
  Calculated as the number of unique values in the **Item ID** column from **_heroes_df_** dataframe.

```python
#Purchasing Analysis (Total)
##Number of Unique Items
nbr_unique_items = heroes_df["Item ID"].nunique() 
```

* **Average Purchase Price**:
  Calculated as the mean of all values in **Price** column from **_heroes_df_** dataframe.

```python
##Average Purchase Price
avg_purch_price = heroes_df["Price"].mean()
```

* **Total Number of Purchases**:
  Calculated as the total number of records in **_heroes_df_** dataframe.

```python
##Total Number of Purchases
total_nbr_purch = len(heroes_df.index)
```

* **Total Revenue**:
  Calculated as the sum of all values in **Price** column from **_heroes_df_** dataframe.

```python
##Total Revenue
total_revenue = heroes_df["Price"].sum()
```

Once all the calculations are stored in their respective variables, a dataframe named **_purch_tot_df_** is created from a dictionary that includes all the variables with their respective column name.

```python
purch_tot_df = pd.DataFrame.from_dict({"Number of unique items":[nbr_unique_items],"Average Price":[avg_purch_price],"Number of Purchases":[total_nbr_purch],"Total Revenue":[total_revenue]}, orient='columns')
```

Finally, currency format is applied for **Total Revenue** and **Average Price** values and dataframe is displayed.

```python
purch_tot_df["Total Revenue"] = purch_tot_df["Total Revenue"].map("$ {:,.2f}".format)
purch_tot_df["Average Price"] = purch_tot_df["Average Price"].map("$ {:,.2f}".format)
purch_tot_df
```

<div>
<p><b> Purchasing Analysis (Total) </b></p>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Number of unique items</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>$ 2.93</td>
      <td>780</td>
      <td>183</td>
      <td>$ 2,286.33</td>
    </tr>
  </tbody>
</table>
</div>

### d. Gender Demographics Dataframe

To obtain the demographics information classified by gender, first a dataframe is created filtering **_heroes_df_** dataframe by dropping duplicates from **SN** column, and then grouping the remaining records by **Gender** column:

```python
#Gender Demographics
##Percentage and Count of Players by Gender
heroes_gender_df = pd.DataFrame(heroes_df.drop_duplicates(["SN"]))
gender_demo_grp = heroes_gender_df.groupby(['Gender'])
```

Once the records have been grouped by gender, next step is to create **_gender_df_** dataframe calculating the **Percentage** and **Count** for each gender, and apply percent format to **Percentage** column.

```python
gender_df = pd.DataFrame({"Total Count":gender_demo_grp["Gender"].count(),"Percentage of players":gender_demo_grp["Gender"].count()/total_players*100})
gender_df["Percentage of players"] = gender_df["Percentage of players"].map("{:.2f}%".format)
gender_df.head()
```

<div>
<p><b> Players Percentage and Count by Gender </b></p>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
     <th>Gender</th>
      <th>Percentage of players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>17.45%</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>81.15%</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.40%</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>

### e. Purchasing Analysis by Gender Dataframe

To obtain the purchasing information classified by gender, first a dataframe is created grouping the records from **_heroes_df_** dataframe by **Gender** column:

```python
#Purchasing Analysis (Gender)
##The below each broken by gender:
###Purchase Count
###Average Purchase Price
###Total Purchase Value
###Normalized Totals
purch_df = pd.DataFrame(heroes_df)
gender_purch = purch_df.groupby(['Gender'])
```

Then, a new dataframe named **_gen_purch_df_** is populated with the required columns calculated and formatted as expected:

* Purchase Count
* Average Purchase Price
* Total Purchase Value
* Normalized Totals

```python
gen_purch_df = pd.DataFrame({"Purchase Count":gender_purch["Price"].count(), "Average Purchase Price":gender_purch["Price"].mean(),"Total Purchase Value":gender_purch["Price"].sum(), "Normalized Totals":gender_purch["Price"].sum()/gender_df["Total Count"]})
gen_purch_df["Average Purchase Price"] = gen_purch_df["Average Purchase Price"].map("${:.2f}".format)
gen_purch_df["Total Purchase Value"] = gen_purch_df["Total Purchase Value"].map("${:,.2f}".format)
gen_purch_df["Normalized Totals"] = gen_purch_df["Normalized Totals"].map("${:,.2f}".format)
gen_purch_df.head()
```

<div>
 <p><b>Purchasing Analysis by Genre</b></p>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Gender</th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>$2.82</td>
      <td>$3.83</td>
      <td>136</td>
      <td>$382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>$2.95</td>
      <td>$4.02</td>
      <td>633</td>
      <td>$1,867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>$3.25</td>
      <td>$4.47</td>
      <td>11</td>
      <td>$35.74</td>
    </tr>
  </tbody>
</table>
</div>

### f. Purchasing Analysis by Age Dataframe

For the Purchasing Analysis by Age Dataframe is required to create bins to group all the players by their specific age range. According to criteria applied, the players were divided in the following age range bins:

* Less than 10
* 10-13
* 14-17
* 18-21
* 22-25
* 26-29
* 30-33
* 34-37
* 38-40
* Greater than 40

```python
age_df = pd.DataFrame(heroes_df)
group_names = ['<10', '10-13', '14-17', '18-21', '22-25', '26-29', '30-33', '34-37', '38-40', '>40']
bins = [0, 9, 13, 17, 21, 25, 29, 33, 37, 40, 80]
age_demo_grp = age_df.groupby(pd.cut(age_df["Age"], bins, labels=group_names))
```

Next step is to create **_age_demo_df_** dataframe and include required columns with their respective calculation and formatting:

* Purchase Count
* Average Purchase Price
* Total Purchase Value
* Normalized Totals

```python
age_demo_df = pd.DataFrame({"Purchase Count":age_demo_grp["Price"].count(), "Average Purchase Price":age_demo_grp["Price"].mean(),"Total Purchase Value":age_demo_grp["Price"].sum(),"Normalized Totals":age_demo_grp["Price"].sum()/age_demo_grp["SN"].nunique()})
age_demo_df["Average Purchase Price"] = age_demo_df["Average Purchase Price"].map("${:.2f}".format)
age_demo_df["Total Purchase Value"] = age_demo_df["Total Purchase Value"].map("${:,.2f}".format)
age_demo_df["Normalized Totals"] = age_demo_df["Normalized Totals"].map("${:,.2f}".format)
age_demo_df
```

<div>
 <p><b>Purchasing Analysis by Age</b></p>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Age</th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th><10</th>
      <td>$2.98</td>
      <td>$4.39</td>
      <td>28</td>
      <td>$83.46</td>
    </tr>
    <tr>
      <th>10-13</th>
      <td>$2.85</td>
      <td>$4.13</td>
      <td>29</td>
      <td>$82.65</td>
    </tr>
    <tr>
      <th>14-17</th>
      <td>$2.87</td>
      <td>$3.81</td>
      <td>93</td>
      <td>$266.48</td>
    </tr>
    <tr>
      <th>18-21</th>
      <td>$2.87</td>
      <td>$3.84</td>
      <td>187</td>
      <td>$537.29</td>
    </tr>
    <tr>
      <th>22-25</th>
      <td>$2.99</td>
      <td>$3.91</td>
      <td>262</td>
      <td>$782.24</td>
    </tr>
    <tr>
      <th>26-29</th>
      <td>$2.82</td>
      <td>$4.20</td>
      <td>58</td>
      <td>$163.81</td>
    </tr>
    <tr>
      <th>30-33</th>
      <td>$3.09</td>
      <td>$4.22</td>
      <td>56</td>
      <td>$172.93</td>
    </tr>
    <tr>
      <th>34-37</th>
      <td>$2.85</td>
      <td>$4.27</td>
      <td>36</td>
      <td>$102.59</td>
    </tr>
    <tr>
      <th>38-40</th>
      <td>$3.08</td>
      <td>$5.07</td>
      <td>28</td>
      <td>$86.24</td>
    </tr>
    <tr>
      <th>>40</th>
      <td>$2.88</td>
      <td>$2.88</td>
      <td>3</td>
      <td>$8.64</td>
    </tr>
  </tbody>
</table>
</div>

### g. Top Spenders Dataframe

To identify the Top Spenders of the game, **_heroes_df_** dataframe is grouped by **SN** column:

```python
#Top Spenders
spenders_df = pd.DataFrame(heroes_df)
top_spnd_grp = spenders_df.groupby(['SN'])
```

Then, new columns are created and formatted for the following calculations:

* Purchase Count
* Average Purchase Price
* Total Purchase Value

```python
top_spnd_df = pd.DataFrame({"Purchase Count":top_spnd_grp["Price"].count(), "Average Purchase Price":top_spnd_grp["Price"].mean(),"Total Purchase Value":top_spnd_grp["Price"].sum()})
top_spnd_df = top_spnd_df.sort_values("Total Purchase Value", ascending=False)
top_spnd_df["Average Purchase Price"] = top_spnd_df["Average Purchase Price"].map("${:.2f}".format)
top_spnd_df["Total Purchase Value"] = top_spnd_df["Total Purchase Value"].map("${:,.2f}".format)
top_spnd_df.head()
```

<div>
<p><b>Top 5 Spenders</b></p>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>SN</th>
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>$3.41</td>
      <td>5</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>$3.39</td>
      <td>4</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>$3.18</td>
      <td>4</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>$4.24</td>
      <td>3</td>
      <td>$12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>$3.86</td>
      <td>3</td>
      <td>$11.58</td>
    </tr>
  </tbody>
</table>
</div>

### h. Most Popular Items DataFrame

To obtain the most popular items is required to group the records from **_heroes_df_** dataframe by **Item ID**, **Item Name** columns, create **_popitems_df_** dataframe including all required columns (with their proper calculation and formatting), and sort dataframe by **Purchase Count** column.

For this dataframe, following columns are required:

* Item ID
* Item Name
* Purchase Count
* Item Price
* Total Purchase Value

```python
#Most Popular Items
popit_df = pd.DataFrame(heroes_df)
popitems_grp = popit_df.groupby(['Item ID','Item Name'])
popitems_df = pd.DataFrame({"Purchase Count":popitems_grp["Price"].count(), "Item Price":popitems_grp["Price"].mean(),"Total Purchase Value":popitems_grp["Price"].sum()})
popitems_df = popitems_df.sort_values("Purchase Count", ascending=False)
popitems_df["Item Price"] = popitems_df["Item Price"].map("${:.2f}".format)
popitems_df["Total Purchase Value"] = popitems_df["Total Purchase Value"].map("${:,.2f}".format)
popitems_df.head()
```

<div>
<p><b>Most Popular Items</b></p>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>$2.35</td>
      <td>11</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>$2.23</td>
      <td>11</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>$2.07</td>
      <td>9</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>$1.24</td>
      <td>9</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>$1.49</td>
      <td>9</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>

### i. Most Profitable Items DataFrame

To obtain the most popular items is required to group the records from **_heroes_df_** dataframe by **Item ID**, **Item Name** columns, create **_popitems_df_** dataframe including all required columns (with their proper calculation and formatting), and sort dataframe by **Total Purchase Value** column.

For this dataframe, following columns are required:

* Item ID
* Item Name
* Purchase Count
* Item Price
* Total Purchase Value

```python
#Most Profitable Items
profit_df = pd.DataFrame(heroes_df)
profit_grp = profit_df.groupby(['Item ID','Item Name'])
profit_df = pd.DataFrame({"Purchase Count":profit_grp["Price"].count(), "Item Price":profit_grp["Price"].mean(),"Total Purchase Value":profit_grp["Price"].sum()})
profit_df = profit_df.sort_values("Total Purchase Value", ascending=False)
profit_df["Item Price"] = profit_df["Item Price"].map("${:.2f}".format)
profit_df["Total Purchase Value"] = profit_df["Total Purchase Value"].map("${:,.2f}".format)
profit_df.head()
```

<div>
<p><b>Most Profitable Items</b></p>
<table class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>$4.14</td>
      <td>9</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>$4.25</td>
      <td>7</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>$4.95</td>
      <td>6</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>$4.87</td>
      <td>6</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>$3.61</td>
      <td>8</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>

## 4. Data Analysis

Once all the information is collected and organized in dataframes, a data analysis is conducted to identify trends and patterns present in the provided data. Purchase analysis report built in Power BI.
![Screenshot 2025-04-04 162731](https://github.com/user-attachments/assets/21fc1552-e8ef-4f50-8e1c-f35b5681f600)


### a. Data Findings

* No one has spent more than $20.00 in the game.
* Most purchases are made by men from 18 to 25 years old.
* Most popular items prices are below the average item price.
