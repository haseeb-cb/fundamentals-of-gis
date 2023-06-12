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

2. Familiarizing yourself with raster data and data classification

3. Familiarizing yourself with using expressions and conditional statements
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
		- Don't forget to give the new file an informative name and save it in your folder! 

	*Tip: If you are confused with the formula, try reading it aloud: “Select the features where X is greater than 0 AND Y is greater or equal than 0, AND…”*

5. **You should end up with a new layer without any -1 values in the four wanted fields.**

---

### Calculating the proportions

6. **In the newly created layer, use the *field calculator* to calculate new fields for the proportions
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
	- In the Symbology-tab and under the *Graduated* symbols you can find different classification methods.
	- When classifying data with *Equal Count* as the classification method and setting the number of classes to four, each class is called a quartile.
		- Thus, each class has the same number of entries (hence equal count)

9. **We’re going to have to utilize QGIS’s visualization tools to find out the class boundaries for
quantiles within QGIS.** You could also use any statistical analysis application (Excel, LibreCalc,
SPSS etc.) to find out the boundaries.
	- So, open the *style* tab of the layer, select *graduated*, select the correct field
		- E.g., Basic-level education proportion
	-  Switch mode to *Quantiles (Equal Count)* and drop the number of classes from 5 down to 4. Click *Classify*
		- Make notes about the class boundaries because you’re going to use them soon. For Basic-level education they look something like this:
		- Do the same for the remaining proportion field (level of income percentage) and make notes about the class boundaries for that field as well.

