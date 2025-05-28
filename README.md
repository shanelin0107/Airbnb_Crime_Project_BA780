# Airbnb_Crime_Project_BA780
## Objective
Problem Statement
1.Aim to investigate the correlation between Airbnb listings and crime rates in Chicago by analyzing crime trends across neighborhoods, mapping Airbnb distribution, and assessing the relationship between listing density and specific crime types.

2.The study will evaluate how the increase in Airbnb listings affects local crime rates, taking into neighborhood safety, house price and police presence to provide a comprehensive understanding of the dynamics involved.

3.Based on the findings, the research will offer actionable recommendations for policymakers to effectively manage Airbnb growth while enhancing neighborhood safety and overall community well-being

## Data Overview
Overview
This data came from two different data sources. The first one is Airbnb listing data from 'Inside Airbnb' website: https://insideairbnb.com/. In the Airbnb data, it provides information on each property listed on Airbnb in Chicago. Some key attributes usually include:

Property Details: Information such as the type of property (e.g., apartment, house), room type (entire home or shared room), number of bedrooms, bathrooms, and other amenities.

Host Information: Data on the host, including their location, response rate, whether they are designated as a superhost, and their experience on the platform.

Pricing and Availability: Nightly price of the property, additional fees (e.g., cleaning fee), availability for future bookings, and discounts for extended stays.

Reviews and Ratings: Feedback left by guests, ratings for cleanliness, communication, and overall guest experience.

Location: Geographical information such as latitude, longitude, and neighborhood, which is key for spatial analysis.

The second dataset came from the Chicago Data Portal: https://data.cityofchicago.org/. The Chicago crime dataset typically includes detailed records of reported crimes in the city of Chicago. Some key attributes include:

Crime Type and Description: General classification of the crime (e.g., theft, assault) and a more detailed description of the incident.

Location: The specific street block where the crime occurred, as well as the latitude and longitude for geographic analysis. Other geographic identifiers include the community area, ward, and police district.

Date and Time: Information about when the crime occurred, which allows for temporal analysis to identify trends by year, month, or time of day.

Arrest and Resolution: Data on whether an arrest was made and other relevant details about how the crime was resolved.

Domestic Incident: Indicator of whether the crime was related to domestic violence, which can be a significant factor in some areas

## Exploring data
In the exploratory phase, we reviewed the information and statistics of the data using the .info() and .describe()functions. We also checked for missing values in both datasets using the .isnull().sum() function. Additionally, we used the missingno library to visualize the missing values. From this visualization, we found that several fields, such as description, price, longitude/latitude, host details, and neighborhood overview, were missing, either not provided by the host, the Airbnb website, or the Chicago government. Our plan is to fill in these missing values with 'Unknown' or 'Unavailable.' For some columns that we consider important for our analysis, such as price or longitude and latitude, we plan to use simple linear regression to impute the missing prices and utilize APIs to calculate neighborhood-based measures. For columns with relatively low numbers of missing values, we plan to drop those rows with missing data, as this should not affect the quality of our results. Lastly, for columns with numerical values, such as the number of bedrooms and bathrooms, we will fill the missing values with the median or mean, depending on the characteristics of the columns.

## Data cleaning
In the data cleaning phase, we first addressed the missing longitude and latitude values in the Chicago Crime data. We filled part of the missing values by using the median longitude and latitude, grouped by block, since multiple crime incidents occurring on the same block often lacked coordinates. This method efficiently filled a portion of the missing data. For the remaining missing longitude and latitude values, we used the Geocoding API to populate their coordinates based on their block. For other missing values, if they represented a relatively small number of rows compared to the entire dataset or involved duplicate columns, we chose to drop them.

Since Location is just a combination of Longitude and Latitude, and X and Y Coordinates are two different ways of specifying locations on the Earth or a map (Latitude/Longitude - Geographic Coordinate System (GCS), X/Y Coordinates - Projected Coordinate System (PCS)), we have decided to drop these columns before merging.

For the Airbnb data, we initially focused on missing rating values. We filled these missing ratings by calculating the mean rating for each neighborhood. Several columns, such as the first review date, last review date, and property descriptions, were also blank, likely because no reviews were available or the information wasn't provided. Columns like host response rate or the number of bathrooms and bedrooms were similarly incomplete, so we filled these missing values with "Unknown" or "Not Provided." One special imputation we performed was predicting the missing property prices using simple linear regression, based on features such as bedrooms, bathrooms, beds, room_type, and neighbourhood_cleansed.

## Conclusion  

Conclusion
Conclusion for Airbnb Stakeholders, New Hosts, and Customers
Our analysis explores the impact of crime rates and neighborhood dynamics on Chicago's Airbnb market. By examining key factors such as property prices, occupancy rates, and crime levels, we offer targeted recommendations to help Airbnb stakeholders, new hosts, and customers make informed, data-driven decisions.

Key Findings:<br>
Crime Types and Hotspots:<br>

Theft is the most common crime near Airbnb listings, especially in high-traffic areas like Near North Side and Loop.
Violent crimes, such as battery and assault, are prevalent in certain high-crime neighborhoods, negatively affecting guest satisfaction and overall ratings.
High-Demand Areas Despite Crime:<br>

Near North Side, West Town, and Lake View maintain strong Airbnb demand with prices ranging from 
300, even in areas with elevated crime. This suggests that benefits like proximity to attractions can sometimes outweigh safety concerns for guests, sustaining strong demand despite higher crime rates.
Recommendations for Airbnb Stakeholders:<br>
Introduce a Neighborhood Safety Badge:<br>

Implement a safety rating or badge system to highlight properties with enhanced security features.
Prioritize listings with visible safety measures (e.g., surveillance cameras, secure entry) in search results to reassure guests.
Provide Crime Trend Data to Hosts:<br>

Equip hosts with local crime trend information to help them adjust pricing or emphasize safety features in areas with rising crime.
Enhance Security in High-Crime Areas:<br>
Collaborate with hosts in neighborhoods like Near North Side to implement safety measures such as upgraded locks and gated access.

Localized Marketing and Dynamic Pricing Campaigns:<br>
Launch targeted campaigns in areas with potential but underperformance in recent reviews.
Use crime data and guest feedback to adjust pricing strategies, offering competitive rates in less attractive areas while maintaining premium pricing where demand is sustained.

Recommendations for New Hosts (Householders):<br>

Near West Side:<br>
Start your investment in Near West Side, which offers budget-friendly properties and stable returns. The combination of lower property prices and a steady occupancy rate makes it an ideal choice for new hosts seeking an affordable entry point and consistent bookings.

Near North Side:<br>
Invest in Near North Side to maximize rental income in a high-demand area. While property prices are higher, the strong occupancy rate and excellent guest reviews make it a prime location for hosts focused on frequent bookings and premium rates.

Loop:<br>
Target long-term, high-value bookings in the Loop. The lower occupancy rate may not suit short-term stays, but it presents opportunities for attracting higher-paying guests seeking extended accommodations, with fewer turnovers.

Recommendations for Customers:<br>

Personalized Safety Tips for Different Stay Durations:<br>
Short-term guests (1-7 nights): Provide safety advice and suggest neighborhoods with lower crime rates.
Long-term guests (31-91+ nights): Recommend neighborhoods like West Town, Loop, and Lake View for a balance of safety and listing availability.

Introduce Neighborhood Safety Labels:<br>
Display safety indicators or crime statistics for each neighborhood on the platform to help guests make more informed booking decisions.

Promote Secure Properties in High-Crime Areas:<br>
Highlight listings with visible safety features (e.g., secure locks, gated access) in neighborhoods with higher crime rates to reassure potential guests.
