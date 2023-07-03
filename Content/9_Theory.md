### Fundamentals of Geographic Information Systems (GIS)

# Theory 9: Public Participation GIS and Directional Distribution

## Public Participation GIS (PPGIS)/SoftGIS
Public Participation GIS, often referred to as PPGIS, is a participatory approach that combines GIS with public involvement in decision-making processes. It aims to engage citizens and stakeholders in mapping and analyzing spatial information to better understand and address local issues.

PPGIS facilitates the collection, visualization, and analysis of geospatial data by involving community members in data collection, interpretation, and decision-making. It recognizes that local knowledge and lived experiences are valuable sources of information that can contribute to a more comprehensive understanding of an area and its challenges.

SoftGIS is a specific implementation of PPGIS that focuses on user-friendly software tools for data collection and analysis. It provides accessible platforms and interfaces that allow individuals with varying levels of technical expertise to participate in mapping activities. SoftGIS tools often include web-based or mobile applications that enable community members to contribute geospatial data, such as points of interest, spatial boundaries, or qualitative information, through surveys, interviews, or other data collection methods.

The collected data can be used for various purposes, such as urban planning, environmental management, social impact assessments, or community development initiatives. By involving the public in the GIS process, PPGIS/SoftGIS fosters collaboration, empowers local communities, and enhances the quality and relevance of decision-making processes.

### PPGIS/SoftGIS tools
There are several PPGIS/SoftGIS tools that have been developed to facilitate public participation in spatial data collection and analysis, but only few are freely available. A good example of a this is **Epicollect5**, an open mobile data-gathering platform developed by the University of Oxford. It was originally developed to track diseases, but is now freely available to anyone that wants to conduct surveys with location data. Especially worth checking out if you want to conduct some kind of survey with geographical data: https://five.epicollect.net/. Another open-source application is Ushahidi: https://www.ushahidi.com/

Alternatively, there are also commercial tools like Mappler, CommunityViz, and ArcGIS Survey123, which are also commonly used.

## Directional Distribution
Directional distribution refers to the analysis and representation of the spatial pattern or arrangement of data points in relation to their directions or angles. It is commonly used to study phenomena that exhibit directional characteristics, such as wind patterns, animal migration routes, or road networks.

In directional distribution analysis, the focus is on understanding the concentration or dispersion of data points in different directions or sectors. This type of analysis can provide insights into the underlying processes or factors that influence the distribution pattern.

By analyzing the distribution of data points in different directions, researchers can identify dominant directions, assess symmetry or asymmetry in the distribution, determine clustering or dispersion patterns, and explore potential relationships between the directional distribution and other variables.

Directional distribution analysis has applications in various fields, including meteorology, ecology, transportation planning, and geospatial analysis. It helps researchers and practitioners gain a better understanding of how phenomena are distributed in space and how directional factors may influence their patterns.

### Deviational Ellipses
We’ll create standard deviational ellipses to summarize the spatial characteristics of geographic features: central tendency, dispersion, and directional trends. 

Standard Deviation Ellipse shows the area where the majority of the features (here, possible wind power sites) are located. When the underlying spatial pattern of features is concentrated in the center with fewer features toward the periphery (a spatial normal distribution), a standard deviational ellipse polygon will cover approximately 68 percent of the features.

![](https://geol260.academic.wlu.edu/files/lecture_notes/standardellipse_stat.gif)

(Hungry for more? 
- http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-statistics-toolbox/directional-distribution.htm
- http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-statistics-toolbox/h-how-directional-distribution-standard-deviationa.htm)





<!--stackedit_data:
eyJoaXN0b3J5IjpbMjk3OTk5NTU2LDYzNTUxMTIxNiwtOTE5NT
YwOTQ1LDczMDk5ODExNl19
-->