# Miniproject 2

### [Assignment](assignment.md)

## Project/Goals
This project pull data from Foursquare, Yelp, and Google APIs to retrieve information about specific types of places within a set distance of a location. It then organizes and cleans said data and uses it to create an SQL database, in addition to outputting Pandas DataFrames. Also contained is a rudimentary function to automatically create SQL tables using dictionary keys as column names.

## Process
#### The first step was pulling data from the Foursquare API and organizing it into a list of dictionaries of the same size. Difficulties included replacing missing rating and popularity data for a variety of places, but the ability to narrow what fields Foursquare returns directly within the API call made this a fairly easy process. From there, setting up a SQL database and table was straightforward, while inserting values required a for loop and some playing around with quotation marks in python.
#### Second was pulling data from Yelp. After pulling the intial data from a simple search API call, I had to set up a loop to iterate through the id of each place and make another API call for each place, as some of the desired information was not returned from the general search. Data from the search and business details API calls was then combined into a list of dictionaries used to create another SQL table and pandas DataFrame. The process for creating the SQL table was essentially identical to the process for Foursquare, making the process easy once data was properly formatted.
#### Third was repeating the process with Google's API. It was fairly similar to Yelp's process, requiring a loop to make additional API calls to retrieve additional information. This additional information was combined with the initially returned information from the search in the same loop.
#### Fourth, I went back and refactored my code into a function that takes data, a connection, and table name as inputs, and creates a SQL table with the specified name and column names derived from dictionary keys. Additionally, the types of each column are derived from the data types in python by creating a dictionary with column names as keys and the SQL equivalents of each column's data type, stored as strings, as values.
#### Lastly, I went and created a table containing more detailed Category information retrieved from the Foursquare API. The main difficulty here was that SQLite does not allow for adding Foreign Keys to an already-existing table, and instead requires Foreign Keys to be specified at table creation. A slight modification of the above-created function to create SQL tables allowed for this, but would ideally be handled differently going forward.

## Results
#### While Foursquare has the best method for sorting the popularity of places, using a scale that takes into account data from the last 6 months where data from farther back in time is weighted less, and the most granular rating data (using tenths of points on a scale from 1 to 10), it also has the most missing rating data by far (nearly half of the places I pulled information for). Google, on the other hand, only returns 40 places in the specified search area, and it does not allow for increasing the limit on places returned. Yelp returns information on the most places, and does not generally have missing information on them, making it appear to be the best source overall.

## Challenges 
#### *API calls: each API had a different format they required for using API keys, in addition to different structures to their stored data. Parsing through it took a while.
#### *Missing data: finding and handling missing data took some time.
#### *Creating SQL tables: while the process for creating SQL tables was fairly straightforward, it was also fairly tedious. Creating a function to automatically create them based on a python list of dictionaries took a fair amount of time and messing around with f-strings to make sure SQL was getting queries it could understand.

## Future Goals
#### With more time, I would ideally change my function to create SQL tables to take another argument allowing the user to specify a column to be a foreign key.