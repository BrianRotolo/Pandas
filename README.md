

```python
import pandas as pd
import numpy as np
import json
```


```python
with open('Resources/purchase_data.json') as json_data:
    dict_purchasedata = json.load(json_data)
    #print(dict_purchasedata)
df = pd.DataFrame.from_dict(dict_purchasedata)
df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
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
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
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




```python
#player count
total_players = df["SN"].nunique()
total_players
```




    573




```python
#purchase analysis > total number of unique items
unique_items = df["Item ID"].nunique()
unique_items
```




    183




```python
#purchase analysis > average purchase price
average_price = round(df["Price"].mean(),2)
average_price
```




    2.93




```python
#purchase analysis > total revenue
total_revenue = round(df["Price"].sum(),2)
total_revenue
```




    2286.33




```python
#purchase analysis > total number of purchases
total_purchases = len(df["Price"])
total_purchases
```




    780




```python
df2 = df.drop_duplicates(["SN"])
df2.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
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
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
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




```python
#gender demographics (pecennt/count) of (male/female/other)
male = df2["Gender"].value_counts()["Male"]
female = df2["Gender"].value_counts()["Female"]
total_gender = df2["Gender"].count()
male_percent = round((male/total_gender) * 100,2)
female_percent = round((female/total_gender) * 100,2)
non_gender_specific = total_gender - male - female
non_gender_percent = round((non_gender_specific/total_gender) * 100,2)
print(f"Total: ", total_gender)
print(f"Male Percentage: ",male_percent)
print(f"Female Percentage: ",female_percent)
print(f"Non-Gender Specific Percentage: ",non_gender_percent)
print(f"Total Males: ", male)
print(f"Total Females: ", female)
print(f"Total Non-Gender Specific: ",non_gender_specific)
```

    Total:  573
    Male Percentage:  81.15
    Female Percentage:  17.45
    Non-Gender Specific Percentage:  1.4
    Total Males:  465
    Total Females:  100
    Total Non-Gender Specific:  8



```python
df_fem = df.loc[df["Gender"] == "Female"]
df_fem.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
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
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
    </tr>
    <tr>
      <th>16</th>
      <td>22</td>
      <td>Female</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Sundista85</td>
    </tr>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
    </tr>
    <tr>
      <th>22</th>
      <td>11</td>
      <td>Female</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Deural48</td>
    </tr>
    <tr>
      <th>29</th>
      <td>16</td>
      <td>Female</td>
      <td>45</td>
      <td>Glinting Glass Edge</td>
      <td>2.46</td>
      <td>Phaedai25</td>
    </tr>
  </tbody>
</table>
</div>




```python
#average female price
mean_fem_price = round(df_fem["Price"].mean(),2)
mean_fem_price
```




    2.82




```python
#total female revenue
total_fem_rev = round(df_fem["Price"].sum(),2)
total_fem_rev
```




    382.91




```python
#total female number of purchases
total_fem_purch = len(df_fem["Price"])
total_fem_purch
```




    136




```python
df_male = df.loc[df["Gender"] == "Male"]
df_male.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
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
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
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




```python
#average male price
mean_male_price = round(df_male["Price"].mean(),2)
mean_male_price
```




    2.95




```python
#total male revenue
total_male_rev = round(df_male["Price"].sum(),2)
total_male_rev
```




    1867.68




```python
#total male number of purchases
total_male_purch = len(df_male["Price"])
total_male_purch
```




    633




```python
#normalized totals, ugh
gender_numbers = df.groupby("Gender")["SN"].nunique()
gender_numbers.head()
```




    Gender
    Female                   100
    Male                     465
    Other / Non-Disclosed      8
    Name: SN, dtype: int64




```python
gender_totals = df2.groupby("Gender")["Price"].sum()
gender_totals
```




    Gender
    Female                    288.79
    Male                     1389.72
    Other / Non-Disclosed      27.58
    Name: Price, dtype: float64




