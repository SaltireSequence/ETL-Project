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
%%html
<style>
table {float:left}
</style>
Containing each team member's Jupyter Notebook, that contains their respective code, used for the extraction and transformation of each team member's dataset:

| Team Member | Filename | Description |
| :- | :- | :- |
| William | `william_notebook.ipynb` | Extrating a CSV file and saving as a Pandas DataFrame, containing stats for 150<br> San Francisco restaurants, before undetaking transformation (inc. `str.replace`<br> and code to convert longitute and latitude to zipcodes) and finally converting into a<br>JSON file. |
| Caitlin | `SFzips.ipynb` | Caitlin's file, that imports 2x CSV files containing (i) Park (ii) Neighbourhood information,<br> performing transformation (inc. dropping duplicates and deleting obsolete rows), before<br> saving 2x new CSV and finally converting the contents of both CSV files to a JSON file). |
| Heesung | `Heesung_code_with_comments.ipynb` | Heesung's file, that imports 2x CSV files (i) Boba Shops in the Bay Area (ii) Pokemon Go<br> Spawns in the Bay Area. Tranformation of the datasets includes (i) removal of irrelevant<br> information, utilizing Geopy to return zipcodes, from latitute and longitude and merging<br> the two datasets using the zipcode as the join. |
| Kathryn | `Google_data.ipynb` | Kathryn used Google's API to query of every hotel located within 50,000 meters from the<br> latitude and longitude corresponding to each zip code in the original dataset |