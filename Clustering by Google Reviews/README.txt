https://slides.com/jvbw/clustering-by-google-reviews

**************

https://archive.ics.uci.edu/ml/datasets/Tarvel+Review+Ratings


Attribute 1 : Unique user id 
Attribute 2 : Average ratings on churches 
Attribute 3 : Average ratings on resorts 
Attribute 4 : Average ratings on beaches 
Attribute 5 : Average ratings on parks 
Attribute 6 : Average ratings on theatres 
Attribute 7 : Average ratings on museums 
Attribute 8 : Average ratings on malls 
Attribute 9 : Average ratings on zoo 
Attribute 10 : Average ratings on restaurants 
Attribute 11 : Average ratings on pubs/bars 
Attribute 12 : Average ratings on local services 
Attribute 13 : Average ratings on burger/pizza shops 
Attribute 14 : Average ratings on hotels/other lodgings 
Attribute 15 : Average ratings on juice bars 
Attribute 16 : Average ratings on art galleries 
Attribute 17 : Average ratings on dance clubs 
Attribute 18 : Average ratings on swimming pools 
Attribute 19 : Average ratings on gyms 
Attribute 20 : Average ratings on bakeries 
Attribute 21 : Average ratings on beauty & spas 
Attribute 22 : Average ratings on cafes 
Attribute 23 : Average ratings on view points 
Attribute 24 : Average ratings on monuments 
Attribute 25 : Average ratings on gardens


**************
Understanding the data :

UCI Machine learning repository
Google reviews on attractions from 24 categories across Europe
From 1 to 5
Average user rating per category


5456 rows, 26 columns
not much cleaning

**************
Exploratory Analysis :
I renamed the columns for better lisibility.
There are no outliers (we see this from the 'describe'), and no nans. The DF is clean.

However : the zeros, I feel, are going to bias the means and calculations.
I'm going to switch back and forth between zeros and nans, as nans are not taken into account when calculating means. I'll switch back to zeros when doing PCAs and plots.

The correlation heatmap seems to show some relationships,that could appear in clusters : 
# churches, cafes, beaches, gardens, monuments "historical tourism"
# parks and viewpoints "outdoorsy ppl"
# malls, zoos and restaurants  "family ppl"...


**************
Feature Engineering :

First try of PCA on the basic data gave poor results, about 45% over 3 components.
I decided to join columns into (subjective) groups.
I created lists, put the lists into a dictionnary, and wrote a function to replace columns.

The PCA on this shrunken data worked better : after MinMax Scaling, we obtain about 58% explained data.

**************
Clustering :
I tested KMeans, Agglomerative Clustering, DBSCAN, Gaussian Mixture for clustering.

The best results were Kmeans and Gaussian Mix. After a visual inspection of scatter plots, I decided to go with Kmeans.

**************
Understanding clusters :
(keep in mind that when re-running the code, clusters might change order)

Cluster 1
enjoy nature and cultural outings, while travelling abroad

Cluster 2
travellers with an extra interest in beauty resorts and cultural and historical locations

Cluster 3
love malls, culture and eating at restaurants.

Cluster 4
love their food and snacks, at home and while travelling !

Cluster 5
your typical dynamic neighbour : food, nightlife, malls and love local services

**************
Conclusions :
Clustering users to send them promotional offers depending on their preferences
Classifying the columns was the most subjective step and had a direct impact on the clusters => in real life, ask an expert ?
PCA wasn't perfect but still gave ok results
Original data could have dealt with zeros better, I felt it biased the overall scores