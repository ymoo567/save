# About project

> K-means algorithm is a type of unsupervised learning and is being applied in various fields. This project aims to combine K-means algorithms from a toy example to a real-world practical problem. The toy example is to divide the points given in the project into three clusters, and the real-world practical problem is to establish an infrastructure for the early regional air mobility (RAM) in Korea. In the former case, the focus is on the number of iterations of the k mean algorithm, and in the latter case, the focus is on determining the appropriate number of clusters.

------------------------------------------

# Information of two codes & Differences

#### Jong_Hyeon's code
> The process of calculating the distance between vertiport point and centroid point and clustering is summarized in the data frame. In addition, the process of updating clustering and calculating distance between the Vertiport point and the centroid point was implied in function in order to to make it possible to repeat the k mean algorithm several times.

#### Yun_Woo's code
> In this code, the number of elements contained in each cluster was compared by the k-means process. 
In the previous other code, the decision was made based on the coordinates of the center point, 
and in this code, it is intended to compare based on the number of elements in each cluster. 
If the number of elements in the clusters is the same as the previous execution, the code progress is stopped. 
One additional difference is that we import the folium library in problem 2 and represent it on the actual map. 
Therefore, it will be possible to visually and accurately recognize the location of each vertiport candidates, which is the result value.

-------------------------------------------

# About two files we used

> The two files consist of two fields: latitude & longitude.

> South_Korea_territory.csv - CSV data of South Korean territory coordinates with 1593 rows

> Vertiport_candidates.csv - CSV data of vertiport location coordinates with 304 rows

-----------------------------------------

# Code Requirements

> Python 3.10.7

> Pandas 1.5.1

> Matplotlib 3.2.2

> folium 0.12.1.post1

-----------------------------------------

# About function & parameters<br><br>

### Jong_Hyeon's code<br><br>

Problem 1.

Function(x,y)

X: list of x values of 8 points as given

Y: list of y values of 8 points as given


kmeans(x1,y1,x2,y2,x3,y3)

x1, x2, x3: x values of centroid points

y1, y2, y3: y values of centroid points<br><br>


problem2.

Function(x, y, cen_x, cen_y)

x: list of x values of 8 points as given

y: list of y values of 8 points as given

cen_x: list of x values of centroid points

cen_y: list of y values of centroid points

k_means(centroid_x, centroid_y)

centroid_x: list of x values of centroid points

centroid_y: list of y values of centroid points<br><br>

### Yun_Woo's code<br><br>
distance(x1, y1, x2, y2) - distance euclidean distance between (x1, y1), (x2, y2)<br><br>

### for Elbow method<br><br>

Install the package 'yellowbrick' which is Machine Learning Visualization Tools

Import KMeans module from sklearn

Visualize the data with KElbowVisualizer<br><br>


----------------------------------------------

# Q1. Divide the given 8 points into 3 clusters using k mean algorithms.

### Jong_Hyeon's code<br><br>
First, our team show a plot the eight points given in the problem. 

Next, we make a function to find the distance between eight points and centroid points by the Euclidean distance method, and show a data frame representing each points and distance using the function we made. 

This data frame also contains information of where the point is clustered. 

After that, a new centroid point was calculated and clustered information that went through the first iteration was represented as a plot. 

Finally, in order to repeat the k mean algorithm, all of the above processes were implied as a function named ‘kmeans’, and they were repeated until the previous centroid point and the new centroid point were the same. 

This process is expressed in the form of plot and centroid point, respectively.<br><br>

### Yun_Woo's code<br><br>
We have to use math library to define a new function necessary for calculating Euclidean distance.

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

--------------------------------------------

# Q2. Divide the RAM in South Korea using k mean algorithms.

### Jong_Hyeon's code<br><br>
First, our team load the given csv file in the problem and put the information of Korea's territory and Vertiport point in the plot. 

Next, we used the mean algorithm to divide the vertiport point into 10 clusters, and in the process of dividing, we used the two functions we made. 

One is to find the distance between vertiport points and centroid points by the Euclidean distance method, and the other could calculate centroid point, and cluster the point. 

We expressed the process of clustering in plot. Lastly, the Elbow method was used to find the appropriate number of clusters.<br><br>

### Yun_Woo's code<br><br>
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

If the following results are printed, you can define as the progress has been successfully executed.<br><br>

![화면 캡처 2022-11-18 113324](https://user-images.githubusercontent.com/118390275/202603602-789841e6-98cf-4d4f-bab5-73137230f068.png)
