# Comparing Airports and Their Hospitality

Extraction:
    In order to compare airports throughout the world and the quality of hospitality that is nearest to these airports, we extracted two sets of data. The first set of data is a CSV file of airport ratings. This CSV file was taken from the "Awesome Public Datasets" located on github. The second set of data was produced by an API call from Google Places in order to get the first hotel names and respective ratings that match with each airport.

Transformation:
    Using pandas, we read the CSV into a workable dataframe.
        
        

        This dataframe contained many unnecessary columns in relation to our project so it was cleaned out leaving us with a dataframe of only the airport names and airport ratings. The data was collected by individual rating scores, so each airport had multiple entries. To best capture an airport's overall score was to get the mean of these entries. 
        
        
     
        At this point we dropped all airports with NaN ratings. We also chose to focus on airports with an average overall rating of at least 5 out of 10. All airport names were then put into a list. With our final goal of gathering hotel information nearest to this airports, we needed to find the latitude and longitude of each individual airport. In order to do this we used a loop through the Google Geocode API.
        
        

        This loop gave us a list of latitudes and longitudes for each airport while also dropping airports that 'failed' from the dataframe. The next step was to use Google Places API to grab the hotel name and rating. Using the latitudes and longitudes found earlier, a loop was created to capture a list of each hotel and its rating.
        
        
     
        These lists were put into a new dataframe with two columns of hotel names and ratings. Both dataframes; airports and hotels were given an id column for easier joining later.
        
Load:
    At this point we created a new database to store our data in pgAdmin. The database was name airports_db with two tables named airports and hotels. Each one was created with a "id" as the primary key.
    
    
    
    If we wanted to gather information from both tables in our database we would run a join that looks like this:
