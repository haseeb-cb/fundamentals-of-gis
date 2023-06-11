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
Work individually or in pairs and make map(s) and write a short reflection (2-3 pages of text excluding images). The following
steps should be done:
1. Cleaning up the data of placeholder values for null/NoData entries.
	- Selecting the rows without null values in the wanted fields:
	
	- Inhabitants belonging to the lowest income category
	
	- Inhabitants with no qualification after basic-level studies
2. Calculation of proportions (percentages) of the variables above we need for the analysis
3. Re-classifying the proportions into 4 classes based upon quartiles
	- Using the field calculator and conditional statements
4. Finding the low-education and low-income grid cells
5. Creating a map (Remember to include the map in the report!)
6. Report:
	- Analyzing the results:
		- How are the different phenomena located in the Helsinki metropolitan region?
Where are the biggest clusters?
		- Can you find any surprising results?
		- Are income and education level data sufficient variables to study segregation?
		- If not, what other variables would you need?
	- Write how your workflow went, which part was hard and which was easy.
	- It’s not needed to write click by click how you did it.
7. Return your exercise report to the course Moodle in one week’s time (by next Wednesday).

## EXERCISE PHASES


<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJlVGM4YW9CSm43emRyZjBrIjp7In
N0YXJ0IjoyNTEsImVuZCI6MjU5LCJ0ZXh0IjoiSGVsc2lua2ki
fSwiUVAxWENiQ3BSc2QwbFZxNSI6eyJzdGFydCI6MTIzNCwiZW
5kIjoxMjQyLCJ0ZXh0IjoiSGVsc2lua2kifSwiV3Z6bnlmS0xY
dm5sRURpNCI6eyJzdGFydCI6MTc3NywiZW5kIjoxNzg5LCJ0ZX
h0IjoicGRmIGluY2x1ZGVkIn19LCJjb21tZW50cyI6eyIzTG9H
S2VRRkVNV3pqYkUxIjp7ImRpc2N1c3Npb25JZCI6ImVUYzhhb0
JKbjd6ZHJmMGsiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJVcGRhdGUgaWYgYXBwbGljYWJsZSIsImNyZWF0ZWQiOjE2OD
Y0NzY0MzY4Nzh9LCJsUGtsVUZiRTRlVTIwMzRaIjp7ImRpc2N1
c3Npb25JZCI6IlFQMVhDYkNwUnNkMGxWcTUiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJVcGRhdGUgaWYgYXBwbGljYWJs
ZSIsImNyZWF0ZWQiOjE2ODY0NzY1Nzk1Njd9LCJCdUJGbWlqR2
lyakVjNVVrIjp7ImRpc2N1c3Npb25JZCI6Ild2em55ZktMWHZu
bEVEaTQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZG
QgcGFnZSIsImNyZWF0ZWQiOjE2ODY0NzY3MzYwNTV9fSwiaGlz
dG9yeSI6Wy0xNjg0MTE0OTUxLC0xMzMyMDg3OTYzXX0=
-->