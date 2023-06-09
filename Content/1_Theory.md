### Fundamentals of Geographic Information Systems (GIS)

# Theory 1: Georeferencing & digitizing

## Digitizing
When some kind of urban development happens, the data we use in GIS needs to updated. Someone has to go in and updated the changes to the roads, buildings, and others. This would be done by digitizing the changes, which is the process of converting geographic data into digital form. 

For this practice we are going to use the Nokia Arena development in Tampere, as you can see below, there have been a significant amount of changes with this project.

- Picture

And if we look at the data set we are working with, you can see that some of the demolished buildings are still present and new buildings lacking. 

- Picture 

In practice, updating this new development would consist of removing the old buildings from the data, and digitizing the new buildings which would mean making new buildings in the data by tracing the buildings from some kind of reference picture. 

In this case we could potentially use the google imagery of the area, as this has already been updated. But this is not always the case, and satellite imagery is not the most accurate as the resolution is not high enough and pictures are taken at an angle. To get the most accuracy, we would survey the area and record the locations using high-accuracy equipment. But for our purpose we don't require high accuracy and we will use the following project plan as a source for the digitizing. 

- Picture

This source is however missing geographic data, as it is just a picture taken from a PDF. To align this picture with our geographic data, we need to apply a process called georeferencing. 

## Georeferencing
- More points + more spacing == better?
So, what needs to happen if the data is not up to date anymore? 
<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyJZT2R0VUthcGVodDFMQ2c0Ijp7In
N0YXJ0Ijo5OSwiZW5kIjo5OSwidGV4dCI6IlBpY3R1cmUifSwi
YVVLWFpmbjZyVTJHUW43ayI6eyJzdGFydCI6OTksImVuZCI6OT
ksInRleHQiOiJQaWN0dXJlIn19LCJjb21tZW50cyI6eyJIRTU3
SVFoa3lVUnlvb1VQIjp7ImRpc2N1c3Npb25JZCI6IllPZHRVS2
FwZWh0MUxDZzQiLCJzdWIiOiJnaDo0MDMwNDc4OCIsInRleHQi
OiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODYyOTA4MzA5Mz
F9LCJYV3d5Um5CM2o5UUI4REFCIjp7ImRpc2N1c3Npb25JZCI6
ImFVS1haZm42clUyR1FuN2siLCJzdWIiOiJnaDo0MDMwNDc4OC
IsInRleHQiOiJBZGQgcGljdHVyZSIsImNyZWF0ZWQiOjE2ODYy
OTA5MzkyODZ9fSwiaGlzdG9yeSI6WzE3MTYyMDc1NzUsMTYzOT
M4ODM2Nl19
-->