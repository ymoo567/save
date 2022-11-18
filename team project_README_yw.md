# Information of this code

In this code, the number of elements contained in each cluster was compared by the k-means process. 
In the previous other code, the decision was made based on the coordinates of the center point, 
and in this code, it is intended to compare based on the number of elements in each cluster. 
If the number of elements in the clusters is the same as the previous execution, the code progress is stopped. 

One more difference is that we import the folium library in problem 2 and represent it on the actual map. 
Therefore, it will be possible to visually and accurately recognize the location of each vertiport candidates, which is the result value.

-----------------------------------------

# Code Requirements

Python 3.10.7

Pandas 1.3.5

Matplotlib 3.2.2

folium 0.12.1.post1

-----------------------------------------

# Description

### Q1.

We will use math library to define a new function necessary for calculating Euclidean distance.

Coordinate information of each centroid and Given points is saved in the list, respectively.

After that, repetitive sentences were used to compare the distances of each coordinate, 
and through the indexing process, it was figured out the closest centroid point from each given 8 points.

The number of elements included in each cluster is printed, and each location and cluster has been visualized in a plot.

In each newly determined cluster, the average (center of gravity) coordinates of each cluster are calculated and defined as a new centroid point.

The new centroid points are represented by star shapes, and the existing eight points are represented by dots.
Points of the same color are included in the same cluster.

After the first iteration, repeat the previous process and check the results for each iteration.
It is contained in one cell, so this process might conveniently carried out.

In code 1, the total amount of coordinates is very small, so it will be compared with coordinate values of centroid points rather than the number of elements.



### Q2.

Import the necessary libraries(pandas / folium) to use data frames and actual maps.

A given South Korean boundary coordinate value and the coordinate value of vertiport candidates are stored in a data frame, and these data are saved in a list.
Using the sample, the coordinates of 10 of them are randomly selected and designated as the initial centroid point.

Bring up the folium library and enter the central coordinates of the Korean Peninsula(36.220711, 128.058276) as the default point of view.
The boundary value of South Korea is indicated by polyline, and the coordinates of the candidate site are indicated by dots.

We will use the same function which is newly defined in the previous problem for calculating the distance between two points.

The coordinates of each point stored in the list are applied exactly as in question 1 to calculate the distance between each point.
Thereafter, candidate points close to each centroid point are included in one cluster.

Every points are included into each clusters and visualized on the map with different colors.
Using the coordinate values of each cluster, the coordinates of 10 new centroid points have been figured out and displayed on the map.

After that, check the results while executing one cell in the same way as question 1.
If the number of elements contained in each cluster is the same as in the previous execution, the execution is stopped.
Display the final results on the map.

------------------------------------------

## result

If the following results are printed, you can define as the progress has been successfully executed.

![화면 캡처 2022-11-18 113324](https://user-images.githubusercontent.com/118390275/202603602-789841e6-98cf-4d4f-bab5-73137230f068.png)
