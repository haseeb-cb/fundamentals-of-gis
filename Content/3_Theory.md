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

1.  **Data Quality**: Data may have errors, inconsistencies, or missing values that can impact the reliability of analysis results. Data preparation involves identifying and correcting errors, resolving inconsistencies, and filling in missing values to enhance data quality and integrity.
    
2.  **Data Format and Compatibility**: GIS software typically has specific requirements regarding data formats, coordinate systems, and attribute tables. Data preparation involves converting data from different formats (such as CSV, Excel, or shapefiles) into a format compatible with GIS software. It also involves ensuring that spatial data aligns with the appropriate coordinate system to maintain spatial accuracy and enable meaningful analysis.
    
3.  **Data Integration**: GIS analysis often involves combining multiple datasets from different sources to gain a comprehensive understanding of a spatial phenomenon. Data preparation includes integrating different datasets, resolving inconsistencies in attribute fields, and establishing proper relationships between spatial and non-spatial data to facilitate effective analysis and interpretation.
    
4.  **Data Standardization**: Datasets collected from various sources may use different terminologies, classifications, or scales. Data preparation involves standardizing and harmonizing datasets to ensure consistency in attribute values, classifications, and spatial units. This standardization allows for meaningful comparisons and analysis across different spatial areas and time periods.
    
5.  **Data Aggregation or Disaggregation**: Depending on the scale of analysis or the research question at hand, it may be necessary to aggregate or disaggregate data to match the desired spatial resolution. Aggregating data involves combining smaller spatial units into larger ones, while disaggregating data involves splitting larger spatial units into smaller ones. Data preparation ensures that the data is appropriately aggregated or disaggregated for the specific analysis requirements.
    
6.  **Data Cleaning and Filtering**: Data preparation involves cleaning and filtering out irrelevant or redundant data to focus on the variables and geographic areas of interest. This process helps streamline the analysis and improve computational efficiency.

### How? 
In our case we will be using expressions to select the data we want, the entries where our selected fields don't contain -1, and export them into a new file. There are other ways of data preparation, here are the typical processes involved in preparing data for GIS analysis: 

1.  **Data Collection**: Identify and gather relevant data from various sources, such as government agencies, surveys, satellite imagery, or field surveys.
    
2.  **Data Cleaning**: Review the data for errors, inconsistencies, or missing values. Correct any inaccuracies, resolve inconsistencies, and fill in missing values through data validation, data cleansing techniques, and interpolation methods.
    
3.  **Coordinate System Alignment**: Ensure that all spatial datasets have consistent coordinate systems. If necessary, transform or project the data to a common coordinate system that matches the analysis requirements and the target GIS software.
    
4.  **Data Format Conversion**: Convert data from different formats (e.g., CSV, Excel, shapefiles) into a format compatible with the GIS software being used. This may involve using conversion tools or import/export functions provided by the GIS software.
    
5.  **Attribute Table Management**: Review and organize attribute tables associated with spatial data. Check for consistency in attribute field names, data types, and values. Rename fields, modify data types, and perform necessary calculations to create new attributes if required.
    
6.  **Spatial Join and Integration**: If multiple datasets are being used, spatially join or integrate them based on common spatial identifiers or geographic boundaries. This allows for the combination of data from different sources into a single dataset.
    
7.  **Standardization**: Standardize attribute values, classifications, and spatial units to ensure consistency across datasets. This may involve reclassifying variables, harmonizing terminology, or aggregating data to a consistent spatial resolution.
    
8.  **Data Filtering and Selection**: Filter out irrelevant or redundant data based on the specific analysis requirements. Select the variables and geographic areas of interest to focus the analysis on the desired subset of data.
    
9.  **Data Validation**: Verify the quality and integrity of the prepared data through visual inspection, statistical analysis, or comparison with reference data. Ensure that the prepared data meets the intended objectives of the GIS analysis.

## Data classification 
Data classification refers to **the process of categorizing or grouping data based on common characteristics, attributes, or criteria**. It involves organizing data into distinct classes or categories to facilitate analysis, interpretation, and communication of information.

In the context of GIS (Geographic Information System), data classification is often applied to spatial data, such as maps or remote sensing imagery. It helps to visually represent and differentiate features or phenomena on a map based on their attributes or values.

There are several methods of data classification, including:

1.  **Equal Count (Quantile)**: Divides the data into equal-sized groups, ensuring an equal number of data points in each group. Useful for reducing the impact of outliers.

2.  **Equal Interval**: Divides the data range into equal intervals. Suitable for data with a uniform distribution.

3. **Logarithmic Scale**: Utilizes a logarithmic transformation of data values to create classes. This method is often used when the data spans a wide range of values, and a logarithmic scale helps to represent the data more evenly and reveal patterns in both small and large values.

4.  **Natural Breaks (Jenks)**: Identifies natural groupings in the data by minimizing the differences within groups and maximizing the differences between groups. Often produces visually distinct and meaningful classes.

5. **Pretty Breaks**: Pretty breaks is a classification method that aims to create visually appealing and easily interpretable class intervals. It selects intervals based on "nice" or "pretty" numbers, such as multiples of 1, 2, or 5. This approach enhances the readability of maps and charts by using intervals that are more intuitive to the human eye.

