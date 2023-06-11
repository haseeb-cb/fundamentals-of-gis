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
Work individually or in pairs and make map(s) and write a short reflection (200-300 words). The following
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
		- How are the different phenomena located in the Helsinki metropolitan region? Where are the biggest clusters?
		- Can you find any surprising results?
		- Are income and education level data sufficient variables to study segregation?
		- If not, what other variables would you need?
	- Write how your workflow went, which part was hard and which was easy.
	- It’s not needed to write click by click how you did it.
7. Return your exercise reflection to the course Moodle.

## EXERCISE PHASES

### Getting familiar with the data

1. Download, unzip and open the exercise 3 data in QGIS from the course Moodle page.

2. **Go through the attribute table and use the pdf-files to decipher the meanings of each field**. The attribute table consists of a few themes (recognizable by the prefixes) and slightly over 100 fields.
	- The fields we’re using depict the following:
		- ko_perus (Inhabitants with no qualification after basic-level studies, education theme’s prefix ko_)
		- hr_pi_tul (Inhabitants belonging to the lowest income category, Inhabitants’ income theme’s prefix hr_)
		- Under each theme, eg. education (prefix ko_) the first field has the total value of each grid cell (feature) in that field. We’ll need these total fields in the analysis:
			- Level of education: ko_ika18y (Total number of people in grid cell, aged 18 or over)
			- Level of income: hr_tuy (Total number of people in grid cell, aged 18 or over)
			Note: ko_ika18y and hr_tuy both contain the same values. However, for clarity you might want to use the one with the same prefix as the one you are comparing it to.
	- Background map.
		- You can use for example QuickMapServices, the spatial data from the Crash Course’s General-folder or find your own data.
		- Tip: Remember that if you first bring in your data (from the practical folder), the background map should project automatically to the right coordinate system.

--- 

### Cleaning up the data

3. As you browsed the attribute table of the data, you might’ve noticed that **some fields have
the value -1 for data privacy protection law. You’ll have to clean up the data** and there are a few
ways to do this. Here we’re focusing on selections.
	- -1 is a placeholder value for NoData or NotAvailable and not an actual value. It does not mean that there are actually -1 people in the cell...
	- The Basic-level studies field (ko_perus) depicts the amount of people whose highest achieved level of education is basic-level studies. It has values of -1 for those grids that have less than 10 people over 18 years old (ko_ika18y).
	- And same thing for the low-income variables hr_pi_tul and hr_tuy.

4. **You could use select by expression** to select the features that have values in the two wanted fields (ko_perus, hr_pi_tul) that are 0 or greater AND have people living in them (ko_ika18y, hr_tuy):
	- To open the expression window press
	- After the selection, save the selected features as a new shapefile (Right click layer with selection > *Export* > *Save selected features as…*).

	*Tip: If you are confused with the formula, try reading it aloud: “Select the features where X is greater than 0 AND Y is greater or equal than 0, AND…”*

5. **You should end up with a new layer without any -1 values in the four wanted fields.**

---

### Calculating the proportions

6. **In the newly created layer, use the field calculator to calculate new fields for the proportions
(percentages)**
	- Calculate the proportions of the wanted fields (Basic education, low-income inhabitants etc.)
		- Make sure to use the correct variables when calculating. Use the total number field of each theme in the calculation.
			- Level of education: ko_ika18y (Aged 18 or over, total)
			- Level of income: hr_tuy (Aged 18 or over, total)
		- For example: to calculate the share of residents with only a basic-level studies in grid cells: (ko_perus / ko_ika18y) * 100 (Studied value divided by total value gives the share, *100 makes the result as %)
		- Make sure the field type is set to decimal numbers and make the values have at least 2 decimal numbers (precision).
		- Name the fields accordingly. Note: Shapefile allows only 10 characters in the field name.

7. **You should end up with two new fields that all have percentage values.**

--- 

### Quantiles and reclassification

8. **Our newly created proportion fields are tempting, but let’s take it to the next level with
quantiles**
	- In the Symbology-tab and under the Graduated symbols you can find different classification methods.
	- When classifying data with Equal Count as the classification method and setting the number of classes to four, each class is called a quartile.
		- Thus, each class has the same number of entries (hence equal count)

9. **We’re going to have to utilize QGIS’s visualization tools to find out the class boundaries for
quantiles within QGIS.** You could also use any statistical analysis application (Excel, LibreCalc,
SPSS etc.) to find out the boundaries.
	- So, open the style tab of the layer, select graduated, select the correct field
		- E.g., Basic-level education proportion
	-  Switch mode to *Quantiles (Equal Count)* and drop the number of classes from 5 down to 4. Click *Classify*
		- Make notes about the class boundaries because you’re going to use them soon. For Basic-level education they look something like this:
		- Do the same for the remaining proportion field (level of income percentage) and make notes about the class boundaries for that field as well.

