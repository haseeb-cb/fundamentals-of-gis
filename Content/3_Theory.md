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

- Examples of GIS socio-spatial differentiation analyses

## Dataset
The exercise accompanying this theory section consists of a GIS socio-spatial differentiation analysis. We will be using the Statistics Finland's Grid Database, which as the name suggests consists of a grid of cells, each of which describes various statistics of the area it covers. In this exercise specifically we will be looking at a 250x250m scale at the spatial distribution of level of education and income in Helsinki. 

You can access the dataset here: https://www.tilastokeskus.fi/tup/ruututietokanta/index_en.html

- Example picture of this dataset

We learned previously that raster data consists of a continuous surface divided into a grid of cells, where each cell corresponds to a specific location and contains a value representing a particular attribute. This value is represented by the color of the cell, images are in a way rasters as well, specifically JPEG, PNG, and GIF images. Do you remember seeing in movies that they store data in pictures? This is not unrealistic, as you could just see pictures as a raster where the color of each cell represents its value. One limitation of rasters however, is that a cell can only hold 1 value , since the cell can also only be 1 color. This is sufficient for a lot of cases, for example a raster which describes the slope of the area only needs one value per cell, the slope. But if we want to use multiple values in a raster, such as statistics of the cells, we need to make use of a grid in a vector format. This is the case in the Statistics Finland's Grid Database, as you will see when you do the exercise. This is important to keep in mind in the future, since this type of data may look like a raster, it needs to be processed using vector methods. While doing the exercise, ask yourself questions like: Do I need my data to be vector or raster? What type of data is this? How do I process this data? 

## Data preparation

### Why?
A regular necessary step in GIS is to prepare data for our analysis, the same can be said for this analysis. As you will see in the data during the exercise, some of the values are -1, which can't be true when we're talking about the statistics of people within an area. -1 in this dataset stands for no data available, which can be for several reasons, but in this case is due to privacy measures. If an area covered by a cell has a very small population, it would be very easy to identify which statistics correspond to which individual. For this reason, grids that have less than 10 inhabitants have been specifically removed from the available dataset to prevent privacy violations. 

But what happens if we do an analysis without excluding these -1 values? This depends on the analysis of course, but in this case the analysis would be flawed. We will be looking at value ranges, and these would be incorrect if the starting value would be -1. Don't worry much about this for now however, it will make more sense after the exercise.  But ask yourself the question at the end of the exercise, what effect would it have had if I didn't exclude the -1 values

There are other reasons why we might need to prepare the data, such as: 

1.  Data Quality: Data may have errors, inconsistencies, or missing values that can impact the reliability of analysis results. Data preparation involves identifying and correcting errors, resolving inconsistencies, and filling in missing values to enhance data quality and integrity.
    
2.  Data Format and Compatibility: GIS software typically has specific requirements regarding data formats, coordinate systems, and attribute tables. Data preparation involves converting data from different formats (such as CSV, Excel, or shapefiles) into a format compatible with GIS software. It also involves ensuring that spatial data aligns with the appropriate coordinate system to maintain spatial accuracy and enable meaningful analysis.
    
3.  Data Integration: GIS analysis often involves combining multiple datasets from different sources to gain a comprehensive understanding of a spatial phenomenon. Data preparation includes integrating different datasets, resolving inconsistencies in attribute fields, and establishing proper relationships between spatial and non-spatial data to facilitate effective analysis and interpretation.
    
4.  Data Standardization: Datasets collected from various sources may use different terminologies, classifications, or scales. Data preparation involves standardizing and harmonizing datasets to ensure consistency in attribute values, classifications, and spatial units. This standardization allows for meaningful comparisons and analysis across different spatial areas and time periods.
    
5.  Data Aggregation or Disaggregation: Depending on the scale of analysis or the research question at hand, it may be necessary to aggregate or disaggregate data to match the desired spatial resolution. Aggregating data involves combining smaller spatial units into larger ones, while disaggregating data involves splitting larger spatial units into smaller ones. Data preparation ensures that the data is appropriately aggregated or disaggregated for the specific analysis requirements.
    
6.  Data Cleaning and Filtering: Data preparation involves cleaning and filtering out irrelevant or redundant data to focus on the variables and geographic areas of interest. This process helps streamline the analysis and improve computational efficiency.

### How? 

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
VldXEiOnsic3RhcnQiOjM5MjMsImVuZCI6Mzk1NiwidGV4dCI6
Ii0gRXhhbXBsZSBwaWN0dXJlIG9mIHRoaXMgZGF0YXNldCJ9LC
J4dTVKYTlteDhUVkNxT0tJIjp7InN0YXJ0IjozOTU4LCJlbmQi
OjUyNzAsInRleHQiOiJXZSBsZWFybmVkIHByZXZpb3VzbHkgdG
hhdCByYXN0ZXIgZGF0YSBjb25zaXN0cyBvZiBhIGNvbnRpbnVv
dXMgc3VyZmFjZSBkaXZpZGVk4oCmIn0sIkpMMDhaTzltZDFndn
RtNTUiOnsic3RhcnQiOjM4MjYsImVuZCI6MzkyMSwidGV4dCI6
IllvdSBjYW4gYWNjZXNzIHRoZSBkYXRhc2V0IGhlcmU6IGh0dH
BzOi8vd3d3LnRpbGFzdG9rZXNrdXMuZmkvdHVwL3J1dXR1dGll
dG9rYW7igKYifX0sImNvbW1lbnRzIjp7ImZVTlVwUUNhazNGQ2
s1WjciOnsiZGlzY3Vzc2lvbklkIjoiVEpuS3N5eVdNb0ZRZ3h5
dCIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaW
N0dXJlIiwiY3JlYXRlZCI6MTY4NjYzNjU0NjQyMn0sImZMQ0hm
czBWZHd4MXFEVVciOnsiZGlzY3Vzc2lvbklkIjoiNXNSZ3c2RE
5QZmJCSWNmaSIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6
IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NjYzNjc3MjU5MH
0sIk9WZUNQbk9VWGRJcU1PWGciOnsiZGlzY3Vzc2lvbklkIjoi
d1lPalZiUEdBVm5LZWV1cSIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6MTY4NjYz
ODI1NzY4OH0sIlU5a3h4eVBRMTZQUTVWd3ciOnsiZGlzY3Vzc2
lvbklkIjoieHU1SmE5bXg4VFZDcU9LSSIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6IkNoZWNrIGZvciBhY2N1cmFjeSIsIm
NyZWF0ZWQiOjE2ODY2MzgyNjU2MDF9LCJGazFpRjk1bTcyYjBi
YkNsIjp7ImRpc2N1c3Npb25JZCI6IkpMMDhaTzltZDFndnRtNT
UiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJDaGVjayBp
ZiBvcGVuIiwiY3JlYXRlZCI6MTY4NjYzODQzMzkyMX19LCJoaX
N0b3J5IjpbLTk3OTc1NjAzOCwtMTc1NDg1MTczLDEzMzIzNzQ5
NDgsLTE3MDUyNTg5MjcsLTE1NDM1MDUwMTVdfQ==
-->