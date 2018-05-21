import codecademylib
import pandas as pd
from matplotlib import pyplot as plt
species = pd.read_csv('species_info.csv')
print(species.head())


species_count = species.scientific_name.nunique()
print(species_count)
species_type = species.category.unique()
print(species_type)
conservation_statuses = species.conservation_status.unique()
print(conservation_statuses)

conservation_counts = species.groupby('conservation_status').scientific_name.nunique().reset_index()
print(conservation_counts)

pecies.fillna('No Intervention', inplace = True)

conservation_counts_fixed = species.groupby('conservation_status').scientific_name.nunique().reset_index()
print(conservation_counts_fixed)

pecies = pd.read_csv('species_info.csv')

species.fillna('No Intervention', inplace = True)
protection_counts = species.groupby('conservation_status')\
    .scientific_name.nunique().reset_index()\
    .sort_values(by='scientific_name')
print(protection_counts)

plt.figure(figsize = (10,4))
ax = plt.subplot()
x = [0, 1, 2, 3, 4]
y = protection_counts.scientific_name.values
plt.bar (x, y)
ax.set_xticks ([0, 1, 2, 3, 4])
ax.set_xticklabels(protection_counts.conservation_status.values)
plt.ylabel('Number of Species')
plt.title('Conservation Status by Species')
plt.show()

pecies = pd.read_csv('species_info.csv')
print(species)

species.fillna('No Intervention', inplace = True)

species['is_protected'] = species.conservation_status != 'No Intervention'
category_counts = species.groupby(['category', 'is_protected']).scientific_name.nunique().reset_index()
print(category_counts.head())

category_pivot = category_counts.pivot(\
    columns='is_protected',\
    index='category',\
    values='scientific_name').reset_index()
print(category_pivot)

# Loading the Data
species = pd.read_csv('species_info.csv')

# print species.head()

# Inspecting the DataFrame
species_count = len(species)

species_type = species.category.unique()

conservation_statuses = species.conservation_status.unique()

# Analyze Species Conservation Status
conservation_counts = species.groupby('conservation_status').scientific_name.count().reset_index()

# print conservation_counts

# Analyze Species Conservation Status II
species.fillna('No Intervention', inplace = True)

conservation_counts_fixed = species.groupby('conservation_status').scientific_name.count().reset_index()

# Plotting Conservation Status by Species
protection_counts = species.groupby('conservation_status')\
    .scientific_name.count().reset_index()\
    .sort_values(by='scientific_name')
    
# plt.figure(figsize=(10, 4))
# ax = plt.subplot()
# plt.bar(range(len(protection_counts)),
#        protection_counts.scientific_name.values)
# ax.set_xticks(range(len(protection_counts)))
# ax.set_xticklabels(protection_counts.conservation_status.values)
# plt.ylabel('Number of Species')
# plt.title('Conservation Status by Species')
# labels = [e.get_text() for e in ax.get_xticklabels()]
# print ax.get_title()
# plt.show()

species['is_protected'] = species.conservation_status != 'No Intervention'

category_counts = species.groupby(['category', 'is_protected'])\
                         .scientific_name.count().reset_index()
  
# print category_counts.head()

category_pivot = category_counts.pivot(columns='is_protected', index='category', values='scientific_name').reset_index()

category_pivot.columns = ['category', 'not_protected', 'protected']

category_pivot['percent_protected'] = category_pivot.protected / (category_pivot.protected + category_pivot.not_protected)

print category_pivot.head()

contingency = [[30, 146],
     [75, 413]]
chi2, pval, dof, expected = chi2_contingency(contingency)
print pval

contingency = [[5, 73],
     [30, 146]]
chi2, pval_reptile_mammal, dof, expected = chi2_contingency(contingency)
print pval_reptile_mammal

species = pd.read_csv('species_info.csv')
species.fillna('No Intervention', inplace = True)
species['is_protected'] = species.conservation_status != 'No Intervention'

observations =  pd.read_csv('observations.csv')
print(observations.head())

species['is_sheep'] = species.common_names.apply (lambda x : \
True if 'Sheep' in x else False)

species_is_sheep = species[species.is_sheep == True]
print(species_is_sheep)
sheep_species = species[(species.is_sheep == True) &
(species.category == 'Mammal')]
print(sheep_species)

sheep_observations = pd.merge(sheep_species, observations)
print(sheep_observations.head())

obs_by_park = sheep_observations.groupby('park_name').observations.sum().reset_index()

print(obs_by_park)


figsize=(16, 4)
ax = plt.subplot()
x = [0, 1, 2, 3]
y = obs_by_park.observations.values
plt.bar(x,y)
ax.set_xticks([0, 1, 2, 3])
ax.set_xticklabels(obs_by_park.park_name.values, rotation=45)
plt.ylabel('Number of Observations')
plt.title('Observations of Sheep per Week')
plt.show()

baseline = 15
minimum_detectable_effect = 33.3
sample_size_per_variant = 870
yellowstone_weeks_observing = 1.716
bryce_weeks_observing = 3.48

