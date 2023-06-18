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
5. Creating a map
6. Reflect:
	- Reflecting on these questions:
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
the value -1. This is because the population within the grid cell is sufficiently small that providing the value would violate data privacy protection laws. You’ll have to clean up the data** and there are a few
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
![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/3_Exercise/3_Exercise_reclassification.png)
	- NOTE: Use a dot as a decimal separator instead of comma.
	- Check the *attribute table* that the values are correct (click the new column field name to order the values in order to see the highest and lowest values, you should only have numbers 1, 2, 3 and 4).
		- If the fields turn out empty , check that “Only update X selected features” is ticked off in the field calculator.
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

### Map outputs

12. Time to make your maps! Think of which maps would be good to describe this analysis, hints:
	- Map highlighting grid squares that have been given the classification 4 in both of the reclassified fields
	- Map with graduated symbology for reclassified fields
	- Think about whether you should include the data we removed earlier(-1 entries), would it be valuable to the viewer of the map? Is the map accurate without them? How would you visualize them? 

Don't forget to include the requirements for a good map (See Crash Course)! 

13. Optional: You can use the plugin we installed during the Crash Course, QuickMapServices (QMS), to get more basemap options
	- You can open the *Search QMS* panel using this icon, it should open below your toolbox:
![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/3_Exercise/3_Exercise_QMS_1.png)
	-  Here are some examples of basemaps you could use:
