# San Francisco Datasets (ETL-Project)
---
### **Objective:**
#### The purpose of this project is to collaborate as a team to:
* **Extract** - 4 different datasets (in at least 2 formats)
* **Transform** - each dataset, based on their current state
* **Load** - these non-related datasets as individual datasets as a collection into a NoSQL database
---
### **Resources:**
#### This repo contains the collaborative work for Team 1. In this repo, you will find the following: ####
#### **Code Folder** ([link here](https://github.com/SaltireSequence/ETL-Project/tree/master/Code)) ####

Containing each team member's Jupyter Notebook, that contains their respective code, used for the extraction and transformation of each team member's dataset:
| Team Member | Filename | Description |
| :- | :- | :- |
| William | `william_notebook.ipynb` | Extrating a CSV file and saving as a Pandas DataFrame, containing stats for 150<br> San Francisco restaurants, before undetaking transformation (inc. `str.replace`<br> and code to convert longitute and latitude to zipcodes) and finally converting into a<br>JSON file. |
| Caitlin | `SFzips.ipynb` | Caitlin's file, that imports 2x CSV files containing (i) Park (ii) Neighbourhood information,<br> performing transformation (inc. dropping duplicates and deleting obsolete rows), before<br> saving 2x new CSV and finally converting the contents of both CSV files to a JSON file). |
| Heesung | `Heesung_code_with_comments.ipynb` | Heesung's file, that imports 2x CSV files (i) Boba Shops in the Bay Area (ii) Pokemon Go<br> Spawns in the Bay Area. Tranformation of the datasets includes (i) removal of irrelevant<br> information, utilizing Geopy to return zipcodes, from latitute and longitude and merging<br> the two datasets using the zipcode as the join. |
| Kathryn | `Google_data.ipynb` | Kathryn used Google's API to query of every hotel located within 50,000 meters from the<br> latitude and longitude corresponding to each zip code in the original dataset |

