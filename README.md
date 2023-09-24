# policedata
US police data analysis in which peoples who are inspected by police.

import pandas as pd

import numpy as np

import matplotlib.pyplot as plt

import seaborn as sns


sns.set()

df = pd.read_csv("wnba.csv")

df.corr()['PTS'].sort_values()

round(df['MIN'].value_counts(bins=5,normalize=True)*100,2).sort_index()

population_mean = df['PTS'].mean()

min_1 = df[df['MIN']<= 213.2]
min_2 = df[df['MIN'].between(213.2, 414.4)]
min_3 = df[df['MIN'].between(414.4,615.6 )]
min_4 = df[df['MIN'].between(615.6,816.8 )]
min_5 = df[df['MIN'] >= 816.81]

proportional_sampling_means = []

for i in range(100):
    sample_min_1 = min_1["PTS"].sample(4, random_state = i)
    sample_min_2 = min_2["PTS"].sample(5, random_state = i)
    sample_min_3 = min_3["PTS"].sample(3, random_state = i)
    sample_min_4 = min_4["PTS"].sample(4, random_state = i)
    sample_min_5 = min_5["PTS"].sample(4, random_state = i)
    final_sample = pd.concat([sample_min_1, sample_min_2, sample_min_3, sample_min_4, sample_min_5])
    mean = final_sample.mean()
    proportional_sampling_means.append(mean)

plt.scatter(range(1,101), proportional_sampling_means)
plt.ylim(100,350)
plt.axhline(population_mean, color = "red")

plt.show()


df['PTS'].median()

plt.scatter(range(1,101), proportional_sampling_means)
plt.ylim(50,350)
plt.axhline(96, color = "red")
plt.axhline(217, color = "red")

plt.show()

