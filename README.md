# Comparing Airports and Their Hospitality

By: Tommy Hvidhyld and Chloe Li

## Extraction:

In order to compare airports throughout the world and the quality of hospitality that is nearest to these airports, we extracted two sets of data. The first set of data is a CSV file of airport ratings. This CSV file was taken from the "Awesome Public Datasets" located on github. The second set of data was produced by an API call from Google Places in order to get the first hotel names and respective ratings that match with each airport.

## Transformation:

Using pandas, we read the CSV into a workable dataframe.

This dataframe contained many unnecessary columns in relation to our project so it was cleaned out leaving us with a dataframe of only the airport names and airport ratings. The data was collected by individual rating scores, so each airport had multiple entries. To best capture an airport's overall score was to get the mean of these entries. 

![Screen Shot 2022-12-21 at 9 44 17 PM](https://user-images.githubusercontent.com/113069752/209051012-f972a99f-8541-4fe5-a258-5edecd3457a8.png)

At this point we dropped all airports with NaN ratings. We also chose to focus on airports with an average overall rating of at least 5 out of 10. All airport names were then put into a list. With our final goal of gathering hotel information nearest to this airports, we needed to find the latitude and longitude for each individual airport. In order to do this we used a loop through the Google Geocode API.
        
![Screen Shot 2022-12-21 at 4 37 37 PM](https://user-images.githubusercontent.com/113069752/209050504-502523a7-484f-447e-9ed1-cb6a1fc83923.png)

This loop gave us a list of latitudes and longitudes for each airport while also dropping airports that 'failed' from the dataframe. The next step was to use Google Places API to grab the hotel name and rating. Using the latitudes and longitudes found earlier, a loop was created to capture a list of each hotel and its rating.
        
![Screen Shot 2022-12-21 at 4 39 18 PM](https://user-images.githubusercontent.com/113069752/209050525-fe84029b-033a-48cc-9f17-16554a461545.png)

These lists were put into a new dataframe with two columns of hotel names and ratings. Both dataframes; airports and hotels were given an id column for easier joining later.
        
## Load:

At this point we created a new database to store our data in pgAdmin. The database was name airports_db with two tables named airports and hotels. Each one was created with a "id" as the primary key.
    
![Screen Shot 2022-12-21 at 4 48 10 PM](https://user-images.githubusercontent.com/113069752/209050699-3ec0ca16-23f4-4785-bc1b-8f1e4f593ee4.png)

If we wanted to gather information from both tables in our database we would run a join that looks like this:

![Screen Shot 2022-12-21 at 10 04 59 PM](https://user-images.githubusercontent.com/113069752/209053330-3dea28da-6fb0-4304-ac45-3487cc9cb029.png)

