# Ex02-Outlier
### AIM:
You are given bhp.csv which contains property prices in the city of banglore, India. You need to examine price_per_sqft column and do following,

(1) Remove outliers using IQR

(2) After removing outliers in step 1, you get a new dataframe.

(3) use zscore of 3 to remove outliers. This is quite similar to IQR and you will get exact same result

(4) for the data set height_weight.csv find the following

(i) Using IQR detect weight outliers and print them

(ii) Using IQR, detect height outliers and print them
### ALGORITHM:
STEP 1:
Read the given data

STEP 2:
Get the information about the data

STEP 3:
Detect the outlier using IQR method and Zscore.

step 4:
Remove the outliers.

STEP 5:
Plot the datas using boxplot.
### PROCEDURE:
DEVELOPED BY : BEJIN.B REG.NO : 212222230021

You are given bhp.csv which contains property prices in the city of banglore, India. You need to examine price_per_sqft column and do following,
(1) Remove outliers using IQR
(2) After removing outliers in step 1, you get a new dataframe.
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns

data=pd.read_csv("/content/bhp.csv")
df=pd.DataFrame(data)

sns.boxplot(data=df)
sns.scatterplot(data=df)

q1=df.quantile(0.25)
q2=df.quantile(0.5)
q3=df.quantile(0.75)
iqr=q3-q1
low=q1-1.5*iqr
high=q3+1.5*iqr

dff=df[((df>=low)&(df<=high))]
dff

df1_new=df[((df>=q1-1.5*iqr)&(df<=q3+1.5*iqr))]
df1_new

sns.boxplot(data=df1_new)
sns.scatterplot(data=df1_new)
```
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/2cf669b8-4b3a-4611-9dc8-b78248957f2e)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/75ce8c28-a52d-40ce-b33c-bd1d23dc2d8d)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/475c3a26-ac70-42bb-834b-b11ab02d62ed)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/968d415f-d331-4dfe-a02c-c191d1632692)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/98eb0e05-fa76-4fc2-9ffb-f50ab0b5618b)
(3) use zscore of 3 to remove outliers. This is quite similar to IQR and you will get exact same result
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns

data=pd.read_csv("/content/bhp.csv")
df=pd.DataFrame(data)

z_score=np.abs(stats.zscore(df['price_per_sqft']))
newdata2=df[(z_score<3)]
print(newdata2)

outlier2=df[(z_score>=3)]
print(outlier2)

newdata2.shape

sns.boxplot(x="price_per_sqft",data=newdata2)
```
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/d673d949-3185-4faf-a2a8-c11fdfcd699a)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/600b119a-a887-43c1-82c8-09e6ff0b98ea)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/969affab-7008-43a5-be4b-16e22836cfa1)
(4) for the data set height_weight.csv find the following
(i) Using IQR detect height outliers and print them
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns

data=pd.read_csv("/content/height_weight.csv")
df=pd.DataFrame(data)
df.shape
df.describe()
df.info()

sns.boxplot(data=df)
sns.scatterplot(data=df)

sns.boxplot(x='height',data=df)

q1h=df['height'].quantile(0.25)
q2h=df['height'].quantile(0.5)
q3h=df['height'].quantile(0.75)
iqr_height=q3h-q1h
l_h=q1h-1.5*iqr_height
u_h=q3h+1.5*iqr_height

outlier_h=df[(df['height']<l_h)|(df['height']>u_h)]
print(outlier_h)

newdata_h=df[(df['height']>=l_h) & (df['height']<=u_h)]
print(newdata_h)

sns.boxplot(x='height',data=newdata_h)
```
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/ca6114d0-cb22-4211-ba07-8223adbe888f)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/98a97960-b7e5-45b7-a581-bef8be299c35)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/5de2e822-20d0-479e-ab93-afc7b727b59c)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/ca5a3733-bc8d-4a5f-8e5e-c6cd3aa891be)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/ab1ac0f5-3c0b-4e85-b2c4-176f5be1c308)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/aeb58b7b-310e-40d8-b40a-e2a1c4e6c472)
(ii) Using IQR, detect weight outliers and print them
```
sns.boxplot(x='weight',data=df)

q1w=df['weight'].quantile(0.25)
q2w=df['weight'].quantile(0.5)
q3w=df['weight'].quantile(0.75)
iqr_weight=q3w-q1w
l_w=q1w-1.5*iqr_weight
u_w=q3w+1.5*iqr_weight

outlier_w=df[(df['weight']<l_w)|(df['weight']>u_w)]
print(outlier_w)

newdata_w=df[(df['weight']>=l_w) & (df['weight']<=u_w)]
print(newdata_w)

sns.boxplot(x='weight',data=newdata_w)
```
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/32caee90-4a94-4e46-bc25-1243b10a58ba)
![image](https://github.com/BejinB/ODD2023---Datascience---Ex-02/assets/118367518/4d8ceba7-4741-4a72-af0b-b19de81559dc)
### RESULT:
the given datasets are read and outliers are detected and are removed using IQR and Z-score methods.









