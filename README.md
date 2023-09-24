# policedata
US police data analysis in which peoples who are inspected by police.

import pandas as pd

import seaborn as sns

import matplotlib.pyplot as plt

police = pd.read_csv('police.csv')

* first we clean the data

sns.heatmap(police.isnull(),cbar=False)

police.info()

police.columns

police.drop(['county_name','search_type'], axis=1, inplace=True)

police = police.dropna(axis=0)

sns.heatmap(police.isnull(),cbar=False)

police.head()

gender = police.groupby(by = ['driver_gender', 'search_conducted'])



gender.driver_race.count()

* "Males are stopped for searches more frequently than females."


* now we transform the "search_conducted" column

def trans_search(v):
    if v== False:
        return 'not searched'
    else:
        return 'searched'

police['search_conducted']=police['search_conducted'].apply(func = trans_search)

* now the "search_conducted" column is converted to more representable value

police


plt.figure(figsize=(5, 4))
sns.countplot(x='driver_gender', hue='search_conducted', data=police)


plt.xlabel('Search Conducted')
plt.ylabel('Count')
plt.title('Search Conducted by Driver Gender')


plt.show()

police['violation_raw']

value_counts = police['violation_raw'].value_counts()

# Plot the pie chart
plt.figure(figsize=(10, 12))
plt.pie(value_counts, labels=value_counts.index, autopct='%1.1f%%', startangle=180)
plt.title('Distribution of Violations')
plt.tight_layout()

# Display the plot
plt.show()

