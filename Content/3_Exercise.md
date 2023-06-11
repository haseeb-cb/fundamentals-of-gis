### Fundamentals of Geographic Information Systems (GIS)

# Exercise 3: Socio-spatial differentiation & social segregation

## OVERVIEW & PURPOSE
Today’s theme is socio-spatial differentiation & social segregation and we’re going to be looking at the
Helsinki metropolitan area’s population dynamics.  One of the key components of the city is as Shakespeare so eloquently put in Coriolanus “What is the city, but the people?”

Socio-economic features of the inhabitants of the city vary across geographical space and across time.
Today we are using the Statistics Finland’s Grid Database 2016 about the social structure in 250x250m
grid cells. Our task today is to study socio-spatial differentiation and pinpoint low-education and low-income
grid cells. This could also be an interesting starting point for the analysis if we study segregation
in the region.

To do this, the data needs some clean-up, some fields need to be calculated and the lowest quartiles for
different variables (income, education) have to be found. You will be learning to use the conditional statement
functionality. The results are once again to be visualized on a map and to be
reflected on.

## OBJECTIVES
1. Examining the socio-economic structure of the Helsinki Metropolitan Region and pinpointing the
areas with the lowest educational & income level on a map
2. Familiarizing yourself with using expressions and conditional statements
	- Using more complex expressions
	- Using conditional statements to reclassify field values

## DATA USED/NEEDED

1. Statistics Finland’s Grid Database 2016
	- Our data set covers the area of the Helsinki metropolitan region.
	- See: http://www.stat.fi/tup/ruututietokanta/index_en.html
	- The attribute table’s field names are in Finnish, but there’s a pdf included in the course
data with the translations, explanations for the field names and longer descriptions (in
English, Finnish, and Swedish).

## COMPLETION

## EXERCISE PHASES


<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJlVGM4YW9CSm43emRyZjBrIjp7In
N0YXJ0IjoyNTEsImVuZCI6MjU5LCJ0ZXh0IjoiSGVsc2lua2ki
fSwiUVAxWENiQ3BSc2QwbFZxNSI6eyJzdGFydCI6MTIzNCwiZW
5kIjoxMjQyLCJ0ZXh0IjoiSGVsc2lua2kifX0sImNvbW1lbnRz
Ijp7IjNMb0dLZVFGRU1XempiRTEiOnsiZGlzY3Vzc2lvbklkIj
oiZVRjOGFvQkpuN3pkcmYwayIsInN1YiI6ImdoOjQwMzA0Nzg4
IiwidGV4dCI6IlVwZGF0ZSBpZiBhcHBsaWNhYmxlIiwiY3JlYX
RlZCI6MTY4NjQ3NjQzNjg3OH0sImxQa2xVRmJFNGVVMjAzNFoi
OnsiZGlzY3Vzc2lvbklkIjoiUVAxWENiQ3BSc2QwbFZxNSIsIn
N1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlVwZGF0ZSBpZiBh
cHBsaWNhYmxlIiwiY3JlYXRlZCI6MTY4NjQ3NjU3OTU2N319LC
JoaXN0b3J5IjpbMTUyMjY5MDY5MV19
-->