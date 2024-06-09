# nosql-challenge

## UK Food Standards Analysis

This project provides an in-depth analysis of the UK Food Standards Agency's food hygiene ratings data. The analysis is divided into three key parts: setting up the database, updating the database with new and corrected information, and performing exploratory data analysis to answer specific questions posed by the food magazine Eat Safe, Love.

### File structure

```
nosql-challenge/
├── Resources
│   └── establishments.json         # JSON file containing the raw data for UK
├── NoSQL_setup.ipynb               # Jupyter Notebook for database setup and updates
├── NoSQL_analysis.ipynb            # Jupyter Notebook for data analysis
└── README.md                       # This README file
```

### What do you need?

- Python 3.x
- Jupyter Notebook
- MongoDB
- PyMongo
- Pandas

### Part 1: Database and Jupyter Notebook Set Up

In this section, I successfully set up a MongoDB database and imported the provided establishments.json data for analysis.

1. Data Import:

   - The data was imported into a MongoDB database named uk_food and the collection was named establishments.
   - The command used for import was:
     ```
     mongoimport --type json -d uk_food -c establishments --drop --jsonArray D:\Data_Boot_Camp\Module_12_challenge\nosql-challenge\Resources\establishments.json
     ```

2. Notebook Initialization:

   - Libraries such as PyMongo and Pretty Print (pprint) were imported to interact with MongoDB and format outputs.
   - An instance of the MongoClient was created, and a connection to the uk_food database was established.

3. Data Verification:

   - I confirmed the creation of the 'uk_food' database and the presence of the 'establishments' collection.
   - I successfully displayed a sample document from the collection to ensure the data was loaded correctly.

### Part 2: Update the Database

In this section, I made several updates to the database as requested by the magazine editors.

1. Adding New Establishment:

   - A new halal restaurant, "Penang Flavours," was added to the establishments collection with the following details:

   ```
     {
        "BusinessName": "Penang Flavours",
        "BusinessType": "Restaurant/Cafe/Canteen",
        "BusinessTypeID": "",
        "AddressLine1": "Penang Flavours",
        "AddressLine2": "146A Plumstead Rd",
        "AddressLine3": "London",
        "PostCode": "SE18 7DY",
        "LocalAuthorityName": "Greenwich",
        "geocode": {
            "longitude": "0.08384000",
            "latitude": "51.49014200"
            },
        "NewRatingPending": true
     }
   ```

2. Updating BusinessTypeID:

   - I identified the BusinessTypeID for "Restaurant/Cafe/Canteen" and updated the "Penang Flavours" document with this ID.

3. Removing Dover Establishments:

   - Establishments within the Dover Local Authority were counted and subsequently removed from the collection.
   - The removal was verified by recounting the documents to confirm the deletion.

4. Data Type Corrections:

   - Latitude and longitude fields were converted from strings to decimal numbers using the update_many method.
   - The RatingValue field was converted from strings to integers, handling any non-numeric values appropriately.

### Part 3: Exploratory Analysis

This section involved performing specific queries to answer questions for Eat Safe, Love.

1. Establishments with Hygiene Score 20:

   - I queried for establishments with a hygiene score of 20.
   - The query returned 41 establishments, which were displayed in a Pandas DataFrame.

2. High-Rated Establishments in London:

   - I found establishments in London with a 'RatingValue' of 4 or higher.
   - The search used a regular expression to accommodate various names for the London Local Authority.
   - The query identified 34 establishments meeting the criteria, with details displayed in a DataFrame.

3. Top Establishments Near "Penang Flavours":

   - I identified the top 5 establishments with a 'RatingValue' of 5, sorted by the lowest hygiene score, near "Penang Flavours".
   - The nearest locations were determined by comparing geocode coordinates within 0.01 degrees of latitude and longitude.
   - The results showed 5 establishments meeting these criteria, displayed in a DataFrame.

4. Local Authorities with High Hygiene Issues:

   - Using aggregation, I counted the number of establishments with a hygiene score of 0 in each Local Authority.
   - The results were sorted from highest to lowest, revealing that the top Local Authority with the highest number of hygiene issues was Thanet, with 1,130 establishments.

### How to use the code?

1. Clone this repository to your local machine
2. Open the Jupyter Notebook:
   - Navigate to the project directory and open the Jupyter Notebook files.
   - Open NoSQL_setup.ipynb for Parts 1 and 2, and NoSQL_analysis.ipynb for Part 3.
3. Run the Notebook:
   - Execute each cell in sequence to perform the database setup, updates, and analysis.

### Summary of Findings

- The UK Food Standards Agency data provided valuable insights into the hygiene ratings of various establishments across the UK.
- Specific queries helped identify establishments with notable hygiene scores and those with high ratings in strategic locations such as London and near "Penang Flavours."
- Data cleanup and type conversion ensured the integrity of the analysis and facilitated accurate query results.
