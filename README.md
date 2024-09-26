# Data Sourcing Challenge

## Overview
The code produced in this assignment, retrieve_data.ipynb, can be used to prepare a dataset for a prediction system to help the NOOA Space Weather Prediction Center predict Geomagnetic Storms (GSTs).

## Description
The code first starts by gathering data from NASA on Coronal Mass Ejections (CMEs) and then gathering NASA data on GSTs.  The files are then merged, reviewed, analyzed, and a dataset exported as a csv file.

## Coronal Mass Ejections Data
To retrieve the CME data a **GET** request is submitted and the response is converted to JSON with both stored as variables. The JSON is then converted to a Pandas DataFrame. The DataFrame is cleaned by removing null values and extracting linkedEvents from the dictionary stored in the column. This is achieved by a loop which extracts the value from the dictionary and creates a new row in the DataFrame for each value item in the dictionary. The DataFrame is further refined by converting startTime to datetime and the GST_ActivityID to a string. The DataFrame is then filtered for just rows where 'GST' is present in the GST_ActivityID column.

## Geomagnetic Storms Data 
A similar process to CME data is performed to retrieve GST DataFrame with CME_ActivityID created. To separate the linkedEvents in the dictionary the Pandas **explode()** method is used.   

## Merge and Export Dataset
Once the DataFrames are retrieved, they are merged with matches on gstid to CME_ActivityID and cmeID to GST_ActivityID.  The merge shows 61 common records. GST to CME start times are compared to show an average difference of 2 days. The ending DataFrame is exported as a csv file.