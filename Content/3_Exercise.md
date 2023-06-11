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
	- Let’s use the conditional statement first for basic-level education proportions. This is where you use the class boundary notes. The expression looks something like this:
	- NOTE: Use a dot as a decimal separator instead of comma.
	- Check the attribute table that the values are correct (click the new column field name to order the values in order to see the highest and lowest values, you should only have numbers 1, 2, 3 and 4).
	- Do the same for the remaining proportion field.
		- Again, read the expression aloud if you don’t understand it!

---

### Finding the low education/low-income areas

11. **Now that you’ve reclassified the proportions into classes 1, 2, 3 or 4 it’s time to find the low
education & low-income areas in Helsinki metropolitan region.**
	
	- Select the grid squares that have been given the classification 4 in both of the reclassified fields
		- Do you remember how to select attributes based on their value? Hint: check step number 4
	- Save the selection as a new layer and give it an informative name
	- Compose a map of the results

---

### Optional: Refining the analysis 

12. The analysis we’ve done above is quite coarse. You can refine it by using the following fields:
	- te_vuok_as (Households living in rental dwellings, Household life theme’s prefix te_)
		- Household life: te_taly (Households, total)
	- pt_tyott (Unemployed, Main type of activity theme’s prefix pt_)
		- Main type of activity: pt_tyovy (Labour force, total)

13.  You should use the original grid data and not the one you’ve been working with. Why?
		- You’ll have an untampered dataset and won’t lose any progress you’ve made with education and income data due to unfortunate errors. 
		- Note: The education and income fields’ total number fields have the population 18 years old and older (can you think of why?), but the totals for household and unemployment fields use different metrics: Total number of households and total number of available workforces.
		- Before tampering with the original grid file, you should save it as a new file, so you have a clean backup to fall back on. 

14. When you’ve reclassified the proportions to the quartiles, you can join the layers using the id_nro field.
	- You can select which fields to join, so you don’t have to join all the fields, just the
reclassified fields for rented dwellings and unemployment.

15. Compose a map of the results
	- How do the refined results differ from the coarser results?
	- Are these refined results enough to delineate segregated areas?
		- Would you need additional data? What data?

 



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
Bsb29rIHNvbWV0aGluZyBsaWtlIHRoaXM6In0sInFkUktoUThz
b0J2ZzVJaFQiOnsic3RhcnQiOjkwOTYsImVuZCI6OTEzNywidG
V4dCI6IlRoZSBleHByZXNzaW9uIGxvb2tzIHNvbWV0aGluZyBs
aWtlIHRoaXM6In19LCJjb21tZW50cyI6eyIzTG9HS2VRRkVNV3
pqYkUxIjp7ImRpc2N1c3Npb25JZCI6ImVUYzhhb0JKbjd6ZHJm
MGsiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJVcGRhdG
UgaWYgYXBwbGljYWJsZSIsImNyZWF0ZWQiOjE2ODY0NzY0MzY4
Nzh9LCJsUGtsVUZiRTRlVTIwMzRaIjp7ImRpc2N1c3Npb25JZC
I6IlFQMVhDYkNwUnNkMGxWcTUiLCJzdWIiOiJnaDo0MDMwNDc4
OCIsInRleHQiOiJVcGRhdGUgaWYgYXBwbGljYWJsZSIsImNyZW
F0ZWQiOjE2ODY0NzY1Nzk1Njd9LCJCdUJGbWlqR2lyakVjNVVr
Ijp7ImRpc2N1c3Npb25JZCI6Ild2em55ZktMWHZubEVEaTQiLC
JzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQgcGFnZSIs
ImNyZWF0ZWQiOjE2ODY0NzY3MzYwNTV9LCJQS0JhSlphM2Rtd2
xWcUY1Ijp7ImRpc2N1c3Npb25JZCI6IkJ3ZFRwa3lIblpFQmNO
clgiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJSZWZlcm
VuY2UiLCJjcmVhdGVkIjoxNjg2NDc3NDc1ODg4fSwidzdFVlMy
eE1QelJjSUNMZiI6eyJkaXNjdXNzaW9uSWQiOiI1dUhCTVNsNU
1TbVpicFZqIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ijoi
QWRkIGluc3RydWN0aW9ucyB0byBkb3dubG9hZCBkYXRhIHRoZW
1zZWx2ZXMiLCJjcmVhdGVkIjoxNjg2NDc3NDk0MTIwfSwiMjNj
RUtkNW1lM2NFbElGNSI6eyJkaXNjdXNzaW9uSWQiOiIydFNYbH
ozT3lyalZIdkZqIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiQWRkIGluc3RydWN0aW9ucyBvbiBob3cgdG8gdXNlIHRoaX
MiLCJjcmVhdGVkIjoxNjg2NDc3NTQ5NzkxfSwiUXQxa3Q3V2hQ
QWtWQW14RCI6eyJkaXNjdXNzaW9uSWQiOiJEdmdmcEpzZnZ3Y0
5mOGlWIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRk
IHBpY3R1cmUgb2YgZXhwcmVzc2lvbiIsImNyZWF0ZWQiOjE2OD
Y0NzgzMDM4ODd9LCJacjJLWnFUUldwcWo2U05UIjp7ImRpc2N1
c3Npb25JZCI6IlJpYktXVTFRQzdyWkNCWDUiLCJzdWIiOiJnaD
o0MDMwNDc4OCIsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0
ZWQiOjE2ODY0Nzg1OTU0NTR9LCJ6aU5QRnNObjJhM3JsWEpCIj
p7ImRpc2N1c3Npb25JZCI6IktmMzRvY21pTEI5NXg5MksiLCJz
dWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJVcGRhdGUgd2l0aC
Bwb3NpdGlvbiBpbiBjb3Vyc2UiLCJjcmVhdGVkIjoxNjg2NDc5
NDY5NjU1fSwiY1ZGTEZWd2VEVnI2ZXp5NiI6eyJkaXNjdXNzaW
9uSWQiOiJUa0xpczlSZndTMkp5bTdsIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiVG9vIGxpdHRsZSBpbnN0cnVjdGlvbn
MgZm9yIHRoaXMgc3RhZ2Ugb2YgdGhlIGNvdXJzZT8iLCJjcmVh
dGVkIjoxNjg2NDc5NTkyNDYxfSwiVHFpMndBdlVoaVVJTlhRMC
I6eyJkaXNjdXNzaW9uSWQiOiIyZHdDOWZ0bHVJRVdUQllWIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVG9vIGxpdHRsZS
BpbnN0cnVjdGlvbnMgZm9yIHRoaXMgc3RhZ2Ugb2YgdGhlIGNv
dXJzZT8iLCJjcmVhdGVkIjoxNjg2NDc5NzU4MTM2fSwiSnRuZD
BtQWVyY1VhSzZpUyI6eyJkaXNjdXNzaW9uSWQiOiJHTHBBUXZO
MXMzUUh2Ukk0Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg2NDc5ODM4MzY3
fSwieGI0Zjc2R0NIQ0kxUmtqayI6eyJkaXNjdXNzaW9uSWQiOi
JxZFJLaFE4c29Cdmc1SWhUIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg2ND
gwMTA5MDMxfX0sImhpc3RvcnkiOlstMjY5NTU4Nzg1LC0xMzY0
MTc0OTkzLDE3MjY4MTM2MzQsLTEzMTE1Mjk0MDUsNTE2MjEzMj
Q4LC0xNzI1NzcyMTYxLDE2NzcwMjkxNTEsLTEzMzIwODc5NjNd
fQ==
-->