```python
normalized_gender = gender_totals/(gender_numbers)
normalized_gender.round(2)
```




    Gender
    Female                   2.89
    Male                     2.99
    Other / Non-Disclosed    3.45
    dtype: float64




```python
gender_percent = gender_numbers/573
gender_percent.round(2)
```




    Gender
    Female                   0.17
    Male                     0.81
    Other / Non-Disclosed    0.01
    Name: SN, dtype: float64




```python
gender_purchase = df.groupby("Gender")["Item Name"]
gender_purchase.count()
```




    Gender
    Female                   136
    Male                     633
    Other / Non-Disclosed     11
    Name: Item Name, dtype: int64




```python
gender_mean = df.groupby("Gender")["Price"].mean()
gender_mean.round(2)
```




    Gender
    Female                   2.82
    Male                     2.95
    Other / Non-Disclosed    3.25
    Name: Price, dtype: float64




```python
#table after figuring out a better way to list gender counts
gender_table = pd.DataFrame({"Purchase Count":gender_purchase, 
                                   "Average Purchase Price":gender_mean,
                                   "Total Purchase Value":gender_totals,
                                   "Normalized Totals":normalized_gender})
gender_table
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>2.815515</td>
      <td>2.887900</td>
      <td>(Female, [Interrogator, Blood Blade of the Que...</td>
      <td>288.79</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2.950521</td>
      <td>2.988645</td>
      <td>(Male, [Bone Crushing Silver Skewer, Stormbrin...</td>
      <td>1389.72</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>3.249091</td>
      <td>3.447500</td>
      <td>(Other / Non-Disclosed, [War-Forged Gold Defle...</td>
      <td>27.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
#bins for ages
bins = [0,10,15,20,25,30,35,40, 45]
ages = ["<10", "10-14","15-19", "20-24", "25-29", "30-34", "35-39", ">=40"]
```


```python
pd.cut(df["Age"], bins, labels=ages)
df["Ages"] = pd.cut(df["Age"], bins, labels= ages)
df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
#purchase count age
age_purchase = df.groupby("Ages")["Item Name"]
age_purchase.count() 
```




    Ages
    <10       32
    10-14     78
    15-19    184
    20-24    305
    25-29     76
    30-34     58
    35-39     44
    >=40       3
    Name: Item Name, dtype: int64




```python
#average purchase age
age_mean = df.groupby("Ages")["Price"].mean()
age_mean.round(2)
```




    Ages
    <10      3.02
    10-14    2.87
    15-19    2.87
    20-24    2.96
    25-29    2.89
    30-34    3.07
    35-39    2.90
    >=40     2.88
    Name: Price, dtype: float64




```python
#total purcahse value age
age_total = df.groupby("Ages")["Price"].sum()
age_total
```




    Ages
    <10       96.62
    10-14    224.15
    15-19    528.74
    20-24    902.61
    25-29    219.82
    30-34    178.26
    35-39    127.49
    >=40       8.64
    Name: Price, dtype: float64




```python
#normailized age
normalized_age = age_total/573
normalized_age.round(2)
```




    Ages
    <10      0.17
    10-14    0.39
    15-19    0.92
    20-24    1.58
    25-29    0.38
    30-34    0.31
    35-39    0.22
    >=40     0.02
    Name: Price, dtype: float64