6.  **Standard Deviation**: Uses the mean and standard deviation to classify data into classes based on a specified number of standard deviations above and below the mean.
    

The choice of classification method depends on the nature of the data, the research question or objective, and the desired visualization or analysis outcomes. The classification method can significantly influence the interpretation and understanding of the data, so it is important to select an appropriate method that best represents the underlying patterns or characteristics in the dataset.

Data classification is an essential step in data analysis, as it enables the visualization and exploration of data patterns, trends, and distributions. It supports the identification of spatial relationships, the comparison of different areas or groups, and the communication of information in a more accessible and meaningful manner.


## Expressions

In GIS, expressions refer to a set of rules or formulas that are used to perform calculations, evaluations, or manipulations on geographic data. They allow users to create customized calculations, queries, or transformations based on specific criteria or conditions.

Expressions in GIS are typically written using a combination of functions, operators, and variables that operate on attribute data associated with spatial features or on the spatial properties of the features themselves. They can be used in various contexts, including data analysis, data visualization, labeling, symbology, and data manipulation.

These are some common examples of how expressions are used in GIS:

1.  Attribute Calculations: Expressions can be used to calculate new attribute values based on mathematical operations, conditional statements, or combinations of existing attribute values. For instance, an expression can calculate population density by dividing the population attribute by the area attribute of each feature.
    
2.  Spatial Queries: Expressions can be used to query and filter spatial data based on specific criteria. For example, an expression can select all features within a certain distance of a particular point or within a specific land use category.
    
3.  Data Manipulation: Expressions can be used to manipulate and transform data. They can convert data types, concatenate strings, extract substrings, perform spatial transformations, or conduct spatial analyses.

For this exercise, we will be cleaning up the data by selecting the entries we want, calculating proportions, and reclassifying the data to quantiles using expressions. One of the expressions you will be using is as follows:

![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/3_Exercise/3_Exercise_reclassification.png)

What do you think is the purpose of this expression?


# Time to get your hands dirty! Move on to the 3rd exercise to apply this new knowledge.


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
dG9rYW7igKYifSwiY0pneGp2WklBMnI3WUJzbCI6eyJzdGFydC
I6MzMyOSwiZW5kIjozMzg1LCJ0ZXh0IjoiLSBFeGFtcGxlcyBv
ZiBHSVMgc29jaW8tc3BhdGlhbCBkaWZmZXJlbnRpYXRpb24gYW
5hbHlzZXMifSwibzlmMmN5WG1yZDZOWTRUZiI6eyJzdGFydCI6
MTI1NTEsImVuZCI6MTMzMDUsInRleHQiOiIxLiAgKipFcXVhbC
BJbnRlcnZhbCoqOiBEaXZpZGVzIHRoZSBkYXRhIHJhbmdlIGlu
dG8gZXF1YWwgaW50ZXJ2YWxzLiBTdWl0YWJsZSBm4oCmIn19LC
Jjb21tZW50cyI6eyJmVU5VcFFDYWszRkNrNVo3Ijp7ImRpc2N1
c3Npb25JZCI6IlRKbktzeXlXTW9GUWd4eXQiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0
ZWQiOjE2ODY2MzY1NDY0MjJ9LCJmTENIZnMwVmR3eDFxRFVXIj
p7ImRpc2N1c3Npb25JZCI6IjVzUmd3NkROUGZiQkljZmkiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZS
IsImNyZWF0ZWQiOjE2ODY2MzY3NzI1OTB9LCJPVmVDUG5PVVhk
SXFNT1hnIjp7ImRpc2N1c3Npb25JZCI6IndZT2pWYlBHQVZuS2
VldXEiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQg
cGljdHVyZSIsImNyZWF0ZWQiOjE2ODY2MzgyNTc2ODh9LCJVOW
t4eHlQUTE2UFE1Vnd3Ijp7ImRpc2N1c3Npb25JZCI6Inh1NUph
OW14OFRWQ3FPS0kiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJDaGVjayBmb3IgYWNjdXJhY3kiLCJjcmVhdGVkIjoxNjg2
NjM4MjY1NjAxfSwiRmsxaUY5NW03MmIwYmJDbCI6eyJkaXNjdX
NzaW9uSWQiOiJKTDA4Wk85bWQxZ3Z0bTU1Iiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiQ2hlY2sgaWYgb3BlbiIsImNyZW
F0ZWQiOjE2ODY2Mzg0MzM5MjF9LCJaWk9CU0FKRFhobXZPaURF
Ijp7ImRpc2N1c3Npb25JZCI6ImNKZ3hqdlpJQTJyN1lCc2wiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgbGlua3Mi
LCJjcmVhdGVkIjoxNjg2NjM5MzMxNTc0fSwienRuUUJYd09EMl
BXbnNpTCI6eyJkaXNjdXNzaW9uSWQiOiJvOWYyY3lYbXJkNk5Z
NFRmIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiZGlhZ3
JhbSIsImNyZWF0ZWQiOjE2ODY2NDA5MjkxODV9fSwiaGlzdG9y
eSI6WzE4MTk2MTc3MDAsMjA4Mzk5Mzk4NiwtMTc1NDg1MTczLD
EzMzIzNzQ5NDgsLTE3MDUyNTg5MjcsLTE1NDM1MDUwMTVdfQ==

-->