![enter image description here](https://raw.githubusercontent.com/rowan8k/fundamentals-of-gis/master/Assets/3_Exercise/3_Exercise_QMS_2.png)
	- Note: These are online sources, which means they might be slow and/or limited to certain scales


---

### Optional: Refining the analysis 

14. The analysis we’ve done above is quite coarse. You can refine it by using the following fields:
	- te_vuok_as (Households living in rental dwellings, Household life theme’s prefix te_)
		- Household life: te_taly (Households, total)
	- pt_tyott (Unemployed, Main type of activity theme’s prefix pt_)
		- Main type of activity: pt_tyovy (Labour force, total)

15.  You should use the original grid data and not the one you’ve been working with. Why?
		- You’ll have an untampered dataset and won’t lose any progress you’ve made with education and income data due to unfortunate errors. 
		- Note: The education and income fields’ total number fields have the population 18 years old and older (can you think of why?), but the totals for household and unemployment fields use different metrics: Total number of households and total number of available workforces.
		- Before tampering with the original grid file, you should save it as a new file, so you have a clean backup to fall back on. 

16. When you’ve reclassified the proportions to the quartiles, you can join the layers using the id_nro field.
	- You can select which fields to join, so you don’t have to join all the fields, just the
reclassified fields for rented dwellings and unemployment.

17. Compose a map of the results
	- How do the refined results differ from the coarser results?
	- Are these refined results enough to delineate segregated areas?
		- Would you need additional data? What data?

 



<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJlVGM4YW9CSm43emRyZjBrIjp7In
RleHQiOiJIZWxzaW5raSIsInN0YXJ0IjoyNTEsImVuZCI6MjU5
fSwiUVAxWENiQ3BSc2QwbFZxNSI6eyJ0ZXh0IjoiSGVsc2lua2
kiLCJzdGFydCI6MTIzNCwiZW5kIjoxMjQyfSwiV3Z6bnlmS0xY
dm5sRURpNCI6eyJ0ZXh0IjoicGRmIGluY2x1ZGVkIiwic3Rhcn
QiOjE4NDUsImVuZCI6MTg1N30sIkJ3ZFRwa3lIblpFQmNOclgi
OnsidGV4dCI6InBkZi1maWxlcyIsInN0YXJ0IjozMzkzLCJlbm
QiOjM0MDJ9LCI1dUhCTVNsNU1TbVpicFZqIjp7InRleHQiOiIx
LiBEb3dubG9hZCwgdW56aXAgYW5kIG9wZW4gdGhlIGV4ZXJjaX
NlIDMgZGF0YSBpbiBRR0lTIGZyb20gdGhlIGNvdXJzZSBNb29k
bGXigKYiLCJzdGFydCI6MzI1OSwiZW5kIjozMzQzfSwiNzFyUm
VWTnE5QWdhSUlnSyI6eyJ0ZXh0IjoicmVzdWx0cyIsInN0YXJ0
IjoyNzI1LCJlbmQiOjI2OTV9LCIxdVAxMEZrNVJsTm4wMkU3Ij
p7InRleHQiOiJSZXR1cm4iLCJzdGFydCI6MzE0OCwiZW5kIjoz
MTU0fSwiUzUyU1F0YzFKZDBTWFp3RCI6eyJ0ZXh0IjoicG9wdW
xhdGlvbiB3aXRoaW4gdGhlIGdyaWQgY2VsbCBpcyBzdWZmaWNp
ZW50bHkgc21hbGwiLCJzdGFydCI6NDg0NiwiZW5kIjo0ODk5fS
wiZHN4UjM5NDlHR3BLWVVHWiI6eyJ0ZXh0IjoidGhpcyIsInN0
YXJ0Ijo4NTUwLCJlbmQiOjg1NTR9LCJKdmJpVXNhdVNWTXg2S0
pVIjp7InRleHQiOiJmaWVsZCIsInN0YXJ0Ijo4MjU4LCJlbmQi
OjgyNjN9fSwiY29tbWVudHMiOnsiM0xvR0tlUUZFTVd6amJFMS
I6eyJkaXNjdXNzaW9uSWQiOiJlVGM4YW9CSm43emRyZjBrIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiVXBkYXRlIGlmIG
FwcGxpY2FibGUiLCJjcmVhdGVkIjoxNjg2NDc2NDM2ODc4fSwi
bFBrbFVGYkU0ZVUyMDM0WiI6eyJkaXNjdXNzaW9uSWQiOiJRUD
FYQ2JDcFJzZDBsVnE1Iiwic3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0
ZXh0IjoiVXBkYXRlIGlmIGFwcGxpY2FibGUiLCJjcmVhdGVkIj
oxNjg2NDc2NTc5NTY3fSwiQnVCRm1pakdpcmpFYzVVayI6eyJk
aXNjdXNzaW9uSWQiOiJXdnpueWZLTFh2bmxFRGk0Iiwic3ViIj
oiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiQWRkIHBhZ2UiLCJjcmVh
dGVkIjoxNjg2NDc2NzM2MDU1fSwiUEtCYUpaYTNkbXdsVnFGNS
I6eyJkaXNjdXNzaW9uSWQiOiJCd2RUcGt5SG5aRUJjTnJYIiwi
c3ViIjoiZ2g6NDAzMDQ3ODgiLCJ0ZXh0IjoiUmVmZXJlbmNlIi
wiY3JlYXRlZCI6MTY4NjQ3NzQ3NTg4OH0sInc3RVZTMnhNUHpS
Y0lDTGYiOnsiZGlzY3Vzc2lvbklkIjoiNXVIQk1TbDVNU21aYn
BWaiIsInN1YiI6ImdoOjQwMzA0Nzg4IiwidGV4dCI6IkFkZCBp
bnN0cnVjdGlvbnMgdG8gZG93bmxvYWQgZGF0YSB0aGVtc2Vsdm
VzIiwiY3JlYXRlZCI6MTY4NjQ3NzQ5NDEyMH0sIlB3V0k2TTBD
eUZRalBkNUwiOnsiZGlzY3Vzc2lvbklkIjoiNzFyUmVWTnE5QW
dhSUlnSyIsInN1YiI6ImdoOjIyMTY4MTU3IiwidGV4dCI6ImFu
ZCByZWZsZWN0aW5nIG9uIHRoZXNlIHF1ZXN0aW9uczoiLCJjcm
VhdGVkIjoxNjg2NzMxNTAyMjk4fSwiODdKTDVEYWZnWlRLRVJ3
USI6eyJkaXNjdXNzaW9uSWQiOiIxdVAxMEZrNVJsTm4wMkU3Ii
wic3ViIjoiZ2g6MjIxNjgxNTciLCJ0ZXh0IjoiSSB0aGluayBh
ZG1pbmlzdHJhdGl2ZWx5LCBpdCB3b3VsZCBiZSBlYXNpZXIgaW
Ygd2UgYXNrZWQgdGhlIHN0dWRlbnRzIHRvIGNvbXBsaWUgYWxs
IHRoZWlyIHJlZmxlY3Rpb25zIGludG8gYSBzaWdubGUgZG9jdW
1lbnQgdGhhdCBnZXRzIHN1Ym1pdHRlZCBhdCB0aGUgZW5kLiIs
ImNyZWF0ZWQiOjE2ODY3MzE1Njc5NjN9LCJ1Tzg0N09yMlhuYl
dIbXJFIjp7ImRpc2N1c3Npb25JZCI6IlM1MlNRdGMxSmQwU1ha
d0QiLCJzdWIiOiJnaDoyMjE2ODE1NyIsInRleHQiOiJzdWdnZX
N0ZWQgYWRkZWQgdGV4dCIsImNyZWF0ZWQiOjE2ODY3MzE2NzA5
NjR9LCJSZlFYMkI3TjljRmYycDJLIjp7ImRpc2N1c3Npb25JZC
I6ImRzeFIzOTQ5R0dwS1lVR1oiLCJzdWIiOiJnaDoyMjE2ODE1
NyIsInRleHQiOiJJIGZpbmQgdGhpcyBzbGlnaHRseSBjb25mdX
NpbmcgZnJvbSBRR0lTLiBRdWFudGlsZXMgc2hvdWxkIGJlIGZp
Y2UgZ3JvdXBzIHdpdGggZXF1YWwgY291bnRzLCBzbyB3aHkgY2
FuIHlvdSBjbmFnZSB0aGUgY2xhc3NlcyB0byA0PyIsImNyZWF0
ZWQiOjE2ODY3MzE5NDg3NzN9LCJJazRTUnlZbXZrdFVTU2s1Ij
p7ImRpc2N1c3Npb25JZCI6Ikp2YmlVc2F1U1ZNeDZLSlUiLCJz
dWIiOiJnaDoyMjE2ODE1NyIsInRleHQiOiJPbmUgdGhpbmcgdG
hhdCBJIG1lbnRpb25lZCBpbiB0aGUgR0lTIHR1dG9yaWFscyB0
aGF0IGJhc2ljYWxseSBubyBvbmUgZGlkIHdhcyBhc2tpbmcgdG
hlbSB0byB0aGluayBhYm91dCB0aGUgbnVtYmVyIG9mIHNpZ25p
ZmljYW50IGZpZ3VyZXMgKG9yIGRlY2ltYWwgcGxhY2VzKS4gRG
8gd2UgbmVlZCB0byBrbm93IHRoaXMgcHJlY2lzaW9uL2lzIGl0
IGV2ZW4gcmVhbGlzdGljPyBQZXJoYXBzIHRlYWNoaW5nIHRoZW
0gaGVyZSBhYm91dCB0aGlzIGFuZCBob3cgdG8gcmVkdWNlIHNp
ZyBmaWdzIGluIHRoZSBsZWdlbmQgd291bGQgYmUgYSBnb29kIG
lkZWEuIiwiY3JlYXRlZCI6MTY4NjczMjcyODc3M319LCJoaXN0
b3J5IjpbNzUyNTc2NTE4LC0xOTc0MjgzNDM1LC0yMDU4OTM5Nz
Y1LDEyODE0NDUyNywyNjU5ODc0MzAsMTk4MTA4NzY3LDczNjQx
OTcwOCwxMjIxMjY0NDMyLDE4MjUwMzcwNDAsLTM5MTg4MjA1MC
wtMTYzNzYwNDE3OSwtMTU2ODc2OTc2OSwxMDc1NTg4OTUyLC00
Njk2NDE2ODIsLTI2OTU1ODc4NSwtMTM2NDE3NDk5MywxNzI2OD
EzNjM0LC0xMzExNTI5NDA1LDUxNjIxMzI0OCwtMTcyNTc3MjE2
MV19
-->