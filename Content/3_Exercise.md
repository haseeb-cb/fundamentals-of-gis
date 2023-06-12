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
		- You can use for example satellite imagery like we did in the Crash Course, or OpenStreetMaps, which you can add using the same steps as for google satellite imagery. 
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
![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/3_Exercise/3_Exercise_datacleanup_expression.png)
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
R0lTIGZyb20gdGhlIGNvdXJzZSBNb29kbGXigKYifSwiRHZnZn
BKc2Z2d2NOZjhpViI6eyJzdGFydCI6NTQ1NCwiZW5kIjo1NjU2
LCJ0ZXh0IjoiNC4gWW91IGNvdWxkIHVzZSBzZWxlY3QgYnkgZX
hwcmVzc2lvbiB0byBzZWxlY3QgdGhlIGZlYXR1cmVzIHRoYXQg
aGF2ZSB2YWx1ZXMgaeKApiJ9LCJSaWJLV1UxUUM3clpDQlg1Ij
p7InN0YXJ0Ijo1ODQ4LCJlbmQiOjU4NTMsInRleHQiOiJwcmVz
cyJ9LCJUa0xpczlSZndTMkp5bTdsIjp7InN0YXJ0Ijo2Mzc2LC
JlbmQiOjY0OTUsInRleHQiOiI2LiAqKkluIHRoZSBuZXdseSBj
cmVhdGVkIGxheWVyLCB1c2UgdGhlIGZpZWxkIGNhbGN1bGF0b3
IgdG8gY2FsY3VsYXRlIG5ldyBmaWVs4oCmIn0sIjJkd0M5ZnRs
dUlFV1RCWVYiOnsic3RhcnQiOjgwNTIsImVuZCI6ODEzNywidG
V4dCI6Ii0gU28sIG9wZW4gdGhlIHN0eWxlIHRhYiBvZiB0aGUg
bGF5ZXIsIHNlbGVjdCBncmFkdWF0ZWQsIHNlbGVjdCB0aGUgY2
9ycmVjdCBmaWXigKYifSwiR0xwQVF2TjFzM1FIdlJJNCI6eyJz
dGFydCI6ODM3MywiZW5kIjo4NDI5LCJ0ZXh0IjoiRm9yIEJhc2
ljLWxldmVsIGVkdWNhdGlvbiB0aGV5IGxvb2sgc29tZXRoaW5n
IGxpa2UgdGhpczoifSwicWRSS2hROHNvQnZnNUloVCI6eyJzdG
FydCI6OTQ3NSwiZW5kIjo5NTE2LCJ0ZXh0IjoiVGhlIGV4cHJl
c3Npb24gbG9va3Mgc29tZXRoaW5nIGxpa2UgdGhpczoifSwiOF
RtdjRabm5HNkRHMW9FQSI6eyJzdGFydCI6OTU3OCwiZW5kIjo5
NzgwLCJ0ZXh0IjoiLSBDaGVjayB0aGUgKmF0dHJpYnV0ZSB0YW
JsZSogdGhhdCB0aGUgdmFsdWVzIGFyZSBjb3JyZWN0IChjbGlj
ayB0aGUgbmV3IGNvbHVtbuKApiJ9LCJNclRDNlhlUUxWeXV5bk
xGIjp7InN0YXJ0IjoxMDM4NywiZW5kIjoxMDQxNywidGV4dCI6
Ii0gQ29tcG9zZSBhIG1hcCBvZiB0aGUgcmVzdWx0cyJ9LCJETj
JnRk9Pc3dCN1R5WGtoIjp7InN0YXJ0IjoxMDMxOCwiZW5kIjox
MDM4NSwidGV4dCI6Ii0gU2F2ZSB0aGUgc2VsZWN0aW9uIGFzIG
EgbmV3IGxheWVyIGFuZCBnaXZlIGl0IGFuIGluZm9ybWF0aXZl
IG5hbWUifX0sImNvbW1lbnRzIjp7IjNMb0dLZVFGRU1XempiRT
EiOnsiZGlzY3Vzc2lvbklkIjoiZVRjOGFvQkpuN3pkcmYwayIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlVwZGF0ZSBpZi
BhcHBsaWNhYmxlIiwiY3JlYXRlZCI6MTY4NjQ3NjQzNjg3OH0s
ImxQa2xVRmJFNGVVMjAzNFoiOnsiZGlzY3Vzc2lvbklkIjoiUV
AxWENiQ3BSc2QwbFZxNSIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IlVwZGF0ZSBpZiBhcHBsaWNhYmxlIiwiY3JlYXRlZC
I6MTY4NjQ3NjU3OTU2N30sIkJ1QkZtaWpHaXJqRWM1VWsiOnsi
ZGlzY3Vzc2lvbklkIjoiV3Z6bnlmS0xYdm5sRURpNCIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwYWdlIiwiY3Jl
YXRlZCI6MTY4NjQ3NjczNjA1NX0sIlBLQmFKWmEzZG13bFZxRj
UiOnsiZGlzY3Vzc2lvbklkIjoiQndkVHBreUhuWkVCY05yWCIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlJlZmVyZW5jZS
IsImNyZWF0ZWQiOjE2ODY0Nzc0NzU4ODh9LCJ3N0VWUzJ4TVB6
UmNJQ0xmIjp7ImRpc2N1c3Npb25JZCI6IjV1SEJNU2w1TVNtWm
JwVmoiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJBZGQg
aW5zdHJ1Y3Rpb25zIHRvIGRvd25sb2FkIGRhdGEgdGhlbXNlbH
ZlcyIsImNyZWF0ZWQiOjE2ODY0Nzc0OTQxMjB9LCJRdDFrdDdX
aFBBa1ZBbXhEIjp7ImRpc2N1c3Npb25JZCI6IkR2Z2ZwSnNmdn
djTmY4aVYiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJB
ZGQgcGljdHVyZSBvZiBleHByZXNzaW9uIiwiY3JlYXRlZCI6MT
Y4NjQ3ODMwMzg4N30sIlpyMktacVRSV3BxajZTTlQiOnsiZGlz
Y3Vzc2lvbklkIjoiUmliS1dVMVFDN3JaQ0JYNSIsInN1YiI6Im
doOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3Jl
YXRlZCI6MTY4NjQ3ODU5NTQ1NH0sImNWRkxGVndlRFZyNmV6eT
YiOnsiZGlzY3Vzc2lvbklkIjoiVGtMaXM5UmZ3UzJKeW03bCIs
InN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IlRvbyBsaXR0bG
UgaW5zdHJ1Y3Rpb25zIGZvciB0aGlzIHN0YWdlIG9mIHRoZSBj
b3Vyc2U/IiwiY3JlYXRlZCI6MTY4NjQ3OTU5MjQ2MX0sIlRxaT
J3QXZVaGlVSU5YUTAiOnsiZGlzY3Vzc2lvbklkIjoiMmR3Qzlm
dGx1SUVXVEJZViIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dC
I6IlRvbyBsaXR0bGUgaW5zdHJ1Y3Rpb25zIGZvciB0aGlzIHN0
YWdlIG9mIHRoZSBjb3Vyc2U/IiwiY3JlYXRlZCI6MTY4NjQ3OT
c1ODEzNn0sIkp0bmQwbUFlcmNVYUs2aVMiOnsiZGlzY3Vzc2lv
bklkIjoiR0xwQVF2TjFzM1FIdlJJNCIsInN1YiI6ImdoOjQwMz
A0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3JlYXRlZCI6
MTY4NjQ3OTgzODM2N30sInhiNGY3NkdDSENJMVJramsiOnsiZG
lzY3Vzc2lvbklkIjoicWRSS2hROHNvQnZnNUloVCIsInN1YiI6
ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBwaWN0dXJlIiwiY3
JlYXRlZCI6MTY4NjQ4MDEwOTAzMX0sIkw3eldib0l0U3hwR1RL
b28iOnsiZGlzY3Vzc2lvbklkIjoiRHZnZnBKc2Z2d2NOZjhpVi
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6ImFuZCBoaW50
IHRvIHByZXZpb3VzIGV4ZXJjaXNlIiwiY3JlYXRlZCI6MTY4Nj
Q4MzY5Mjk2NX0sIkNSQ3Jkc0pNdU1WRm9rTGQiOnsiZGlzY3Vz
c2lvbklkIjoiRHZnZnBKc2Z2d2NOZjhpViIsInN1YiI6ImdoOj
QwMzA0Nzg4IiwidGV4dCI6ImFuZCB3cml0ZSBvdXQgZnVydGhl
ciB0byBleHBsYWluIiwiY3JlYXRlZCI6MTY4NjU1MDYzMDMwNX
0sIlZJSjFFQ094NFNMUmIzVEUiOnsiZGlzY3Vzc2lvbklkIjoi
OFRtdjRabm5HNkRHMW9FQSIsInN1YiI6ImdoOjQwMzA0Nzg4Ii
widGV4dCI6IklmIGl0IGFwcGVhcnMgbm8gdmFsdWVzIGhhdmUg
YmVlbiBjYWxjdWxhdGVkLCBjaGVjayB0aGF0IFwiT25seSB1cG
RhdGUgWCBzZWxlY3RlZCBmZWF0dXJlc1wiIGlzIHRpY2tlZCBv
ZmYgaW4gdGhlIGZpZWxkIGNhbGN1bGF0b3IuIiwiY3JlYXRlZC
I6MTY4NjU1MzA0Njk2OH0sIlB6ZHhWZVc4bG5TOXhaaUsiOnsi
ZGlzY3Vzc2lvbklkIjoiTXJUQzZYZVFMVnl1eW5MRiIsInN1Yi
I6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkhvdyBtYW55IGFuZCBv
ZiB3aGF0PyIsImNyZWF0ZWQiOjE2ODY1NTMyMzcxNzV9LCJXMm
tLNmdZdUU4RjZpb3p5Ijp7ImRpc2N1c3Npb25JZCI6IkROMmdG
T09zd0I3VHlYa2giLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleH
QiOiJUaGlzIG9yIGdyYWR1YXRlZD8iLCJjcmVhdGVkIjoxNjg2
NTUzMjkwMzM1fSwiU2ZGYzlnQjdYY0d2dDg2MiI6eyJkaXNjdX
NzaW9uSWQiOiJNclRDNlhlUUxWeXV5bkxGIiwic3ViIjoiZ2g6
NDAzMDQ3ODgiLCJ0ZXh0IjoiYW5kIFFNUyBpbnN0cnVjdGlvbn
MiLCJjcmVhdGVkIjoxNjg2NTU0NDI4NTE4fX0sImhpc3Rvcnki
OlstMTM4NjIyNjQxMywxODI1MDM3MDQwLC0zOTE4ODIwNTAsLT
E2Mzc2MDQxNzksLTE1Njg3Njk3NjksMTA3NTU4ODk1MiwtNDY5
NjQxNjgyLC0yNjk1NTg3ODUsLTEzNjQxNzQ5OTMsMTcyNjgxMz
YzNCwtMTMxMTUyOTQwNSw1MTYyMTMyNDgsLTE3MjU3NzIxNjEs
MTY3NzAyOTE1MSwtMTMzMjA4Nzk2M119
-->