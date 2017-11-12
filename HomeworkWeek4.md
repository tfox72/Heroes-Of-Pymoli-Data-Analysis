



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
userinput = input('Please enter which file you want to read, purchase_data.json or purchase_data2.json.')
myfile = userinput
```

    Please enter which file you want to read, purchase_data.json or purchase data2.json.purchase_data2.json
    


```python
myfile
```




    'purchase_data2.json'




```python
data1 = pd.read_json(myfile)
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
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
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
      <td>74</td>
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
      <td>63</td>
      <td>2.92</td>
      <td>78</td>
      <td>228.1</td>
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
gender2= gender2[['Percent of Players','Gender Count']]
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
      <th>Percent of Players</th>
      <th>Gender Count</th>
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
      <td>81.08</td>
      <td>60</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.57</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>1.35</td>
      <td>1</td>
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
      <td>64</td>
      <td>2.88</td>
      <td>184.60</td>
      <td>2.88</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>13</td>
      <td>3.18</td>
      <td>41.38</td>
      <td>3.18</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>1</td>
      <td>2.12</td>
      <td>2.12</td>
      <td>2.12</td>
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
      <td>6.76</td>
      <td>5</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>4.05</td>
      <td>3</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>14.86</td>
      <td>11</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>45.95</td>
      <td>34</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>10.81</td>
      <td>8</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>8.11</td>
      <td>6</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>8.11</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Over 40</th>
      <td>1.35</td>
      <td>1</td>
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
TopSpend1 = TopSpend1[['Purchase Count', 'Average Purchase Price', 'Total Purchase Value']]

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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
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
      <th>[Sundaky74]</th>
      <td>2</td>
      <td>3.70</td>
      <td>7.41</td>
    </tr>
    <tr>
      <th>[Aidaira26]</th>
      <td>2</td>
      <td>2.56</td>
      <td>5.13</td>
    </tr>
    <tr>
      <th>[Eusty71]</th>
      <td>1</td>
      <td>4.81</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>[Chanirra64]</th>
      <td>1</td>
      <td>4.78</td>
      <td>4.78</td>
    </tr>
    <tr>
      <th>[Alarap40]</th>
      <td>1</td>
      <td>4.71</td>
      <td>4.71</td>
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
      <th>[94]</th>
      <td>[Mourning Blade]</td>
      <td>3</td>
      <td>[3.64]</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>[90]</th>
      <td>[Betrayer]</td>
      <td>2</td>
      <td>[4.12]</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>[111]</th>
      <td>[Misery's End]</td>
      <td>2</td>
      <td>[1.79]</td>
      <td>3.58</td>
    </tr>
    <tr>
      <th>[64]</th>
      <td>[Fusion Pummel]</td>
      <td>2</td>
      <td>[2.42]</td>
      <td>4.84</td>
    </tr>
    <tr>
      <th>[154]</th>
      <td>[Feral Katana]</td>
      <td>2</td>
      <td>[4.11]</td>
      <td>8.22</td>
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
      <th>[94]</th>
      <td>[Mourning Blade]</td>
      <td>3</td>
      <td>[3.64]</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>[117]</th>
      <td>[Heartstriker, Legacy of the Light]</td>
      <td>2</td>
      <td>[4.71]</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>[93]</th>
      <td>[Apocalyptic Battlescythe]</td>
      <td>2</td>
      <td>[4.49]</td>
      <td>8.98</td>
    </tr>
    <tr>
      <th>[90]</th>
      <td>[Betrayer]</td>
      <td>2</td>
      <td>[4.12]</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>[154]</th>
      <td>[Feral Katana]</td>
      <td>2</td>
      <td>[4.11]</td>
      <td>8.22</td>
    </tr>
  </tbody>
</table>
</div>


