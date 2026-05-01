# pandas-movie-analysis
<p align="center">
  <img src="https://github.com/user-attachments/assets/0ba21105-6f44-473f-9977-a9f953743892" 
       alt="mermaid-diagram" 
       width="90%" />
</p>
🧹 Data Cleaning Workflow
🔹 1. Removing Duplicate Rows
df.drop_duplicates(subset='id', inplace=True)

✔ Ensures each movie has a unique id.

🔹 2. Dropping Unnecessary Columns

Removed irrelevant columns:

adult, imdb_id, homepage
video, poster_path, original_title

✔ Reduces noise and improves dataset clarity.

🔹 3. Converting JSON Columns to Python Objects
import ast
df['column'] = df['column'].apply(
    lambda x: ast.literal_eval(x) if pd.notnull(x) else []
)

✔ Converts stringified JSON into usable Python objects.

🔹 4. Data Type Conversion
df['release_date'] = pd.to_datetime(df['release_date'], errors='coerce')
df['budget'] = df['budget'].astype('float64')
df['popularity'] = df['popularity'].astype('float64')

✔ Ensures correct data types for analysis.

🔹 5. Flattening Nested Data

Extracted meaningful values from:

🎭 Genres
📦 Collections
🌍 Languages
🏢 Production Companies
🌎 Production Countries
🔹 6. Processing Credits Dataset (df2)

Split into:

cast
crew
🔹 7. Extracting Important Information
🎭 Cast
Extracted actor names and characters
🎬 Director
Extracted director name from crew data
🔹 8. Data Validation Before Merge

✔ Verified consistency using id
✔ Ensured alignment across:

Movies dataset
Cast dataset
Crew dataset
🔹 9. Handling Missing Values
Data Type	Strategy
Numerical	0 / Median
Categorical	'Unknown'
Lists	[]
🔹 10. Merging Datasets
df = df.merge(cast, on='id', how='left')
df = df.merge(crew, on='id', how='left')

✔ Combines all relevant information into one dataset.

🔹 11. Rearranging Columns

✔ Structured for readability:

Basic Info
Financial Data
Production Details
Cast & Crew
🔹 12. Saving Cleaned Dataset
movies_metadata_cleaned.csv

✔ Final cleaned dataset ready for use.