```python
#age table
age_table = pd.DataFrame({"Purchase Count":age_purchase,
                            "Average Purchase Price":age_mean,
                            "Total Purchase Value": age_total,
                            "Normalized Totals": normalized_age})
age_table

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Ages</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>3.019375</td>
      <td>0.168621</td>
      <td>(&lt;10, [Darkheart, Butcher of the Champion, Woe...</td>
      <td>96.62</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>2.873718</td>
      <td>0.391187</td>
      <td>(10-14, [Phantomlight, Brimstone, Conqueror Ad...</td>
      <td>224.15</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>2.873587</td>
      <td>0.922757</td>
      <td>(15-19, [Sleepwalker, Mercenary Sabre, Alpha, ...</td>
      <td>528.74</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>2.959377</td>
      <td>1.575236</td>
      <td>(20-24, [Stormbringer, Dark Blade of Ending Mi...</td>
      <td>902.61</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>2.892368</td>
      <td>0.383630</td>
      <td>(25-29, [Interrogator, Blood Blade of the Quee...</td>
      <td>219.82</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>3.073448</td>
      <td>0.311099</td>
      <td>(30-34, [Primitive Blade, Expiration, Warscyth...</td>
      <td>178.26</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>2.897500</td>
      <td>0.222496</td>
      <td>(35-39, [Bone Crushing Silver Skewer, Bonecarv...</td>
      <td>127.49</td>
    </tr>
    <tr>
      <th>&gt;=40</th>
      <td>2.880000</td>
      <td>0.015079</td>
      <td>(&gt;=40, [Venom Claymore, Suspension, Despair, F...</td>
      <td>8.64</td>
    </tr>
  </tbody>
</table>
</div>




```python
#set up dataframe for working with top spenders
purch_count = df.groupby("SN").count()["Price"].rename("Purchase Count")
average_purch_price = df.groupby("SN").mean()["Price"].rename("Average Purchase Price")
total_purch_val = df.groupby("SN").sum()["Price"].rename("Total Purchase Value")

```


```python
SN_df = pd.DataFrame({"Purchase Count":purch_count,
                                   "Average Purchase Price": average_purch_price,
                                   "Total Purchase Value": total_purch_val})
SN_df.head() 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.460000</td>
      <td>1</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>2.233333</td>
      <td>3</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>1.933333</td>
      <td>3</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.460000</td>
      <td>1</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.270000</td>
      <td>1</td>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
#big money gamers
big_money = SN_df.sort_values("Total Purchase Value", ascending=False)
big_money.head() 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>3.412000</td>
      <td>5</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>3.390000</td>
      <td>4</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>3.185000</td>
      <td>4</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>4.243333</td>
      <td>3</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>3.860000</td>
      <td>3</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
#set up dataframe for working with top items

item_purch_count = df.groupby(["Item ID", "Item Name"]).count()["Price"].rename("Purchase Count")
item_average_purch_price = df.groupby(["Item ID", "Item Name"]).mean()["Price"].rename("Average Purchase Price")
item_total_purch_val = df.groupby(["Item ID", "Item Name"]).sum()["Price"].rename("Total Purchase Value")

```


```python
item_df = pd.DataFrame({"Purchase Count":item_purch_count,
                                   "Item Price":item_average_purch_price,
                                   "Total Purchase Value":item_total_purch_val,})

item_df.head() 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <th>Splinter</th>
      <td>1.82</td>
      <td>1</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <th>Crucifer</th>
      <td>2.28</td>
      <td>4</td>
      <td>9.12</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Verdict</th>
      <td>3.40</td>
      <td>1</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <th>Phantomlight</th>
      <td>1.79</td>
      <td>1</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Bloodlord's Fetish</th>
      <td>2.28</td>
      <td>1</td>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
#popular items
popular_items = item_df.sort_values("Purchase Count", ascending=False)
popular_items.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>2.35</td>
      <td>11</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>2.23</td>
      <td>11</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>2.07</td>
      <td>9</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>1.24</td>
      <td>9</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>1.49</td>
      <td>9</td>
      <td>13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
#profitable items
profit_items = item_df.sort_values("Total Purchase Value", ascending=False)
profit_items.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>4.14</td>
      <td>9</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>4.25</td>
      <td>7</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>4.95</td>
      <td>6</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>4.87</td>
      <td>6</td>
      <td>29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>3.61</td>
      <td>8</td>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Observable trends based on data:
# 1. The players are mostly male.
# 2. Players age 15 - 24 are spend more money in-game than all other age brackets combined.
# 3. Players age 30 - 34 are most likely to spend money on more expensive items.
```
# Heroes-of-Pymoli