10. **Now that we have the boundaries for the two classifications, it’s time to reclassify the data
into four classes.**
		- Open the attribute table and field calculator, we’re creating new fields for the reclassified values using a slightly more complex conditional statement this time. Note! Do all the analyses in the same layer so that you get the new columns in the same layer.
		- The logic behind the numbering of the classes should be the same across all the reclassifications. In this instance our logic can be as follows: class 1 is the lowest (e.g. lowest share of inhabitants with no qualification after basic-level studies) and class 4 is the highest quartile (e.g. highest share of inhabitants with no qualification after basiclevel studies).

 



<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJlVGM4YW9CSm43emRyZjBrIjp7In
N0YXJ0IjoyNTEsImVuZCI6MjU5LCJ0ZXh0IjoiSGVsc2lua2ki
fSwiUVAxWENiQ3BSc2QwbFZxNSI6eyJzdGFydCI6MTIzNCwiZW
5kIjoxMjQyLCJ0ZXh0IjoiSGVsc2lua2kifSwiV3Z6bnlmS0xY
dm5sRURpNCI6eyJzdGFydCI6MTc3NywiZW5kIjoxNzg5LCJ0ZX
h0IjoicGRmIGluY2x1ZGVkIn0sIkJ3ZFRwa3lIblpFQmNOclgi
Onsic3RhcnQiOjMzNjEsImVuZCI6MzM3MCwidGV4dCI6InBkZi
1maWxlcyJ9LCI1dUhCTVNsNU1TbVpicFZqIjp7InN0YXJ0Ijoz
MjI3LCJlbmQiOjMzMTEsInRleHQiOiIxLiBEb3dubG9hZCwgdW
56aXAgYW5kIG9wZW4gdGhlIGV4ZXJjaXNlIDMgZGF0YSBpbiBR
R0lTIGZyb20gdGhlIGNvdXJzZSBNb29kbGXigKYifSwiMnRTWG
x6M095cmpWSHZGaiI6eyJzdGFydCI6NDMxOCwiZW5kIjo0NDQw
LCJ0ZXh0IjoiLSBZb3UgY2FuIHVzZSBmb3IgZXhhbXBsZSBRdW
lja01hcFNlcnZpY2VzLCB0aGUgc3BhdGlhbCBkYXRhIGZyb20g
dGhlIENyYXNoIENvdeKApiJ9LCJEdmdmcEpzZnZ3Y05mOGlWIj
p7InN0YXJ0Ijo1MzQwLCJlbmQiOjU1NDIsInRleHQiOiI0LiBZ
b3UgY291bGQgdXNlIHNlbGVjdCBieSBleHByZXNzaW9uIHRvIH
NlbGVjdCB0aGUgZmVhdHVyZXMgdGhhdCBoYXZlIHZhbHVlcyBp
4oCmIn0sIlJpYktXVTFRQzdyWkNCWDUiOnsic3RhcnQiOjU1Nz
YsImVuZCI6NTU4MSwidGV4dCI6InByZXNzIn0sIktmMzRvY21p
TEI5NXg5MksiOnsic3RhcnQiOjExNzQsImVuZCI6MTE4NCwidG
V4dCI6Ik9CSkVDVElWRVMifSwiVGtMaXM5UmZ3UzJKeW03bCI6
eyJzdGFydCI6NjAxNywiZW5kIjo2MTM0LCJ0ZXh0IjoiNi4gKi
pJbiB0aGUgbmV3bHkgY3JlYXRlZCBsYXllciwgdXNlIHRoZSBm
aWVsZCBjYWxjdWxhdG9yIHRvIGNhbGN1bGF0ZSBuZXcgZmllbO
KApiJ9LCIyZHdDOWZ0bHVJRVdUQllWIjp7InN0YXJ0Ijo3Njg3
LCJlbmQiOjc3NjgsInRleHQiOiItIFNvLCBvcGVuIHRoZSBzdH
lsZSB0YWIgb2YgdGhlIGxheWVyLCBzZWxlY3QgZ3JhZHVhdGVk
LCBzZWxlY3QgdGhlIGNvcnJlY3QgZmll4oCmIn0sIkdMcEFRdk
4xczNRSHZSSTQiOnsic3RhcnQiOjgwMDQsImVuZCI6ODA2MCwi
dGV4dCI6IkZvciBCYXNpYy1sZXZlbCBlZHVjYXRpb24gdGhleS
Bsb29rIHNvbWV0aGluZyBsaWtlIHRoaXM6In19LCJjb21tZW50
cyI6eyIzTG9HS2VRRkVNV3pqYkUxIjp7ImRpc2N1c3Npb25JZC
I6ImVUYzhhb0JKbjd6ZHJmMGsiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJVcGRhdGUgaWYgYXBwbGljYWJsZSIsImNyZW
F0ZWQiOjE2ODY0NzY0MzY4Nzh9LCJsUGtsVUZiRTRlVTIwMzRa
Ijp7ImRpc2N1c3Npb25JZCI6IlFQMVhDYkNwUnNkMGxWcTUiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJVcGRhdGUgaWYg
YXBwbGljYWJsZSIsImNyZWF0ZWQiOjE2ODY0NzY1Nzk1Njd9LC
JCdUJGbWlqR2lyakVjNVVrIjp7ImRpc2N1c3Npb25JZCI6Ild2
em55ZktMWHZubEVEaTQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsIn
RleHQiOiJBZGQgcGFnZSIsImNyZWF0ZWQiOjE2ODY0NzY3MzYw
NTV9LCJQS0JhSlphM2Rtd2xWcUY1Ijp7ImRpc2N1c3Npb25JZC
I6IkJ3ZFRwa3lIblpFQmNOclgiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJSZWZlcmVuY2UiLCJjcmVhdGVkIjoxNjg2ND
c3NDc1ODg4fSwidzdFVlMyeE1QelJjSUNMZiI6eyJkaXNjdXNz
aW9uSWQiOiI1dUhCTVNsNU1TbVpicFZqIiwic3ViIjoiZ2g6ND
AzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGluc3RydWN0aW9ucyB0byBk
b3dubG9hZCBkYXRhIHRoZW1zZWx2ZXMiLCJjcmVhdGVkIjoxNj
g2NDc3NDk0MTIwfSwiMjNjRUtkNW1lM2NFbElGNSI6eyJkaXNj
dXNzaW9uSWQiOiIydFNYbHozT3lyalZIdkZqIiwic3ViIjoiZ2
g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIGluc3RydWN0aW9ucyBv
biBob3cgdG8gdXNlIHRoaXMiLCJjcmVhdGVkIjoxNjg2NDc3NT
Q5NzkxfSwiUXQxa3Q3V2hQQWtWQW14RCI6eyJkaXNjdXNzaW9u
SWQiOiJEdmdmcEpzZnZ3Y05mOGlWIiwic3ViIjoiZ2g6NDAzMD
Q3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUgb2YgZXhwcmVzc2lv
biIsImNyZWF0ZWQiOjE2ODY0NzgzMDM4ODd9LCJacjJLWnFUUl
dwcWo2U05UIjp7ImRpc2N1c3Npb25JZCI6IlJpYktXVTFRQzdy
WkNCWDUiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZG
QgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODY0Nzg1OTU0NTR9LCJ6
aU5QRnNObjJhM3JsWEpCIjp7ImRpc2N1c3Npb25JZCI6IktmMz
RvY21pTEI5NXg5MksiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRl
eHQiOiJVcGRhdGUgd2l0aCBwb3NpdGlvbiBpbiBjb3Vyc2UiLC
JjcmVhdGVkIjoxNjg2NDc5NDY5NjU1fSwiY1ZGTEZWd2VEVnI2
ZXp5NiI6eyJkaXNjdXNzaW9uSWQiOiJUa0xpczlSZndTMkp5bT
dsIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVG9vIGxp
dHRsZSBpbnN0cnVjdGlvbnMgZm9yIHRoaXMgc3RhZ2Ugb2YgdG
hlIGNvdXJzZT8iLCJjcmVhdGVkIjoxNjg2NDc5NTkyNDYxfSwi
VHFpMndBdlVoaVVJTlhRMCI6eyJkaXNjdXNzaW9uSWQiOiIyZH
dDOWZ0bHVJRVdUQllWIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiVG9vIGxpdHRsZSBpbnN0cnVjdGlvbnMgZm9yIHRoaX
Mgc3RhZ2Ugb2YgdGhlIGNvdXJzZT8iLCJjcmVhdGVkIjoxNjg2
NDc5NzU4MTM2fSwiSnRuZDBtQWVyY1VhSzZpUyI6eyJkaXNjdX
NzaW9uSWQiOiJHTHBBUXZOMXMzUUh2Ukk0Iiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdG
VkIjoxNjg2NDc5ODM4MzY3fX0sImhpc3RvcnkiOlsxNjUzMDc3
Mjg5LC0xMzExNTI5NDA1LDUxNjIxMzI0OCwtMTcyNTc3MjE2MS
wxNjc3MDI5MTUxLC0xMzMyMDg3OTYzXX0=
-->