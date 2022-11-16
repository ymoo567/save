# Information of this project

The goal of this project is to cluster coordinate points using the k-means algorithm. The initial k value was designated as 3 in question 1 and 10 in question 2. In Problem 1, where 8 coordinates and 3 initial center points were set, a graph was drawn on the python plot, and the distance from 8 points to each center point was calculated and clustered. In the second problem, coordinates representing the boundary value of South Korea and coordinates of several candidate sites in the area were used to determine the vertiport candidate site. Through clustering, the regions were divided into 10 clusters, and among them, the coordinates at the center of each cluster were calculated to derive the final 10 candidate sites. A detailed description of the code is provided below.

-----------------------------------------

# Question 1.


##### Import libraries required for operation
    import matplotlib.pyplot as plt

    import math


##### Make a new function that calculates the distance between two points
    def distance(x1, y1, x2, y2):

    result = math.sqrt(math.pow(x1 - x2, 2) + math.pow(y1 - y2, 2))
    
    return result

##### Define three center points & eight given points
    c1 = (2, 10)
    c2 = (5, 8)
    c3 = (1, 2)
    
    p1 = (2, 5)
    p2 = (8, 4)
    p3 = (7, 5)
    p4 = (6, 4)
    p5 = (4, 9)
    p6 = (2, 10) # center point
    p7 = (5, 8) # center point
    p8 = (1, 2) # center point


##### Visualize the eight given coordinates with black dot
##### Three center points are displayed with each cluster color with star
    plt.scatter(p1[0], p1[1], c = 'black')
    plt.scatter(p2[0], p2[1], c = 'black')
    plt.scatter(p3[0], p3[1], c = 'black')
    plt.scatter(p4[0], p4[1], c = 'black')
    plt.scatter(p5[0], p5[1], c = 'black')
    plt.scatter(p6[0], p6[1], c = 'black')
    plt.scatter(p7[0], p7[1], c = 'black')
    plt.scatter(p8[0], p8[1], c = 'black')

    plt.scatter(c1[0], c1[1], c = 'r', marker = '*', s = 100)
    plt.scatter(c2[0], c2[1], c = 'g', marker = '*', s = 100)
    plt.scatter(c3[0], c3[1], c = 'b', marker = '*', s = 100)
    plt.show()

##### make new empty lists, which distance value (distance between each points with 3 center points) will be stored
##### (to make indexing each information more comfortable, make this list as two-dimention list)
    c = [c1, c2, c3] # 'c' is a list that stores cordinates of three center points
    p = [p1, p2, p3, p4, p5, p6, p7, p8] # 'p' is a list that stores cordinates of eight given points
    pdis = []
    n1 = []
    n2 = []
    n3 = []
    m = [n1, n2, n3] # each lists will be stored in one large list
    llistt = [] # save the number of how many we attempted the k-means process
    cnt = 1 # this is first iteration
    
    for i in list(range(len(p))):
      pdis.append([])
      for o in list(range(len(c))):
        pdis[i].append(distance(p[i][0], p[i][1], c[o][0], c[o][1]))

    for i in list(range(len(p))): # eight process - results of which center point is nearest with each eight points
      print(i + 1, "번째 점은", pdis[i].index(min(pdis[i])) + 1, "번째 Center와 가장 가깝습니다.") # derive result through indexing
      if (pdis[i].index(min(pdis[i])) + 1) == 1: # if the point is closest to the first center point
        plt.scatter(p[i][0], p[i][1], c = 'r') # cluster it with red color
        n1.append(p[i]) # save the coordinates of the points(in the first cluster) in the n1 list
      if (pdis[i].index(min(pdis[i])) + 1) == 2: # if the point is closest to the second center point
        plt.scatter(p[i][0], p[i][1], c = 'g') # cluster it with green color
        n2.append(p[i]) # save the coordinates of the points(in the second cluster) in the n2 list
      if (pdis[i].index(min(pdis[i])) + 1) == 3: # if the point is closest to the third center point
        plt.scatter(p[i][0], p[i][1], c = 'b') # cluster it with blue color
        n3.append(p[i]) # save the coordinates of the points(in the third cluster) in the n3 list

##### calculate the number of each cluster's elements and visualize it in the plot
    print(" ")
    for i in range(0, 3):
      print(i + 1, "번째 클러스터 원소의 개수는", len(m[i])) # save in each cluster's list & print how many elements (coordinates) each cluster contains
    print(" ")
    plt.show()
