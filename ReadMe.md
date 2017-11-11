



**Player Count**

* Total Number of Players

**Purchasing Analysis (Total)**

* Number of Unique Items
* Average Purchase Price
* Total Number of Purchases
* Total Revenue

**Gender Demographics**

* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed

**Purchasing Analysis (Gender)** 

* The below each broken by gender
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals

**Age Demographics**

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.) 
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals

**Top Spenders**

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value

**Most Popular Items**

* Identify the 5 most popular items by purchase count, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

**Most Profitable Items**

* Identify the 5 most profitable items by total purchase value, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

As final considerations:

* Your script must work for both data-sets given.
* You must use the Pandas Library and the Jupyter Notebook.
* You must submit a link to your Jupyter Notebook with the viewable Data Frames. 
* You must include an exported markdown version of your Notebook called  `README.md` in your GitHub repository.  
* You must include a written description of three observable trends based on the data. 
* See [Example Solution](HeroesOfPymoli/HeroesOfPymoli_Example.pdf) for a reference on expected format. 




```python
import pandas as pd
import json as js
```


```python
data1 = pd.read_json('purchase_data.json')
```


```python
data2 = pd.read_json('purchase_data2.json')
```


```python
data1.head()
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
totalplayers= {'Total Players':[len(data1['SN'].value_counts())]}
totalplayers1 = pd.DataFrame(totalplayers)
totalplayers1
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Number of Unique Items
UniqueItems = len(data1['Item Name'].value_counts())
#Average Purchase Price
AvPurchPrice = round(data1['Price'].mean(),2)
#Total Purchase Value
TotalPurchases = round(data1['Price'].sum(),2)

```