#### **Input Folder** ([link here](https://github.com/SaltireSequence/ETL-Project/tree/master/Inputs)) ####
Contains each team members raw dataset(s), once extraction was completed, but before transformation and loading into the destination database:
| TEAM MEMBER | FILENAME | DESCRIPTION |
| :- | :- | :- |
| William | `restaurant_raw.csv` | contains data (inc. longitude and latitude) of 150 Bay Area restaurants.
| Caitlin | `Neighborhoods.csv` | contains data for San Francisco parks (inc. a score for each park and<br> it's longitude and latitude)
|  | `SFZ.csv` | contains a list of zipcodes for each neighbourhood in San Francisco.
| Heesung | `boba.csv` | contains a data for Boba merchants in the Bay Area, which includes each location's longitude and latitude.
|  | `pokemon-spawns.csv` | contains data for Pokemon Go spawns in the Bay Area - includes the longitude and latitude of each spawn<br> location, as well as a unique identifier for each Pokemon
| Kathryn | **N/A** | As Kathryn queried and API, she has no input file per se.

#### **Outputs Folder**  ([link here](https://github.com/SaltireSequence/ETL-Project/tree/master/Outputs)) ####
Containing each team member's output files, which includes JSON files (that were subsquently used to form the collections, that made the final MongoDB database) and also any output files, once transformation was completed and before conversion to JSON files:

| TEAM MEMBER | FILENAME | DESCRIPTION |
| :- | :- | :- |
| William | `will_data.JSON` | the byproduct of William's data extraction and transformation is a JSON file, used for loading in as the<br> 'Restaurants' collection of the final MongoDB database.
| Caitlin | `SF_Park_Scores.csv` | the output files of both of Caitlin's datasets, once transformation had been completed on her original input<br> files, which were `SF_Park_Scores.csv` & `SFZ.csv`.
|  | `sf_parks.json` | the output files of both of Caitlin's datasets, once transformation had been completed on her original input<br> files, which were `SF_Park_Scores.csv` & `SFZ.csv`.
| Heesung | `pika_boba.csv` | contains a CSV of both datasets, once transformation had completed and before conversion into a JSON file.
|  | `boba_pika.json` | contains the boba dataset, once zip codes had bee obtainined, using the longitude and latitude of each boba<br> shop, with help from the `geocoders` library.
|  | `boba_zip.csv` | contains the merged dataset data (clean_boba_pika_df) in JSON format, ready for loading to the MongoDB<br> database, as a collection.
|  | `pika_zip.csv` | contains the Pokeman dataset, including zip codes for each spawn location.
|  | `pika_zip.csv` | contains the Pokeman dataset, including zip codes for each spawn location.
| Kathryn | `TBC` | **CONFIRM WITH KATHRYN**
___
### **The Process:**
The objective of this project was to work as a team, as collaboratively as possible, to walkthrough the the ETL process with at least 2 datasets, from different sources (e.g Kaggle & API, in atleast 2 differeing formats (e.g JSON and CSV).

The obvious approach would to have had individual team members tackle a different stage of the ETL process, however it was collectively agreed that this approach wouldn't necessarily have the entire team empowered with the knowledge of every step of the ETL process.

Consensus was therefore reached, that each team member would go through the ETL process individually, but in parallel. **Each team member would therefore:**

- **Extract** at least 1x dataset
- Perform **transformation**, dependant on the type and state of the data, following extraction. The prerequisite being, that each team member would present their transformed data in JSON format.
- Individually **load** their JSON-formatted transformed dataset(s) into a personal NOSQL (MongoDB) data, as a sanity check, before...
- Submitting their JSON file (that has successfully parsed by MongoDB) to the team member's respective resources file.

Once each team member had successfully extracted, transformed and 'test' loaded their datasets into MongoDB, Kathryn then took the helm of the load element of the project, by uploading each team member's dataset JSON file as individual collections in a master MongoDB database.

#### **Extraction** ####
In total the team extracted 6 datasets, from 3 sources, in 2 formats:

 - **6 datasets:** stored in the [Input Folder](https://github.com/SaltireSequence/ETL-Project/tree/master/Inputs)
 - **3 sources:** we used [Kaggle](https://www.kaggle.com) and the [Google API](https://maps.googleapis.com/)
 - **2 formats:** William, Heesung and Cailin's data all derived in CSV format, whilst Kathryn's API call to Google, returned a JSON file.
 
The team describes individually, their decision behind the extract of each respective data:

 - **Heesung Extraction Notes:** In this project, I would like to find out the correlation between the boba shop rating and the number of spawn of Pokemon Go Pikachu in SF Bay Area. The dataset in the two files included the following information:
 
     - **Boba shop in bay area:**
       - id: Unique id of the boba shop
       - name : Name of the boba shop
       - rating : Yelp rating of the boba shop, on a scale of 1-5
       - address : Address of the boba shop
       - ity : City the boba shop is in
       - lat : Latitude of the boba shop
       - long : Longitude of the boba shop
    
     - **SF Bay Area Pokemon Go Spawns:**
        - id: Unique id of pokemon
        - number:unique number of pokemon character
        - lat: Latitude of the despawn location
        - long: Longitude of the despawn location
        - encounter_ms: Time encountered with Pokemon
        - diappear_ms:The time when Pokemon was disappered


 - **William Extraction Notes:** as a budding restaurant goer (and as someone who is relatively new the the Bay Area) I wanted to find data that represented restaurant data in the Bay Area, that might make for interesting analysis. I found a dataset on Kaggle that looked like it had been neglected. It is information for 150 restaurants, including address, cuisine type, price point and importantly the longitude and latitude of the restaurant. My extraction only involved downloading my dataset from Kaggle, before beginning transformation.
 
 - **Caitlin Extraction Notes:** bla, bla, bla, bla
 
 - **Kathryn Extraction Notes:** for my data, I chose to locate all of the hotels that are located in each of the zip codes in the bay area. I used the Google Places api to locate hotels within the approximately 30 miles from the latitude and longitude coordinates corresponding to each zip code. This generated about 20 hotels per zip code, of which there were 50 in the dataset.

#### **Transformation** ####
Whilst all team member's extracted there data from reputable sources, all data required a degree of data cleanup and analysis. The following transformations took place:

 - **Heesung Transformation Notes:** Once I had loaded my files, as CVS into DataFrames, I performed a series of tasks that included:
 
  **(i)** Removing irrelevant to the project<br>
  **(ii)** Using Geopy to find zip codes, using longitude and latitude<br>
  **(iii)** Merging both datasets on the zip codes column<br>
  **(iv)** Removing rows containing missing information<br>
  **(v)** Saving the cleansed DataSets, firstly as CSV and secondly as a JSON file

  | TRANSFORMATION | CODE | DESCRIPTION |
  | :- | :- | :- |
  | **DataType conversion** | `.astype(int) ` | Checking data volume for each Pokemon
  | **Filtering** | `.loc[pokemon_df["name"]=="Pikachu",:]` | Filtering on a specific   character
  | **Index reset** | `.reset_index(drop=True)` | Resetting the index on a DataFrame
  | **Geopy query** | `geopy.Nominatim` | Used to query the zip codes of corresponding longitute<br> and latitude
  | **Counting** | `.value_counts()` | Counting instances of certain Pokemon characters
  | **Purging** | `['Unnamed: 0']` | Deleting unnecessary columns
  | **JSON conversion** | `to_json` | Converting DataFrame(s) / CSV to JSON
  
  - **William's Transformation Notes:** the Hotel information dataset that I extracted from Kaggle looked to be a badly converted JSON to CSV file and contained alot of white space, obsolete characters and values from one column spilling over into a complete seperate columns cells. My objective from my transformation was to simply bring order and consistency to my data. I struggled initially to write the code to repetitively remove white space from different columns, however following alot of trial-and-error, I was able to write a simple for loop that iteracted through my DataFrame and (by referencing a list containing correct column headers) and replace the white space, with correct vaules. The other challenging element of my transformation, was using Arcgis to look up zipcodes for each restaurant, using that restaurants respectuve latitude and longitude. 
 
  | TRANSFORMATION | CODE | DESCRIPTION |
  | :- | :- | :- |
  | **CSV to DataFrame** | `pd.DataFrame` | Converting my read CSV file into a DataFrame in preparation for Transformation
  | **String replacement** | `str.replace` | Replacing white space
  | **Dropping columns / cells** | `df.drop` | Removing obsolete columns and or cells.
  | **Merging DataFrames** | `df.merge ` | Merging dataframes together, prior to JSON conversion
  | **JSON conversion** | `to_json` | Converting DataFrame(s) / CSV to JSON

- **Caitlin's Transformation Notes:** bla, bla, bla

  | TRANSFORMATION | CODE | DESCRIPTION |
  | :- | :- | :- |
  | **Drop duplicates** | `.drop_duplicates()` | Dropping duplicate values
  | **Drop NaaN** | `dropna()` | Dropping NaaN values
  | **Renaming Columns** | `[‘new_column_name]` | Renaming columns for consistency
  | **DataType conversion** | `.astype(int) ` | Converting DataType, prior to JSON conversion
  | **JSON conversion** | `to_json` | Converting DataFrame(s) / CSV to JSON

#### **Loading** ####

**Loading all datasets:** Kathryn volunteered to take all our JSON files are build the team database. Here are the steps she took:

**Kathryn Team Loading Steps:** I looped through a pandas dataframe of zip codes in San Francisco, making an api call to google places for all hotels within 50,000 feet of each zip code’s latitude and longitude equivalent:<br>
- Each of these records was added to MongoDB database called locations_mdb under a collection called “hotels”. Now all hotels can be viewed for each latitude and longitude pair.<br>
- Heesung’s data I imported to the database under a collection called ‘boba’<br>
- The remaining two dataframes I converted to JSON format from a csv by:<br> 
    - Converting each to a dictionary in “index” format<br>
    - Converting each dictionary to a JSON string<br>
    - Loading each json string into JSON format<br>
    - Inserting the data into its the MongoDB database as its own collection (resulting in “parks” and “restaurants” collections)