10. **Now that we have the boundaries for the two classifications, it’s time to reclassify the data
into four classes.**
	- Open the *attribute table* and *field calculator*, we’re creating new fields for the reclassified values using a slightly more complex conditional statement this time. 
		- Note! Do all the analyses in the same layer so that you get the new columns in the same layer.
	- The logic behind the numbering of the classes should be the same across all the reclassifications. In this instance our logic can be as follows: class 1 is the lowest (e.g. lowest share of inhabitants with no qualification after basic-level studies) and class 4 is the highest quartile (e.g. highest share of inhabitants with no qualification after basic level studies).
	- Let’s use the conditional statement first for basic-level education proportions. This is where you use the class boundary notes. The expression looks something like this:
	- NOTE: Use a dot as a decimal separator instead of comma.
	- Check the *attribute table* that the values are correct (click the new column field name to order the values in order to see the highest and lowest values, you should only have numbers 1, 2, 3 and 4).
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
dm5sRURpNCI6eyJzdGFydCI6MTg0NSwiZW5kIjoxODU3LCJ0ZX
h0IjoicGRmIGluY2x1ZGVkIn0sIkJ3ZFRwa3lIblpFQmNOclgi
Onsic3RhcnQiOjM0MjksImVuZCI6MzQzOCwidGV4dCI6InBkZi
1maWxlcyJ9LCI1dUhCTVNsNU1TbVpicFZqIjp7InN0YXJ0Ijoz
Mjk1LCJlbmQiOjMzNzksInRleHQiOiIxLiBEb3dubG9hZCwgdW
56aXAgYW5kIG9wZW4gdGhlIGV4ZXJjaXNlIDMgZGF0YSBpbiBR
R0lTIGZyb20gdGhlIGNvdXJzZSBNb29kbGXigKYifSwiMnRTWG
x6M095cmpWSHZGaiI6eyJzdGFydCI6NDM4NiwiZW5kIjo0NTA4
LCJ0ZXh0IjoiLSBZb3UgY2FuIHVzZSBmb3IgZXhhbXBsZSBRdW
lja01hcFNlcnZpY2VzLCB0aGUgc3BhdGlhbCBkYXRhIGZyb20g
dGhlIENyYXNoIENvdeKApiJ9LCJEdmdmcEpzZnZ3Y05mOGlWIj
p7InN0YXJ0Ijo1NDA4LCJlbmQiOjU2MTAsInRleHQiOiI0LiBZ
b3UgY291bGQgdXNlIHNlbGVjdCBieSBleHByZXNzaW9uIHRvIH
NlbGVjdCB0aGUgZmVhdHVyZXMgdGhhdCBoYXZlIHZhbHVlcyBp
4oCmIn0sIlJpYktXVTFRQzdyWkNCWDUiOnsic3RhcnQiOjU2ND
QsImVuZCI6NTY0OSwidGV4dCI6InByZXNzIn0sIlRrTGlzOVJm
d1MySnltN2wiOnsic3RhcnQiOjYxNzIsImVuZCI6NjI5MSwidG
V4dCI6IjYuICoqSW4gdGhlIG5ld2x5IGNyZWF0ZWQgbGF5ZXIs
IHVzZSB0aGUgZmllbGQgY2FsY3VsYXRvciB0byBjYWxjdWxhdG
UgbmV3IGZpZWzigKYifSwiMmR3QzlmdGx1SUVXVEJZViI6eyJz
dGFydCI6Nzg0OCwiZW5kIjo3OTMzLCJ0ZXh0IjoiLSBTbywgb3
BlbiB0aGUgc3R5bGUgdGFiIG9mIHRoZSBsYXllciwgc2VsZWN0
IGdyYWR1YXRlZCwgc2VsZWN0IHRoZSBjb3JyZWN0IGZpZeKApi
J9LCJHTHBBUXZOMXMzUUh2Ukk0Ijp7InN0YXJ0Ijo4MTY5LCJl
bmQiOjgyMjUsInRleHQiOiJGb3IgQmFzaWMtbGV2ZWwgZWR1Y2
F0aW9uIHRoZXkgbG9vayBzb21ldGhpbmcgbGlrZSB0aGlzOiJ9
LCJxZFJLaFE4c29Cdmc1SWhUIjp7InN0YXJ0Ijo5MjcxLCJlbm
QiOjkzMTIsInRleHQiOiJUaGUgZXhwcmVzc2lvbiBsb29rcyBz
b21ldGhpbmcgbGlrZSB0aGlzOiJ9LCI4VG12NFpubkc2REcxb0
VBIjp7InN0YXJ0Ijo5Mzc0LCJlbmQiOjk1NzYsInRleHQiOiIt
IENoZWNrIHRoZSAqYXR0cmlidXRlIHRhYmxlKiB0aGF0IHRoZS
B2YWx1ZXMgYXJlIGNvcnJlY3QgKGNsaWNrIHRoZSBuZXcgY29s
dW1u4oCmIn0sIk1yVEM2WGVRTFZ5dXluTEYiOnsic3RhcnQiOj
EwMTgzLCJlbmQiOjEwMjEzLCJ0ZXh0IjoiLSBDb21wb3NlIGEg
bWFwIG9mIHRoZSByZXN1bHRzIn0sIkROMmdGT09zd0I3VHlYa2
giOnsic3RhcnQiOjEwMTE0LCJlbmQiOjEwMTgxLCJ0ZXh0Ijoi
LSBTYXZlIHRoZSBzZWxlY3Rpb24gYXMgYSBuZXcgbGF5ZXIgYW
5kIGdpdmUgaXQgYW4gaW5mb3JtYXRpdmUgbmFtZSJ9fSwiY29t
bWVudHMiOnsiM0xvR0tlUUZFTVd6amJFMSI6eyJkaXNjdXNzaW
9uSWQiOiJlVGM4YW9CSm43emRyZjBrIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiVXBkYXRlIGlmIGFwcGxpY2FibGUiLC
JjcmVhdGVkIjoxNjg2NDc2NDM2ODc4fSwibFBrbFVGYkU0ZVUy
MDM0WiI6eyJkaXNjdXNzaW9uSWQiOiJRUDFYQ2JDcFJzZDBsVn
E1Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVXBkYXRl
IGlmIGFwcGxpY2FibGUiLCJjcmVhdGVkIjoxNjg2NDc2NTc5NT
Y3fSwiQnVCRm1pakdpcmpFYzVVayI6eyJkaXNjdXNzaW9uSWQi
OiJXdnpueWZLTFh2bmxFRGk0Iiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiQWRkIHBhZ2UiLCJjcmVhdGVkIjoxNjg2NDc2
NzM2MDU1fSwiUEtCYUpaYTNkbXdsVnFGNSI6eyJkaXNjdXNzaW
9uSWQiOiJCd2RUcGt5SG5aRUJjTnJYIiwic3ViIjoiZ2g6NDAz
MDQ3ODgiLCJ0ZXh0IjoiUmVmZXJlbmNlIiwiY3JlYXRlZCI6MT
Y4NjQ3NzQ3NTg4OH0sInc3RVZTMnhNUHpSY0lDTGYiOnsiZGlz
Y3Vzc2lvbklkIjoiNXVIQk1TbDVNU21aYnBWaiIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbnN0cnVjdGlvbnMg
dG8gZG93bmxvYWQgZGF0YSB0aGVtc2VsdmVzIiwiY3JlYXRlZC
I6MTY4NjQ3NzQ5NDEyMH0sIjIzY0VLZDVtZTNjRWxJRjUiOnsi
ZGlzY3Vzc2lvbklkIjoiMnRTWGx6M095cmpWSHZGaiIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBpbnN0cnVjdGlv
bnMgb24gaG93IHRvIHVzZSB0aGlzIiwiY3JlYXRlZCI6MTY4Nj
Q3NzU0OTc5MX0sIlF0MWt0N1doUEFrVkFteEQiOnsiZGlzY3Vz
c2lvbklkIjoiRHZnZnBKc2Z2d2NOZjhpViIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIG9mIGV4cHJl
c3Npb24iLCJjcmVhdGVkIjoxNjg2NDc4MzAzODg3fSwiWnIyS1
pxVFJXcHFqNlNOVCI6eyJkaXNjdXNzaW9uSWQiOiJSaWJLV1Ux
UUM3clpDQlg1Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg2NDc4NTk1NDU0
fSwiY1ZGTEZWd2VEVnI2ZXp5NiI6eyJkaXNjdXNzaW9uSWQiOi
JUa0xpczlSZndTMkp5bTdsIiwic3ViIjoiZ2g6NDAzMDQ3ODgi
LCJ0ZXh0IjoiVG9vIGxpdHRsZSBpbnN0cnVjdGlvbnMgZm9yIH
RoaXMgc3RhZ2Ugb2YgdGhlIGNvdXJzZT8iLCJjcmVhdGVkIjox
Njg2NDc5NTkyNDYxfSwiVHFpMndBdlVoaVVJTlhRMCI6eyJkaX
NjdXNzaW9uSWQiOiIyZHdDOWZ0bHVJRVdUQllWIiwic3ViIjoi
Z2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVG9vIGxpdHRsZSBpbnN0cn
VjdGlvbnMgZm9yIHRoaXMgc3RhZ2Ugb2YgdGhlIGNvdXJzZT8i
LCJjcmVhdGVkIjoxNjg2NDc5NzU4MTM2fSwiSnRuZDBtQWVyY1
VhSzZpUyI6eyJkaXNjdXNzaW9uSWQiOiJHTHBBUXZOMXMzUUh2
Ukk0Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIH
BpY3R1cmUiLCJjcmVhdGVkIjoxNjg2NDc5ODM4MzY3fSwieGI0
Zjc2R0NIQ0kxUmtqayI6eyJkaXNjdXNzaW9uSWQiOiJxZFJLaF
E4c29Cdmc1SWhUIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0
IjoiQWRkIHBpY3R1cmUiLCJjcmVhdGVkIjoxNjg2NDgwMTA5MD
MxfSwiTDd6V2JvSXRTeHBHVEtvbyI6eyJkaXNjdXNzaW9uSWQi
OiJEdmdmcEpzZnZ3Y05mOGlWIiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiYW5kIGhpbnQgdG8gcHJldmlvdXMgZXhlcmNp
c2UiLCJjcmVhdGVkIjoxNjg2NDgzNjkyOTY1fSwiQ1JDcmRzSk
11TVZGb2tMZCI6eyJkaXNjdXNzaW9uSWQiOiJEdmdmcEpzZnZ3
Y05mOGlWIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiYW
5kIHdyaXRlIG91dCBmdXJ0aGVyIHRvIGV4cGxhaW4iLCJjcmVh
dGVkIjoxNjg2NTUwNjMwMzA1fSwiVklKMUVDT3g0U0xSYjNURS
I6eyJkaXNjdXNzaW9uSWQiOiI4VG12NFpubkc2REcxb0VBIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiSWYgaXQgYXBwZW
FycyBubyB2YWx1ZXMgaGF2ZSBiZWVuIGNhbGN1bGF0ZWQsIGNo
ZWNrIHRoYXQgXCJPbmx5IHVwZGF0ZSBYIHNlbGVjdGVkIGZlYX
R1cmVzXCIgaXMgdGlja2VkIG9mZiBpbiB0aGUgZmllbGQgY2Fs
Y3VsYXRvci4iLCJjcmVhdGVkIjoxNjg2NTUzMDQ2OTY4fSwiUH
pkeFZlVzhsblM5eFppSyI6eyJkaXNjdXNzaW9uSWQiOiJNclRD
NlhlUUxWeXV5bkxGIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZX
h0IjoiSG93IG1hbnkgYW5kIG9mIHdoYXQ/IiwiY3JlYXRlZCI6
MTY4NjU1MzIzNzE3NX0sIlcya0s2Z1l1RThGNmlvenkiOnsiZG
lzY3Vzc2lvbklkIjoiRE4yZ0ZPT3N3QjdUeVhraCIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlRoaXMgb3IgZ3JhZHVhdG
VkPyIsImNyZWF0ZWQiOjE2ODY1NTMyOTAzMzV9LCJTZkZjOWdC
N1hjR3Z0ODYyIjp7ImRpc2N1c3Npb25JZCI6Ik1yVEM2WGVRTF
Z5dXluTEYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJh
bmQgUU1TIGluc3RydWN0aW9ucyIsImNyZWF0ZWQiOjE2ODY1NT
Q0Mjg1MTh9fSwiaGlzdG9yeSI6Wy0zMDcwMzQxOTAsMTgyNTAz
NzA0MCwtMzkxODgyMDUwLC0xNjM3NjA0MTc5LC0xNTY4NzY5Nz
Y5LDEwNzU1ODg5NTIsLTQ2OTY0MTY4MiwtMjY5NTU4Nzg1LC0x
MzY0MTc0OTkzLDE3MjY4MTM2MzQsLTEzMTE1Mjk0MDUsNTE2Mj
EzMjQ4LC0xNzI1NzcyMTYxLDE2NzcwMjkxNTEsLTEzMzIwODc5
NjNdfQ==
-->