```python
#Purchasing Analysis (Total)
PurchasingAnalysis= {'Unique Items':[UniqueItems],'Average Price':[AvPurchPrice],'Number of Purchases': [len(data1)],'Total Purchases':[TotalPurchases]}
PurchasingAnalysis1 =pd.DataFrame(PurchasingAnalysis)
PurchasingAnalysis1 = PurchasingAnalysis1[['Unique Items','Average Price','Number of Purchases','Total Purchases']]
PurchasingAnalysis1
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
      <th>Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Purchases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>179</td>
      <td>2.93</td>
      <td>780</td>
      <td>2286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Gender Demographics

# Total Count
total_count = len(data1["SN"].unique())

#Percentage and Count of Male Players
#Male = data1.loc[data1['Gender'] =='Male',:]
Male1= data1.groupby(['Gender']).get_group(('Male'))
Male2= len(Male1['SN'].unique())
MalePercent= round((Male2/total_count)*100,2)

#Percentage and Count of Female Players
Female1= data1.groupby(['Gender']).get_group(('Female'))
Female2= len(Female1['SN'].unique())
FemalePercent= round((Female2/total_count)*100,2)

#Percentage and Count of Other / Non-Disclosed Players
Other1= data1.groupby(['Gender']).get_group(('Other / Non-Disclosed'))
Other2= len(Other1['SN'].unique())
OtherPercent= round((Other2/total_count)*100,2)

#Make it into a Gender DataFrame
gender1 = {'Percent of Players':[MalePercent,FemalePercent,OtherPercent],'Gender':["Male",'Female','Other'],'Gender Count':[Male2,Female2,Other2]}
gender2 =  pd.DataFrame(gender1)
gender2= gender2.set_index('Gender')
gender2
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
      <th>Gender Count</th>
      <th>Percent of Players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>465</td>
      <td>81.15</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>8</td>
      <td>1.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender)

#Purchase Count
MalePurchaseCount = len(Male1)
FemalePurchaseCount = len(Female1)
OtherPurchaseCount = len(Other1)

#Average Purchase Price
MaleAvgPrice =round((Male1["Price"].sum())/len(Male1["Price"]),2)
FemaleAvgPrice= round((Female1["Price"].sum())/len(Female1["Price"]),2)
OtherAvgPrice= round((Other1["Price"].sum())/len(Other1["Price"]),2)


#Total Purchase Value
MaleTotalPurchase = round(Male1['Price'].sum(),2)
FemaleTotalPurchase = round(Female1['Price'].sum(),2)
OtherTotalPurchase = round(Other1['Price'].sum(),2)

# Normalised Totals
# male/female/Other
NormMale = round((MaleTotalPurchase/MalePurchaseCount), 2)
NormFemale = round((FemaleTotalPurchase/FemalePurchaseCount), 2)
NormOther = round((OtherTotalPurchase/OtherPurchaseCount), 2)

PurchByGender = {"Purchase Count":[MalePurchaseCount,FemalePurchaseCount,OtherPurchaseCount],
                    "Gender":["Male","Female","Other"],
                    "Average Purchase Price":[MaleAvgPrice,FemaleAvgPrice,OtherAvgPrice],
                    "Total Purchase Value":[MaleTotalPurchase,FemaleTotalPurchase,OtherTotalPurchase],
                "Normalized Totals":[NormMale,NormFemale,NormOther]}
PurchByGender1 = pd.DataFrame(PurchByGender)
PurchByGender1 = PurchByGender1.set_index('Gender')
PurchByGender1= PurchByGender1[['Purchase Count','Average Purchase Price','Total Purchase Value','Normalized Totals']]
PurchByGender1

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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
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
      <th>Male</th>
      <td>633</td>
      <td>2.95</td>
      <td>1867.68</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>2.82</td>
      <td>382.91</td>
      <td>2.82</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>11</td>
      <td>3.25</td>
      <td>35.74</td>
      <td>3.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Age Demographics
MaxAge = data1['Age'].max()
#print(MaxAge)
#bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
bins = [0,10,14,19,24,29,34,39,46]
Agelabels = ["Under 10","10-14","15-19","20-24","25-29","30-34","35-39","Over 40"]
data1['Age Summary'] = pd.cut(data1['Age'],bins,labels= Agelabels)

#Purchase Count
Bin1 = data1.groupby(['Age Summary']).get_group(('Under 10'))
pc1 = len(Bin1['SN'].unique())
PerBin1 = (pc1/total_count)*100

Bin2 = data1.groupby(['Age Summary']).get_group(('10-14'))
pc2 = len(Bin2['SN'].unique())
PerBin2 = (pc2/total_count)*100

Bin3 = data1.groupby(['Age Summary']).get_group(('15-19'))
pc3 = len(Bin3['SN'].unique())
PerBin3 = (pc3/total_count)*100

Bin4 = data1.groupby(['Age Summary']).get_group(('20-24'))
pc4 = len(Bin4['SN'].unique())
PerBin4 = (pc4/total_count)*100

Bin5 = data1.groupby(['Age Summary']).get_group(('25-29'))
pc5 = len(Bin5['SN'].unique())
PerBin5 = (pc5/total_count)*100

Bin6 = data1.groupby(['Age Summary']).get_group(('30-34'))
pc6 = len(Bin6['SN'].unique())
PerBin6 = (pc6/total_count)*100

Bin7 = data1.groupby(['Age Summary']).get_group(('35-39'))
pc7 = len(Bin7['SN'].unique())
PerBin7 = (pc7/total_count)*100

Bin8 = data1.groupby(['Age Summary']).get_group(('Over 40'))
pc8 = len(Bin8['SN'].unique())
PerBin8 = (pc8/total_count)*100


PlayerBinsCount=[pc1,pc2,pc3,pc4,pc5,pc6,pc7,pc8]
PercentBins= [PerBin1,PerBin2,PerBin3,PerBin4,PerBin5,PerBin6,PerBin7,PerBin8]
PercentBins= [round(x,2) for x in PercentBins]

AgeDem = {"Age Summary":Agelabels,"Total Player Count":PlayerBinsCount,"Percentage Of Players":PercentBins}
AgeDem1 = pd.DataFrame(AgeDem)
AgeDem1 = AgeDem1.set_index('Age Summary')
AgeDem1

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
      <th>Percentage Of Players</th>
      <th>Total Player Count</th>
    </tr>
    <tr>
      <th>Age Summary</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Under 10</th>
      <td>3.84</td>
      <td>22</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>3.49</td>
      <td>20</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>45.20</td>
      <td>259</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>15.18</td>
      <td>87</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>8.20</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>4.71</td>
      <td>27</td>
    </tr>
    <tr>
      <th>Over 40</th>
      <td>1.92</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Spenders

#SN
SN = data1.groupby(data1["SN"])
ScreenName = SN["SN"].unique()

#Purchase Count
SNCount = SN['Age'].count()

#Average Purchase Price
SNAverage = round(SN['Price'].mean(),2)

#Total Purchase Value
SNTotal = SN['Price'].sum()


TopSpend = {"SN":ScreenName,"Purchase Count":SNCount,
                 "Average Purchase Price":SNAverage,"Total Purchase Value":SNTotal}
TopSpend1= pd.DataFrame(TopSpend)
TopSpend1= TopSpend1.set_index('SN')
TopSpend1 = TopSpend1.sort_values("Total Purchase Value",ascending=False)


TopSpend1.iloc[:5]

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
      <th>[Undirrala66]</th>
      <td>3.41</td>
      <td>5</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>[Saedue76]</th>
      <td>3.39</td>
      <td>4</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>[Mindimnya67]</th>
      <td>3.18</td>
      <td>4</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>[Haellysu29]</th>
      <td>4.24</td>
      <td>3</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>[Eoda93]</th>
      <td>3.86</td>
      <td>3</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Popular Items

#Identify the 5 most popular items by purchase count, then list (in a table):


#Item ID
ItemId = data1.groupby(data1['Item ID'])
Items = ItemId['Item ID'].unique()
#Item Name

ItemName = ItemId["Item Name"].unique()

#Purchase Count
ItemPurCount = ItemId['Age'].count()

#Item Price
ItemPrice= ItemId['Price'].unique()


#Total Purchase Value
ItemTotalPurchase = ItemId['Price'].sum()

ItemTable = {'Item ID':Items,'Item Name':ItemName,'Item Price':ItemPrice,'Item Count':ItemPurCount,'Total Purchase':ItemTotalPurchase}
ItemTable1 = pd.DataFrame(ItemTable)
ItemTable1 = ItemTable1.set_index('Item ID')
ItemTable1= ItemTable1.sort_values('Item Count', ascending=False)
ItemTable1 = ItemTable1[['Item Name','Item Count','Item Price','Total Purchase']]
ItemTable1.iloc[:5]
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
      <th>Item Name</th>
      <th>Item Count</th>
      <th>Item Price</th>
      <th>Total Purchase</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>[39]</th>
      <td>[Betrayal, Whisper of Grieving Widows]</td>
      <td>11</td>
      <td>[2.35]</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>[84]</th>
      <td>[Arcane Gem]</td>
      <td>11</td>
      <td>[2.23]</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>[31]</th>
      <td>[Trickster]</td>
      <td>9</td>
      <td>[2.07]</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>[175]</th>
      <td>[Woeful Adamantite Claymore]</td>
      <td>9</td>
      <td>[1.24]</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>[13]</th>
      <td>[Serenity]</td>
      <td>9</td>
      <td>[1.49]</td>
      <td>13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Profitable Items
#Item ID
#Item Name
#Purchase Count
#Item Price
#Total Purchase Value

MostProfit= ItemTable1.sort_values('Total Purchase', ascending=False)
MostProfit[:5]


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
      <th>Item Name</th>
      <th>Item Count</th>
      <th>Item Price</th>
      <th>Total Purchase</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>[34]</th>
      <td>[Retribution Axe]</td>
      <td>9</td>
      <td>[4.14]</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>[115]</th>
      <td>[Spectral Diamond Doomblade]</td>
      <td>7</td>
      <td>[4.25]</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>[32]</th>
      <td>[Orenmir]</td>
      <td>6</td>
      <td>[4.95]</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>[103]</th>
      <td>[Singed Scalpel]</td>
      <td>6</td>
      <td>[4.87]</td>
      <td>29.22</td>
    </tr>
    <tr>
      <th>[107]</th>
      <td>[Splitter, Foe Of Subtlety]</td>
      <td>8</td>
      <td>[3.61]</td>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```


```python

```
