### Fundamentals of Geographic Information Systems (GIS)

# Theory 3: Socio-spatial differentiation & social segregation

## Background information
Socio-spatial differentiation refers to the **unequal distribution of social groups and resources across space**. It recognizes that cities and other geographic areas are not homogeneous entities, but rather consist of diverse neighborhoods, districts, or zones that are characterized by distinct social, economic, and cultural features. These areas can be differentiated based on factors such as income levels, educational attainment, employment opportunities, housing conditions, access to amenities and services, and racial or ethnic composition.

This spatial segregation can lead to disparities in quality of life, opportunities, and social interactions between different social groups. Socio-spatial differentiation often reflects patterns of social inequality and segregation within a society. Certain groups may concentrate in specific areas due to historical, economic, or cultural factors, while others may be excluded or marginalized from accessing certain spaces or resources.

Understanding socio-spatial differentiation is important for analyzing and addressing social inequalities and urban development challenges. It helps identify areas that may be experiencing higher levels of deprivation or exclusion, and informs policies and interventions aimed at promoting more inclusive and equitable spatial patterns within cities and regions.

- Example picture of socio-spatial differentiation

GIS (Geographic Information System) is a powerful tool that can be used to analyze and understand socio-spatial differentiation. By **integrating spatial data with social and demographic information**, GIS enables researchers and planners to examine the relationships between different social groups and the spaces they occupy.

GIS can provide visual representations of socio-spatial patterns, allowing for the identification of concentrations, disparities, and spatial dynamics within a given area. It can map variables such as income levels, educational attainment, or racial composition, allowing for the visualization of spatial variations and patterns of social differentiation. GIS can also integrate additional layers of information, such as transportation networks, amenities, and services, to better understand the spatial dimensions of social inequality and access to resources.

With GIS, it is possible to conduct spatial analyses and modeling to assess the impacts of socio-spatial differentiation on various aspects of urban life. For example, researchers can examine the relationship between neighborhood characteristics and health outcomes, educational opportunities, or crime rates. GIS can also assist in identifying areas of social exclusion, helping policymakers target interventions and resources to address spatial inequalities and promote more inclusive development.

Furthermore, GIS allows for the monitoring and evaluation of policies and interventions aimed at reducing socio-spatial differentiation. By analyzing spatial data over time, planners can assess the effectiveness of urban development strategies and determine whether they contribute to more equitable spatial patterns and improved social outcomes.

- Example picture of GIS analysis


## Dataset
The exercise accompanying this theory section consists of a GIS socio-spatial differentiation analysis. We will be using the Statistics Finland's Grid Database, which as the name suggests consists of a grid of cells, each of which describes various statistics of the area it covers. In this exercise specifically we will be looking at a 250x250m scale at the spatial distribution of level of education and income in Helsinki. 

- Example picture of this dataset

We learned previously that raster data consists of a continuous surface divided into a grid of cells, where each cell corresponds to a specific location and contains a value representing a particular attribute. This value is represented by the color of the cell, images are in a way rasters as well, specifically JPEG, PNG, and GIF images. Do you remember seeing in movies that they store data in pictures? This is not unrealistic, as you could just see pictures as a raster where the color of each cell represents its value. One limitation of rasters however, is that a cell can only hold 1 value , since the cell can also only be 1 color. This is sufficient for a lot of cases, for example a raster which describes the slope of the area only needs one value per cell, the slope. But if we want to use multiple values in a raster, such as statistics of the cells, we need to make use of a grid in a vector format. This is the case in the Statistics Finland's Grid Database, as you will see when you do the exercise. This is important to keep in mind in the future, since this type of data may look like a raster, it needs to be processed using vector methods. While doing the exercise, ask yourself questions like: Do I need my data to be vector or raster? What type of data is this? How do I process this data? 

## Data preparation
- Data cleanup
	- Why?
	- How?

### Data classification 
- Equal count

## Expressions
- Case



<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJUSm5Lc3l5V01vRlFneHl0Ijp7In
N0YXJ0IjoxNTA0LCJlbmQiOjE1MTksInRleHQiOiJFeGFtcGxl
IHBpY3R1cmUifSwiNXNSZ3c2RE5QZmJCSWNmaSI6eyJzdGFydC
I6MzI5NCwiZW5kIjozMzI3LCJ0ZXh0IjoiLSBFeGFtcGxlIHBp
Y3R1cmUgb2YgR0lTIGFuYWx5c2lzIn0sIndZT2pWYlBHQVZuS2
VldXEiOnsic3RhcnQiOjM3NjksImVuZCI6MzgwMiwidGV4dCI6
Ii0gRXhhbXBsZSBwaWN0dXJlIG9mIHRoaXMgZGF0YXNldCJ9LC
J4dTVKYTlteDhUVkNxT0tJIjp7InN0YXJ0IjozODA0LCJlbmQi
OjUxMTYsInRleHQiOiJXZSBsZWFybmVkIHByZXZpb3VzbHkgdG
hhdCByYXN0ZXIgZGF0YSBjb25zaXN0cyBvZiBhIGNvbnRpbnVv
dXMgc3VyZmFjZSBkaXZpZGVk4oCmIn19LCJjb21tZW50cyI6ey
JmVU5VcFFDYWszRkNrNVo3Ijp7ImRpc2N1c3Npb25JZCI6IlRK
bktzeXlXTW9GUWd4eXQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODY2MzY1
NDY0MjJ9LCJmTENIZnMwVmR3eDFxRFVXIjp7ImRpc2N1c3Npb2
5JZCI6IjVzUmd3NkROUGZiQkljZmkiLCJzdWIiOiJnaDo0MDMw
NDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOj
E2ODY2MzY3NzI1OTB9LCJPVmVDUG5PVVhkSXFNT1hnIjp7ImRp
c2N1c3Npb25JZCI6IndZT2pWYlBHQVZuS2VldXEiLCJzdWIiOi
JnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNy
ZWF0ZWQiOjE2ODY2MzgyNTc2ODh9LCJVOWt4eHlQUTE2UFE1Vn
d3Ijp7ImRpc2N1c3Npb25JZCI6Inh1NUphOW14OFRWQ3FPS0ki
LCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDaGVjayBmb3
IgYWNjdXJhY3kiLCJjcmVhdGVkIjoxNjg2NjM4MjY1NjAxfX0s
Imhpc3RvcnkiOlstMTc1NDg1MTczLDEzMzIzNzQ5NDgsLTE3MD
UyNTg5MjcsLTE1NDM1MDUwMTVdfQ==
-->