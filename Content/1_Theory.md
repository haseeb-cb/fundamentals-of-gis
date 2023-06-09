### Fundamentals of Geographic Information Systems (GIS)

# Theory 1: Georeferencing & digitizing

## Spatial data sources

Spatial data is available through various sources, some of which are restricted, but a good amount is freely available. Common providers of spatial data are governmental institutions, local governments(cities and municipalities), education institutes, crowd sourced data, among others. Even some commercial companies provide open data. But there is also data that is restricted, for example because of commercial motivation, but also privacy or other reasons. It is however good to practice **open science** with GIS as well to make the data and research as accessible as possible.   

Examples of data sources are:
| Provider | Data | Note |
|--|--|--|
| City of Tampere | https://kartat.tampere.fi/oskari/?lang=en | Various datasets related to the city |
| Paituli | https://paituli.csc.fi/ | Collection of various Finnish data providers, mostly governmental institutes |
| Protected planet | https://www.protectedplanet.net/country/BRA | Worldwide collection of protected areas  |
| OpenStreetMap | https://www.openstreetmap.org/about | Community maintained data |

We keep a collection of our known data sources for your use: 
If you have any that are missing from this collection, please let us know! 

Data can either be accessed by downloading the dataset locally and importing the data, or by ad

- Data source methods
- Be critical of the data

But what if the data we need isn't already available or outdated? That's when we start gathering or making our own data, and where digitizing comes in.  

## Digitizing

When some kind of urban development happens, the data we use in GIS needs to updated. Someone has to go in and updated the changes to the roads, buildings, and others. This would be done by digitizing the changes, which is the process of **converting geographic data into digital form**. 

For this practice we are going to use the Nokia Arena development in Tampere, as you can see below, there have been a significant amount of changes with this project.

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/1_Theory/GIS_theory1_example.png)

And if we look at the data set we are working with, you can see that some of the demolished buildings are still present and new buildings lacking. 

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/1_Theory/QGIS_theory1_nokia_outdated.png)

In practice, updating this new development would consist of removing the old buildings from the data, and digitizing the new buildings, which would mean making new buildings in the data by **tracing** the buildings from some kind of reference picture. 

In this case we could potentially use the google imagery of the area, as this has already been updated. But this is not always the case, and satellite imagery is not the most accurate as the resolution is not high enough and pictures are taken at an angle. To get the most accuracy, we would survey the area and record the locations using high-accuracy equipment. But for our purpose we don't require high accuracy and we will use the following project plan as a source for the digitizing. 

![](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/1_Theory/GIS_theory1_plan.png)

This source is however missing geographic data, as it is just a picture taken from a PDF. To align this picture with our geographic data, we need to apply a process called georeferencing. 

## Georeferencing

Georeferencing is the process of **associating geographic data (coordinates) to a digital or physical object**, such as a map, image, or dataset, in our case a project plan. The goal of georeferencing is to establish a spatial reference for the object, enabling it to be positioned correctly within a coordinate system. It is essential for integrating different sources of geospatial data, enabling them to be overlaid and analyzed together. By assigning geographic coordinates or a coordinate system to an object, it becomes possible to accurately locate and spatially relate features, points, or areas represented within that object.

In practice, georeferencing involves identifying a set of control points on the object and matching them to corresponding locations on a reference map or in some form of software, such as QGIS. These control points represent identifiable features, such as road intersections or landmarks, and are used to create a transformation function that aligns the object with the reference system.

In our case we can use the buildings that remained unchanged and are on the project plan for reference to georeference the project plan, which we can then use to digitize the new buildings. 

<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJvSmFOSlZwYTFCeDRmd2tpIjp7In
N0YXJ0IjoxMTkzLCJlbmQiOjEyNTMsInRleHQiOiJXZSBrZWVw
IGEgY29sbGVjdGlvbiBvZiBvdXIga25vd24gZGF0YSBzb3VyY2
VzIGZvciB5b3VyIHVzZToifX0sImNvbW1lbnRzIjp7Imh3eUI5
c1duS3FveThyRlciOnsiZGlzY3Vzc2lvbklkIjoib0phTkpWcG
ExQng0ZndraSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBsaW5rIiwiY3JlYXRlZCI6MTY4NjMwMzgxMTk1NX19LC
JoaXN0b3J5IjpbLTE0NTIwNjA0NTcsLTQ5NTQ2ODQ4NywtOTUy
NzA2NjgsLTM2NzMzNDEyNCwtMzU0NjYwNjYxLDE3MTYyMDc1Nz
UsMTYzOTM4ODM2Nl19
-->