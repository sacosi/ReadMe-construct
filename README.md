## Project Title - COVID-19 Research ETL

### Project Description
This project's goal is to apply the acquired ETL (extract, transform, load) learnings in class to a topic of our choice.<br/>
Our group has decided to focus this project on the major topic of the moment - Corona Virus / Covid-19.

### Project Team -Pandas in Pandemic
- Kendall Marquard
- Smiti Swain
- Luis Ramirez
- Salvador Neves
- Tejas

### ETL:

<< Insert an ETL data flow Diagram >>

<ins>**Country Table**</ins><br/>
#### Data Extraction:
The data source is a json file from https://worldpopulationreview.com/

<<<<< Insert a picture snip of the json file >>>>>>

1) Json library was used to handle the file.
2) We looped through the json to append the values to arrays previously created. 
3) From there we created a Data Frame.

#### Data Transformation:
1) Selected only the necessary fields from json file.
2) Renamed fields while storing in Data Frame
3) Set Country ID as index.

<< insert some code snippets >>
<<<<< Insert a snip of the Data Frame >>>>>


<ins>**State Table**</ins><br/>
#### Data Extraction:
The data source is wikipedia. <<< add a link to wiki >>>
<<< add a snip of the wiki table >>>

1) Pandas scraping (pandas.read_html) was used.
2) The table information sourced directly from the website was stored in a Data Frame.

<<<<< Insert a snip of the Data Frame >>>>>
#### Data Transformation:
1) The table scraped from Wikipedia had two levels of column headers so we dropped the top one.
2) Dropped columns that we don't need in the data frame.
3) Renamed columns to friendly names.
4) Used a dictionary with state abreviations and names, converted it to a dataframe.
5) Merged the state and name Data Frame with the previous data frame to add abreviations to the State Table.

<< insert some code snippets >>

<ins>**Country_Cases Table**</ins><br/>
#### Data Extraction:
The data source is an API end point https://api.covid19api.com/country/{country} 

<<<<< Insert a snip of the API data >>>>>

1) Using Requests module, response was received from the API endpoint,with start and end date as parameters.
2) Country_ID column from the Country Table was used to do call this API for every single country between January 22, 2020 and April 24, 2020.
3) The data retrived was stored in a Data Frame.

<<<<< Insert a snip of the API call code >>>>>

<<<<< Insert a snip of the Data Frame>>>>>

#### Data Transformation:

1) For the Country_Case Table we had a small issue with the API which was that for some Countries the level of information was down to the city. So in order to fix this issue, we have use an aggregator function, we grouped by Country and date and got the sum of the confirmed, deaths, recovered and active cases.
2) Converted the timestamp returned by the API to a Date format.
3) Set CountryID and Date as the index.

<< insert some code snippets >>

<ins>**US_States_Cases Table**</ins><br/>
#### Data Extraction:
The data source is an API end point https://covidtracking.com/api/v1/states/daily.json

<<<<< Insert a snip of the API data >>>>>

1) Using Requests module, response was received from the API endpoint.
2) Using JSON traversal, desired datapoints were collected and stored in lists.
3) The data retrived was then stored in a Data Frame.

<<<<< Insert a snip of the API call code >>>>>

<<<<< Insert a snip of the Data Frame >>>>>

#### Data Transformation:
1) For the US_States_Cases Table the json data returned from API was not consistent . For example , if for a day there are no positive cases , the json data did not have the key altogether. In order to fix this issue, try - except code bloack was used, when the key is now fund, and store the value as "0".
2) Converted the date returned by the API from string to Date format.

<< insert some code snippets >>

<ins>**Index_prices Table**</ins><br/>
#### Data Extraction:
The data source is "yfinance" module, which is a python library that scrapes data from Yahoo! Finance and returns the data in a DataFrame format to get free stock market data.

1) We needed to pip install yfinance.
2) We created a dictionary to hold the ticker and country code for major world indices.
2) Using a For loop , and the yfinance module, data was received for each of the ticker passed from the previously cretaed dictionary.

<<<<< Insert a snip of the Data Frame retrived from yahoo >>>>>

#### Data Transformation:
1) Data Frame returned from yfinance module did not have the Index Ticker, name and County. Using a dictionary converted dataframe and  a for loop to iterate through the dataframe , new columns were added to the main Data Frames. 
2) Reset Index on the Data Frame, that previously had Date as the index.

<< insert some code snippets >>

#### Data Load:

1) Created tables in postgres database.
2) Using sqlalchemy create-engine , connection was set up with the postgres database.
3) Using pandas to_sql(), data was inserted into the tables.

<< insert the database ERD >>

