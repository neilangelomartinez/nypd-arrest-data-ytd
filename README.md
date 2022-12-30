### NYPD Arrest Data

**Year to Date (2022)**

![](RackMultipart20221230-1-jlgznu_html_2748009eabfe57d9.png)

_Interact with the dashboard here:_[https://www.novypro.com/project/nypd-arrest-data-2](https://www.novypro.com/project/nypd-arrest-data-2)

### Introduction

This study aims to analyze and recognize patterns and trends in New York City police enforcement activity as represented in statistics on arrests made by the NYPD. The information comprises the type of crime, the location and date of enforcement, and perpetrator demographics. By examining this data, it is intended to obtain insight into the nature of police activity in the city and how it may change depending on criteria.

### Data sources

The data for this project was collected from the New York City Police Department's NYPD Arrest Data (Year to Date) dataset. This dataset comprises records of every arrest made in New York City by the NYPD during the current fiscal year and is updated quarterly.

· _Why is this data collected?_ This is a breakdown of every arrest effected in NYC by the NYPD during the current year.

· _How is this data collected?_ This data is manually extracted every quarter and reviewed by the Office of Management Analysis and Planning.

· _What does each record represent?_ Each record represents an arrest effected in NYC by the NYPD and includes information about the type of crime, the location, and the time of enforcement.

· _How can this data be used?_ In addition, information related to suspect demographics is also included.

· _What are the idiosyncrasies or limitations of the data to be aware of?_ This data can be used by the public to explore the nature of police enforcement activity.

Please refer to the attached data [footnotes](https://data.cityofnewyork.us/api/views/uip8-fykc/files/62a746df-66ca-4603-aae4-46c02bac2972?download=true&filename=NYPD_Arrest_Incident_Level_Data_Footnotes.pdf) for additional information about this dataset.

### Data cleaning and preparation

The main tool that is used for data analysis is Power BI. The NYPD Arrest Data (Year to Date) dataset needed to be cleaned and processed before analysis could begin. This involved several processes, including:

1. Removed Errors

2. In the LAW\_CAT\_CD (level of offense) column, the values only include a single letter, with "F" representing a felony, "M" representing a misdemeanor, "I" representing an infraction, and "V" representing a violation. _Replace values_ were used to replace those values to show their meaning. The blank values were also replaced with "Unclassified". However, there is a value of "9" that does not correspond to any of these categories and should be removed.

![](RackMultipart20221230-1-jlgznu_html_5abbaf55c0e38619.png) ![](RackMultipart20221230-1-jlgznu_html_d1e98ebb10f1ad6b.png)

3. Replaced values of ARREST\_BORO (Borough of arrest) column. B(Bronx), S(Staten Island), K(Brooklyn), M(Manhattan), Q(Queens).

![](RackMultipart20221230-1-jlgznu_html_25813e361d86ec73.png)

4. Added a conditional column to show the jurisdiction responsible for the arrest. Jurisdiction codes: 0(Patrol), 1(Transit) and 2(Housing) represent NYPD whilst codes 3 and more represent non-NYPD jurisdictions

![](RackMultipart20221230-1-jlgznu_html_1abb36d7551c1f7a.png)

5. Replaced Values of PERP\_SEX column, F to Female and M to Male.

![](RackMultipart20221230-1-jlgznu_html_994b815d86240b4b.png)

6. Remove columns: X\_COORD\_CD, and Y\_COORD\_CD since there's already Latitude and Longitude for Global Coordinate System.

7. To make values uniform, change the text format to _Capitalize Each Word_ for all text columns.

![](RackMultipart20221230-1-jlgznu_html_4435193f9c6af0fc.png)

8. The shape map that will be created later on for the dashboard needs to show only New York. NYC Open Data provides a JSON file providing a map of New York. Click on GeoJSON to download the file.

![](RackMultipart20221230-1-jlgznu_html_2c194651d2b86b4.png) NYC Open Data website

9. After downloading the file, it should be imported into [mapshaper.org](https://mapshaper.org/) and converted to TopoJSON format. This is necessary since Power BI only supports TopoJSON for shape maps.

![](RackMultipart20221230-1-jlgznu_html_90acca161b6cf7b2.png)

10. Click Export on the rightmost part of the website. A message box will appear, select TopoJSON, and then click Export.

![](RackMultipart20221230-1-jlgznu_html_772e2561903fa990.png)

11. To show which day of the week has the most number of arrests, go back to the Power Query editor and duplicate the table. Then, use the Group By function. Select Day Name and then Count for the aggregate function.

### Data exploration and visualization

1. Starting with the shape map, import the JSON file that was downloaded by clicking on _Get Data_ and then selecting JSON.

![](RackMultipart20221230-1-jlgznu_html_53ed3711eaddd522.png)

2. Go to the _Model_ tab and then drag the _precinct_ column from the NYPD to the main table to have a relationship.

![](RackMultipart20221230-1-jlgznu_html_ffe29a8243b4550b.png)

3. Next, add a shape map to the dashboard. Shape maps need to be turned on from the settings (File\>Options and Settings\>Options\>Global\>Preview Features). After adding the shape map, add _Precinct_ to the Location, and then in Color saturation add the _number of arrests_. Go to the Visual tab, change Map type to Custom map and then upload the converted TopoJSON file.

![](RackMultipart20221230-1-jlgznu_html_3eae06d44cf969b1.png) ![](RackMultipart20221230-1-jlgznu_html_ed405ea84d6c30d3.png)

The shape map should look like this:

![](RackMultipart20221230-1-jlgznu_html_96795b51d104dc16.png)

4. The next chart to add is a ribbon chart, which is a type of chart that shows trends over time and can be used to compare multiple series of data. To create the ribbon chart, add the _Arrest Date_ column to the X-axis, _Arrests_ in the Y-axis, and _Borough_ to the Legend. This will allow us to see how the number of arrests varies over time for each borough.

![](RackMultipart20221230-1-jlgznu_html_7ebfab087d13285c.png) ![](RackMultipart20221230-1-jlgznu_html_c780ecc3ab5b687d.png)

5. There are different kinds of levels of offenses, which can be shown by using a funnel chart.

6. Next, three filters are added: Borough, Precinct, and Jurisdiction.

![](RackMultipart20221230-1-jlgznu_html_93ebf7aa2eb33c0d.png)

7. Two cards have been added to display the borough with the highest number of arrests at the current time and the day of the week with the most arrests. For the card showing the highest number of arrests, add a filter on the visual and choose filter type to _Top N_, input Top 1 and then choose _Max of Count_ under _By value_.

![](RackMultipart20221230-1-jlgznu_html_5354c2d4ad9aa48.png)

Interactions for these cards have been disabled, so they will not be affected by any changes made to filters.

![](RackMultipart20221230-1-jlgznu_html_821a880bf97700e5.png)

8. The next dashboard, called the "Perp Dashboard," displays information about the demographics of the perpetrators. It includes two stacked bar charts for the Perp Age Group and Perp Race, a pie chart for the Perp gender, and a bar chart that shows all offenses. All of these charts are used to visualize the data about the perpetrators.

![](RackMultipart20221230-1-jlgznu_html_a9412c3f8528d5e3.png)

9. All charts are now placed in the dashboard. After editing the theme and the background, here are the final dashboards:

![](RackMultipart20221230-1-jlgznu_html_1298b981eea15de9.png)

![](RackMultipart20221230-1-jlgznu_html_a96e97b2d17aae0e.png)

![](RackMultipart20221230-1-jlgznu_html_d8078238ead602d3.png)

### Insights

1. Brooklyn has the largest number of arrests among New York City's five boroughs during the first three quarters of 2022, with a total of 38,064 arrests. The Bronx had the second largest number of arrests, with 32,307, followed by Manhattan (34,580), Queens (29,038), and Staten Island (6,247). There could be a variety of reasons why some boroughs had higher arrest rates than others. It might be brought on by factors like population density, socio-economic status, the presence of various businesses or industries, or the performance of local law enforcement.

2. With a total of 74,915 arrests throughout the first three quarters of 2022 in New York City, it appears that misdemeanors accounted for the majority of those. Although misdemeanors generally are less serious than felonies, they can still result in serious penalties including fines and jail time. With 63,227 arrests, felonies had the second largest number of arrests. Felonies are more serious offenses that can result in longer jail sentences and harsher punishments. With only 1,362 arrests for unclassified offenses, the number of arrests was quite low. Unclassified offenses are crimes that do not fall into a defined category and are often handled on a case-by-case basis.

3. According to the data, it appears that Black people accounted for the race in New York City with the highest number of arrests during the first three quarters of 2022, totaling 69,531. Also, 82.5% of perps arrested are male. With 80,873 arrests, the age group of 25 to 44 had the most arrests. The two most common offenses were assault and petit larceny/petty theft.

### Recommendation

It would be helpful for police departments and city officials to think about implementing strategies into action that address any potential causes of high arrest rates for specific offenses, such as addressing underlying social and economic factors that may contribute to crime, enhancing the efficiency of law enforcement efforts, and allocating more funds for crime prevention and intervention programs. Additionally, it would be crucial to keep an eye on arrest statistics and other crime data to spot any changes or patterns over time and assess the success of any applied strategies.

### References

NYC Open Data (2022). GIS data: Boundaries of Police Precincts. Police precincts. [https://data.cityofnewyork.us/Public-Safety/Police-Precincts/78dh-3ptz](https://data.cityofnewyork.us/Public-Safety/Police-Precincts/78dh-3ptz)

Police Department (NYPD) (2022). NYPD Arrest Data (Year to Date). [https://data.cityofnewyork.us/Public-Safety/NYPD-Arrest-Data-Year-to-Date-/uip8-fykc](https://data.cityofnewyork.us/Public-Safety/NYPD-Arrest-Data-Year-to-Date-/uip8-fykc)

**Visit my website:** [https://bit.ly/neilmartinez](https://bit.ly/neilmartinez)

**BI Portfolio:** [https://bit.ly/neilmartinez-novypro](https://bit.ly/neilmartinez-novypro)

**Check out my other blogs:** [https://bit.ly/neilmartinez-medium](https://bit.ly/neilmartinez-medium)

**LinkedIn** : [https://bit.ly/neilmartinez-linkedin](https://bit.ly/neilmartinez-linkedin)