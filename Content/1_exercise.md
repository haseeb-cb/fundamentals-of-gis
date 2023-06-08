### Fundamentals of Geographic Information Systems (GIS)

# Exercise 1: Introduction continuation



## Overview & purpose
Urban areas undergo continuous development, and maps need to be updated regularly to account for new construction, demolition, and land use changes for example. In this tutorial, the objective is to **edit a GIS layer to show urban development**. In this case, we will be looking at the development of the Nokia Arena in the city centre of Tampere, Finland. 

The learning objectives are:
- Understand vector data
- How to create and edit vector data
- How to georeference a picture
- How to project data in the right Coordinate Reference System

## Objectives

## Data used

## Completion

## Exercise phases
### Getting familiar with the data
It is good to be familiar with the area you will be working with in this exercise:
- https://en.wikipedia.org/wiki/Nokia_Arena_(Tampere)
- https://goo.gl/maps/MifgU6b51S6QKacf7

1. Save the downloaded GIS data in an empty folder for this exercise.
2. Open QGIS and load the tampere_buildings.shp, tampere_roads.shp, and tampere_railway.shp into QGIS (See Crash Course exercise 2.1), the project CRS will change to the CRS of these layers (ETS89/TM35FIN).
3. Add Google Satellite imagery: Navigate to your browser panel > expand XYZ Tiles > drag "Google Satellite" to you the layers panel (See Crash Course exercise 1.2).
4. Take a moment to examine the data you added now, what is it about? What kind of attributes does the data have?
	- Can you find the location of where the Nokia Arena is constructed? (hint: the coordinates are 328300 east, 6822050 north in the ETS89 / TM35FIN(E,N) coordinate system. Does the arena and new development exist in the tampere_buildings layer? What about in the Google satellite imagery?

	We have a vector layer with the buildings in central Tampere, and a vector layer showing the roads – both of which originally came from OpenStreetMap. This data is old – it shows the area before the development of the arena. In addition, we have a raster image file that shows the designs for the Arena, taken from a planning document. Unfortunately, this raster is not spatially referenced – there is no spatial information associated with each raster cell.

<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJXcmFjeFYwYVZSSlI0SUp5Ijp7In
N0YXJ0Ijo2NzMsImVuZCI6NjgzLCJ0ZXh0IjoiT2JqZWN0aXZl
cyJ9LCJBR0NsRE1hanRLVkZGZ0x6Ijp7InN0YXJ0Ijo2ODUsIm
VuZCI6Njk3LCJ0ZXh0IjoiIyMgRGF0YSB1c2VkIn0sIjB2TE9q
dlFUYVdYVHp2aUgiOnsic3RhcnQiOjY5OSwiZW5kIjo3MTIsIn
RleHQiOiIjIyBDb21wbGV0aW9uIn19LCJjb21tZW50cyI6eyJo
NzY0bVdIYjNKWTd1MU5NIjp7ImRpc2N1c3Npb25JZCI6IldyYW
N4VjBhVlJKUjRJSnkiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJDb21lIGJhY2sgdG8gdGhpcyBhZnRlciBmaW5pc2hpbm
cgdGhlIGV4ZXJjaXNlIHBoYXNlIiwiY3JlYXRlZCI6MTY4NjIw
MjMwMDA5MH0sIkFRaTZ1UFRJb1QyRzlDNVIiOnsiZGlzY3Vzc2
lvbklkIjoiQUdDbERNYWp0S1ZGRmdMeiIsInN1YiI6ImdoOjQw
MzA0Nzg4IiwidGV4dCI6IlNhbWUgYXMgYWJvdmUiLCJjcmVhdG
VkIjoxNjg2MjAyMzIxNDEwfSwiTjlBNjZHMGkyUVFVRUc2biI6
eyJkaXNjdXNzaW9uSWQiOiIwdkxPanZRVGFXWFR6dmlIIiwic3
ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiU2FtZSBhcyBhYm92
ZSIsImNyZWF0ZWQiOjE2ODYyMDIzMjk0ODJ9fSwiaGlzdG9yeS
I6Wzg2NTY0Mzc0NV19
-->