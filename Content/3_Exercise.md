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
2.1 step 7
4. **You could use select by expression** to select the features that have values in the two wanted fields (ko_perus, hr_pi_tul) that are 0 or greater AND have people living in them (ko_ika18y, hr_tuy):
![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/3_Exercise/3_Exercise_datacleanup_expression.png)
	- Hint: Crash Course 2.1 step 7
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
	- Hint: Crash Course 2.1 step 5, 6, and 9

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
	- So, open the *symbology* tab of the layer, select *graduated*, select the correct field
		- E.g., Basic-level education proportion
	-  Switch mode to *Quantiles (Equal Count)* and drop the number of classes from 5 down to 4. Click *Classify*
		- Make notes about the class boundaries because you’re going to use them soon. For Basic-level education they look something like this:
![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/3_Exercise/3_Exercise_data_classification_edu.png)
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
R0lTIGZyb20gdGhlIGNvdXJzZSBNb29kbGXigKYifSwiMmR3Qz
lmdGx1SUVXVEJZViI6eyJzdGFydCI6ODA5OSwiZW5kIjo4MTg4
LCJ0ZXh0IjoiLSBTbywgb3BlbiB0aGUgc3R5bGUgdGFiIG9mIH
RoZSBsYXllciwgc2VsZWN0IGdyYWR1YXRlZCwgc2VsZWN0IHRo
ZSBjb3JyZWN0IGZpZeKApiJ9LCJHTHBBUXZOMXMzUUh2Ukk0Ij
p7InN0YXJ0Ijo4NDI0LCJlbmQiOjg0ODAsInRleHQiOiJGb3Ig
QmFzaWMtbGV2ZWwgZWR1Y2F0aW9uIHRoZXkgbG9vayBzb21ldG
hpbmcgbGlrZSB0aGlzOiJ9LCJxZFJLaFE4c29Cdmc1SWhUIjp7
InN0YXJ0Ijo5Njg1LCJlbmQiOjk3MjYsInRleHQiOiJUaGUgZX
hwcmVzc2lvbiBsb29rcyBzb21ldGhpbmcgbGlrZSB0aGlzOiJ9
LCI4VG12NFpubkc2REcxb0VBIjp7InN0YXJ0Ijo5Nzg4LCJlbm
QiOjk5OTAsInRleHQiOiItIENoZWNrIHRoZSAqYXR0cmlidXRl
IHRhYmxlKiB0aGF0IHRoZSB2YWx1ZXMgYXJlIGNvcnJlY3QgKG
NsaWNrIHRoZSBuZXcgY29sdW1u4oCmIn0sIk1yVEM2WGVRTFZ5
dXluTEYiOnsic3RhcnQiOjEwNTk3LCJlbmQiOjEwNjI3LCJ0ZX
h0IjoiLSBDb21wb3NlIGEgbWFwIG9mIHRoZSByZXN1bHRzIn0s
IkROMmdGT09zd0I3VHlYa2giOnsic3RhcnQiOjEwNTI4LCJlbm
QiOjEwNTk1LCJ0ZXh0IjoiLSBTYXZlIHRoZSBzZWxlY3Rpb24g
YXMgYSBuZXcgbGF5ZXIgYW5kIGdpdmUgaXQgYW4gaW5mb3JtYX
RpdmUgbmFtZSJ9fSwiY29tbWVudHMiOnsiM0xvR0tlUUZFTVd6
amJFMSI6eyJkaXNjdXNzaW9uSWQiOiJlVGM4YW9CSm43emRyZj
BrIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVXBkYXRl
IGlmIGFwcGxpY2FibGUiLCJjcmVhdGVkIjoxNjg2NDc2NDM2OD
c4fSwibFBrbFVGYkU0ZVUyMDM0WiI6eyJkaXNjdXNzaW9uSWQi
OiJRUDFYQ2JDcFJzZDBsVnE1Iiwic3ViIjoiZ2g6NDAzMDQ3OD
giLCJ0ZXh0IjoiVXBkYXRlIGlmIGFwcGxpY2FibGUiLCJjcmVh
dGVkIjoxNjg2NDc2NTc5NTY3fSwiQnVCRm1pakdpcmpFYzVVay
I6eyJkaXNjdXNzaW9uSWQiOiJXdnpueWZLTFh2bmxFRGk0Iiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBhZ2UiLC
JjcmVhdGVkIjoxNjg2NDc2NzM2MDU1fSwiUEtCYUpaYTNkbXds
VnFGNSI6eyJkaXNjdXNzaW9uSWQiOiJCd2RUcGt5SG5aRUJjTn
JYIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiUmVmZXJl
bmNlIiwiY3JlYXRlZCI6MTY4NjQ3NzQ3NTg4OH0sInc3RVZTMn
hNUHpSY0lDTGYiOnsiZGlzY3Vzc2lvbklkIjoiNXVIQk1TbDVN
U21aYnBWaiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6Ik
FkZCBpbnN0cnVjdGlvbnMgdG8gZG93bmxvYWQgZGF0YSB0aGVt
c2VsdmVzIiwiY3JlYXRlZCI6MTY4NjQ3NzQ5NDEyMH0sIlRxaT
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
JlYXRlZCI6MTY4NjQ4MDEwOTAzMX0sIlZJSjFFQ094NFNMUmIz
VEUiOnsiZGlzY3Vzc2lvbklkIjoiOFRtdjRabm5HNkRHMW9FQS
IsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IklmIGl0IGFw
cGVhcnMgbm8gdmFsdWVzIGhhdmUgYmVlbiBjYWxjdWxhdGVkLC
BjaGVjayB0aGF0IFwiT25seSB1cGRhdGUgWCBzZWxlY3RlZCBm
ZWF0dXJlc1wiIGlzIHRpY2tlZCBvZmYgaW4gdGhlIGZpZWxkIG
NhbGN1bGF0b3IuIiwiY3JlYXRlZCI6MTY4NjU1MzA0Njk2OH0s
IlB6ZHhWZVc4bG5TOXhaaUsiOnsiZGlzY3Vzc2lvbklkIjoiTX
JUQzZYZVFMVnl1eW5MRiIsInN1YiI6ImdoOjQwMzA0Nzg4Iiwi
dGV4dCI6IkhvdyBtYW55IGFuZCBvZiB3aGF0PyIsImNyZWF0ZW
QiOjE2ODY1NTMyMzcxNzV9LCJXMmtLNmdZdUU4RjZpb3p5Ijp7
ImRpc2N1c3Npb25JZCI6IkROMmdGT09zd0I3VHlYa2giLCJzdW
IiOiJnaDo0MDMwNDc4OCIsInRleHQiOiJUaGlzIG9yIGdyYWR1
YXRlZD8iLCJjcmVhdGVkIjoxNjg2NTUzMjkwMzM1fSwiU2ZGYz
lnQjdYY0d2dDg2MiI6eyJkaXNjdXNzaW9uSWQiOiJNclRDNlhl
UUxWeXV5bkxGIiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0Ij
oiYW5kIFFNUyBpbnN0cnVjdGlvbnMiLCJjcmVhdGVkIjoxNjg2
NTU0NDI4NTE4fX0sImhpc3RvcnkiOlsxNTAzNjk5NTAwLDE4Mj
UwMzcwNDAsLTM5MTg4MjA1MCwtMTYzNzYwNDE3OSwtMTU2ODc2
OTc2OSwxMDc1NTg4OTUyLC00Njk2NDE2ODIsLTI2OTU1ODc4NS
wtMTM2NDE3NDk5MywxNzI2ODEzNjM0LC0xMzExNTI5NDA1LDUx
NjIxMzI0OCwtMTcyNTc3MjE2MSwxNjc3MDI5MTUxLC0xMzMyMD
g3OTYzXX0=
-->