![화면 캡처 2022-11-17 044654](https://user-images.githubusercontent.com/118390275/202279365-a85a5ac7-3b9d-4439-9260-5857b2251c7d.png)

##### number of each cluster's element
![화면 캡처 2022-11-17 043849](https://user-images.githubusercontent.com/118390275/202277973-d442a197-d445-4c53-9bbd-686e8ddfd6dd.png)

##### visualize in the plot
![화면 캡처 2022-11-17 044125](https://user-images.githubusercontent.com/118390275/202278300-8333727d-5408-4d3e-ac28-f9b1a6a3c5ac.png)

##### with these result, we have to figure out new center point,
##### which is the center of mass(weight center) of each cluster points
    for i in list(range(1, 9)):
      if (pdis[i - 1].index(min(pdis[i - 1])) + 1) == 1: 
        plt.scatter(p[i - 1][0], p[i - 1][1], c = 'r')
      if (pdis[i - 1].index(min(pdis[i - 1])) + 1) == 2:
        plt.scatter(p[i - 1][0], p[i - 1][1], c = 'g') 
      if (pdis[i - 1].index(min(pdis[i - 1])) + 1) == 3:
        plt.scatter(p[i - 1][0], p[i - 1][1], c = 'b') 

    list1 = [] # make a empty list to save X coordinates of each points
    list2 = [] # make a empty list to save Y coordinates of each points

    for o in list(range(len(c))): # index number (0~2) of new 3 center point
      list1.append([]) 
      list2.append([])
      for i in list(range(len(m[o]))): # run as number of elements in each cluster
        list1[o].append(m[o][i][0]) # For ease of indexing, create a two-dimensional list and store it in order for each cluster
        list2[o].append(m[o][i][1]) 
      if len(list1) == 0: # If the number of elements in a particular cluster is zero (though that won't happen), then proceed without running
        continue
      else: # Calculate the average value of coordinates in each cluster to create a new center point and store it to 'c'
        c[o] = (sum(list1[o]) / len(list1[o]), sum(list2[o]) / len(list2[o]))

    # save the coordinates(center point) of first iteration
    llistt.append(c)
    print(cnt, "번째 iteration의 center point까지 :", llistt)
    print(" ")
    print(cnt, "번째 iteration")

    # mark new center points in scatter plot
    plt.scatter(c[0][0], c[0][1], c = 'r', marker = '*', s = 100)
    plt.scatter(c[1][0], c[1][1], c = 'g', marker = '*', s = 100)
    plt.scatter(c[2][0], c[2][1], c = 'b', marker = '*', s = 100)
    plt.show()
    
![화면 캡처 2022-11-17 044302](https://user-images.githubusercontent.com/118390275/202278646-5936a2c2-9271-44c0-9d5e-a11724a13f46.png)

-------------------------------------------

##### From the second process, we will put the above in one cell and execute it as a whole to watch the results.

    cnt += 1 # number of attempts

    p = [p1, p2, p3, p4, p5, p6, p7, p8]
    pdis = []
    n1 = []
    n2 = []
    n3 = []
    m = [n1, n2, n3]

    for i in list(range(len(p))):
      pdis.append([])
      for o in list(range(len(c))):
        pdis[i].append(distance(p[i][0], p[i][1], c[o][0], c[o][1]))

    for i in list(range(len(p))): 
      print(i + 1, "번째 점은", pdis[i].index(min(pdis[i])) + 1, "번째 Center와 가장 가깝습니다.") 
      if (pdis[i].index(min(pdis[i])) + 1) == 1: 
        plt.scatter(p[i][0], p[i][1], c = 'r') 
        n1.append(p[i])
      if (pdis[i].index(min(pdis[i])) + 1) == 2:
        plt.scatter(p[i][0], p[i][1], c = 'g') 
        n2.append(p[i]) 
      if (pdis[i].index(min(pdis[i])) + 1) == 3:
        plt.scatter(p[i][0], p[i][1], c = 'b') 
        n3.append(p[i]) 

    print(" ")
    for i in range(0, 3):
      print(i + 1, "번째 클러스터 원소의 개수는", len(m[i]))
    print(" ")

    list1 = [] 
    list2 = [] 

    for o in list(range(len(c))): 
      list1.append([]) 
      list2.append([])
      for i in list(range(len(m[o]))):
        list1[o].append(m[o][i][0])
        list2[o].append(m[o][i][1]) 
      if len(list1) == 0: 
        continue
      else: 
        c[o] = (sum(list1[o]) / len(list1[o]), sum(list2[o]) / len(list2[o]))

    llistt.append(c)
    print(cnt, "번째 iteration의 center point까지 :", llistt)
    print(" ")
    print(cnt, "번째 iteration")

    plt.scatter(c[0][0], c[0][1], c = 'r', marker = '*', s = 100)
    plt.scatter(c[1][0], c[1][1], c = 'g', marker = '*', s = 100)
    plt.scatter(c[2][0], c[2][1], c = 'b', marker = '*', s = 100)
    plt.show()

##### As each executions runs through, the center point of the cluster gradually stabilizes and the change decreases.

##### Second iteration
![화면 캡처 2022-11-17 044944](https://user-images.githubusercontent.com/118390275/202279915-697bf3eb-2188-476d-9dfd-54d0204563d3.png)

##### Third iteration
![화면 캡처 2022-11-17 045053](https://user-images.githubusercontent.com/118390275/202280150-c3bea4f4-9e97-4e4f-8be9-a0ed15628a95.png)

##### Fourth iteration
![화면 캡처 2022-11-17 045144](https://user-images.githubusercontent.com/118390275/202280263-a98fc206-e813-4c69-8822-b5b86b2efc7c.png)

##### It can be considered that there is little change after the fourth iteration, so we ended up this process.

-----------------------------------------

# Question 2.

##### This codes are made by Google Colab, so it is necessary to mount it on Google Drive
    from google.colab import drive
    drive.mount('/content/drive')

##### Import several necessary library for the k-means progress
    import pandas as pd
    import math
    import folium

##### South Korea Border Coordinates (Point Data)

    krt = pd.read_csv('/content/drive/MyDrive/2022-2 기계학습개론/South_Korea_territory.csv')
    krt
![화면 캡처 2022-11-17 045829](https://user-images.githubusercontent.com/118390275/202281696-c5b39f37-19f2-4433-a7c9-5a5ecdf944f2.png)

##### Generate an empty list for saving the S.K boundary coordinates
    terr_list = []
    for data in krt.index:
      terr_list.append((krt.loc[data, 'Latitude (deg)'], krt.loc[data, 'Longitude (deg)']))
    terr_list

![화면 캡처 2022-11-17 050012](https://user-images.githubusercontent.com/118390275/202282033-6301e0ac-2942-4a89-9c02-a5f9e22a7494.png)

##### Vertiport Candidate Coordinates (Point Data)

    vrc = pd.read_csv('/content/drive/MyDrive/2022-2 기계학습개론/Vertiport_candidates.csv')
    vrc
![화면 캡처 2022-11-17 050123](https://user-images.githubusercontent.com/118390275/202282293-454a6e54-e0e7-4139-a997-16509e9a2a2d.png)

##### Extract data of 10 rows by random from Vertiport Candidate Coordinates data

    initialvrc = vrc.sample(n = 10)
    initialvrc
![화면 캡처 2022-11-17 050314](https://user-images.githubusercontent.com/118390275/202282659-c996e5b2-dc5f-4dd1-82c7-0437806bc4b6.png)

##### When the coordinates are displayed with a general plot, the coordinates are distorted. Therefore, folium library was used for clear notation.
##### Set Map Default Point of View
##### Visualize South Korea border address point data with lines

      Map = folium.Map(location=[36.220711, 128.058276], zoom_start = 7)
      folium.PolyLine(terr_list, color = 'black').add_to(Map)
      # if you want to change theme of map, add - tiles = 'Stamen Toner'

##### Mark all candidate coordinates as dots in black
##### 10 randomly drawn coordinates are then marked in red
##### Set the red dot to the initial center point

    for data in vrc.index:
      longt = vrc.loc[data, 'Longitude (deg)']
      lat = vrc.loc[data, 'Latitude (deg)']
      folium.CircleMarker([lat, longt], color = 'black', radius = 0.1).add_to(Map)

    for data in initialvrc.index:
      longt = initialvrc.loc[data, 'Longitude (deg)']
      lat = initialvrc.loc[data, 'Latitude (deg)']
      folium.CircleMarker([lat, longt], color = 'red', radius = 0.1).add_to(Map)

    Map
![화면 캡처 2022-11-17 050645](https://user-images.githubusercontent.com/118390275/202283305-1fb3a741-fc6b-4dc3-a908-99ecd6d9eda8.png)

##### Define a function that calculates the euclidean distance between each point

    def distance(x1, y1, x2, y2):
        result = math.sqrt(math.pow(x1 - x2, 2) + math.pow(y1 - y2, 2))
        return result

##### 

    c = c_location_list # 10 random list of given coordinates
    p = location_list # vertiport candidates coordinates
    pdis = [] # Calculate the distance from each point to the center point and store it in an empty list
    n1 = [] # Create an empty list, each list will contain coordinate values contained in the n th cluster
    n2 = []
    n3 = []
    n4 = []
    n5 = []
    n6 = []
    n7 = []
    n8 = []
    n9 = []
    n10 = []
    m = [n1, n2, n3, n4, n5, n6, n7, n8, n9, n10] # Create as a two-dimensional list to easy indexing

    for i in list(range(len(p))):
      pdis.append([])
      for o in list(range(len(c))):
        pdis[i].append(distance(p[i][0], p[i][1], c[o][0], c[o][1]))

    pdis # Distance information from each point to 10 center points is stored in the list. Each list contains 10 elements

#####

    Map = folium.Map(location=[36.220711, 128.058276], zoom_start = 7) # Camera view initialization
    folium.PolyLine(terr_list, color = 'black').add_to(Map) # South Korean territory marking

    # Using the index order of the list generated above, find the shortest distance from each point to center points

    for i in list(range(len(p))): 
      print(i + 1, "번째 점은", pdis[i].index(min(pdis[i])) + 1, "번째 Center와 가장 가깝습니다.") 
      if (pdis[i].index(min(pdis[i])) + 1) == 1: # If it is closest to the first center point,
        n1.append(p[i]) # Store the coordinates of the points in the first cluster in the n1 list
        folium.CircleMarker(p[i], color = 'red', radius = 0.1).add_to(Map) # Mark in red on the map
      if (pdis[i].index(min(pdis[i])) + 1) == 2:
        n2.append(p[i])
        folium.CircleMarker(p[i], color = 'blue', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 3:
        n3.append(p[i])
        folium.CircleMarker(p[i], color = 'green', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 4:
        n4.append(p[i])
        folium.CircleMarker(p[i], color = 'yellow', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 5:
        n5.append(p[i])
        folium.CircleMarker(p[i], color = 'purple', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 6:
        n6.append(p[i])
        folium.CircleMarker(p[i], color = 'darkorange', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 7:
        n7.append(p[i])
        folium.CircleMarker(p[i], color = 'lime', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 8:
        n8.append(p[i])
        folium.CircleMarker(p[i], color = 'lightseagreen', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 9:
        n9.append(p[i])
        folium.CircleMarker(p[i], color = 'darkviolet', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 10:
        n10.append(p[i])
        folium.CircleMarker(p[i], color = 'firebrick', radius = 0.1).add_to(Map)

    for i in range(0, 10):
      print(i + 1, "번째 클러스터 원소의 개수는", len(m[i])) # Save to each cluster list and print how many elements (coordinates) each cluster contains

    Map

##### Newly clustered coordinates
![화면 캡처 2022-11-17 051542](https://user-images.githubusercontent.com/118390275/202285056-e3d5da01-5690-4909-83f7-02465472f9af.png)

##### The process of finding a new center point

    list1 = []
    list2 = []

    for o in list(range(len(c))): # New 10 center point indexes (0 to 9)
      for i in list(range(len(m[o]))): # Range the number of elements in each cluster
        list1.append([]) 
        list1[o].append(m[o][i][0]) # For ease of indexing, create a two-dimensional list and store it in order for each cluster as well
        list2.append([])
        list2[o].append(m[o][i][1])
      if len(list1) == 0: # If the number of elements in a particular cluster is zero (though that won't happen), then pass the code without running
        continue
      else: # Calculate the average value of coordinates in a cluster to create a new center point and save it in the 'c'
        c[o] = (sum(list1[o]) / len(list1[o]), sum(list2[o]) / len(list2[o]))

    Map = folium.Map(location=[36.220711, 128.058276], zoom_start = 7)
    folium.PolyLine(terr_list, color = 'black').add_to(Map)

    cnt = 1 # Save the number of iterations in the cnt

    for i in range(0, 10):
      folium.CircleMarker(c[i], color = 'red', radius = 0.1).add_to(Map)
    Map # Display 10 newly created center points on the map
    
![화면 캡처 2022-11-17 051943](https://user-images.githubusercontent.com/118390275/202285792-efa879a4-aa9d-43ab-b009-e607a50cc42f.png)

##### Repeat the same as the above process
##### Increase the number of times by repeatedly executing the code in the cell

    cnt += 1 # number of iteration + 1

    list1 = []
    list2 = []

    for o in list(range(len(c))):
      for i in list(range(len(m[o]))):
        list1.append([])
        list1[o].append(m[o][i][0])
        list2.append([])
        list2[o].append(m[o][i][1])
      if len(list1) == 0:
        continue
      else:
        c[o] = (sum(list1[o]) / len(list1[o]), sum(list2[o]) / len(list2[o]))

    pdis = []
    n1 = []
    n2 = []
    n3 = []
    n4 = []
    n5 = []
    n6 = []
    n7 = []
    n8 = []
    n9 = []
    n10 = []
    m = [n1, n2, n3, n4, n5, n6, n7, n8, n9, n10]

    for i in list(range(len(p))):
      pdis.append([])
      for o in list(range(len(c))):
        pdis[i].append(distance(p[i][0], p[i][1], c[o][0], c[o][1]))

    Map = folium.Map(location=[36.220711, 128.058276], zoom_start = 7)
    folium.PolyLine(terr_list, color = 'black').add_to(Map)

    for i in list(range(len(p))):
      print(i + 1, "번째 점은", pdis[i].index(min(pdis[i])) + 1, "번째 Center와 가장 가깝습니다.")
      if (pdis[i].index(min(pdis[i])) + 1) == 1:
        n1.append(p[i])
        folium.CircleMarker(p[i], color = 'red', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 2:
        n2.append(p[i])
        folium.CircleMarker(p[i], color = 'blue', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 3:
        n3.append(p[i])
        folium.CircleMarker(p[i], color = 'green', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 4:
        n4.append(p[i])
        folium.CircleMarker(p[i], color = 'yellow', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 5:
        n5.append(p[i])
        folium.CircleMarker(p[i], color = 'purple', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 6:
        n6.append(p[i])
        folium.CircleMarker(p[i], color = 'darkorange', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 7:
        n7.append(p[i])
        folium.CircleMarker(p[i], color = 'lime', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 8:
        n8.append(p[i])
        folium.CircleMarker(p[i], color = 'lightseagreen', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 9:
        n9.append(p[i])
        folium.CircleMarker(p[i], color = 'darkviolet', radius = 0.1).add_to(Map)
      if (pdis[i].index(min(pdis[i])) + 1) == 10:
        n10.append(p[i])
        folium.CircleMarker(p[i], color = 'firebrick', radius = 0.1).add_to(Map)

    print(cnt, "번째 iteration") # Print by using the cnt variable to print how many iteration was excuted

    Map

##### After progressing until the number of elements in each cluster is same with the previous step
![화면 캡처 2022-11-17 052311](https://user-images.githubusercontent.com/118390275/202286391-2f5f8fdd-7f95-4685-afe6-ffd3fd87e522.png)

##### 10 newly created center points are displayed separately on the map

list1 = []
list2 = []

for o in list(range(len(c))):
  for i in list(range(len(m[o]))):
    list1.append([])
    list1[o].append(m[o][i][0])
    list2.append([])
    list2[o].append(m[o][i][1])
  if len(list1) == 0:
    continue
  else:
    c[o] = (sum(list1[o]) / len(list1[o]), sum(list2[o]) / len(list2[o]))

Map = folium.Map(location=[36.220711, 128.058276], zoom_start = 7)
folium.PolyLine(terr_list, color = 'black').add_to(Map)

for i in range(0, 10):
  folium.Marker(c[i], color = 'blue', radius = 0.1).add_to(Map)
Map
![화면 캡처 2022-11-17 052529](https://user-images.githubusercontent.com/118390275/202286799-bbdb4154-ad25-4f1b-909d-a851122714e8.png)



