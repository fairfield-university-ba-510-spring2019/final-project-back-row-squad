## Our Readme File

### Back Row Squad Final project.

This file will detail our project for BA510 course. In this project, our goal was to produce a database and data warehouse for Fairfield University course catalog information and scheduling. Information from the course catlogs was scraped by Dr. Huntley into a number of .csv files, in which there are three main classes of files for each term starting from Fall 2014: one is a listing of courses offered during the specific term (courses.csv),  one is all course meetings for all courses offered (course_meetings.csv), and two remaining csv files which detail information about programs, classes in these programs, and information regarding prerequesets, corequesets, and more (CourseCatalog.csv). A more detailed explanation of these files is given later in this file. Using data from these files, we built a reltional database, `CourseData.db` and a datawarehouse, `CourseDataWarehouse.db`, to store this data efficiently.  

Our project followed the outline of the Instructions.md file, and can be summerized with the following steps:

__1. Created an ERD that outlines the structure of our `CourseData.db` database

__2. Transitioned the ERD into the `CourseData.db` file, which will house all of our data in a relational database.

__3. Imported .csv data into `CourseData.db` and filled our database tables with corresponding .csv data.

__4. Created document `CourseDataTests.ipynb` to test the integrity of our `CourseData.db`.

__5. Designed and built a data warehouse called `CourseDataWarehouse.db`.

__6. Created document `CourseDataWarehouseTest.ipynb`. to test the integrity of our datawarehouse. 

__7. Created document `CourseDataWarehouseDemo.ipynb` that contains query demos which illustrates the usefulness of the data warehouse.


Next, we go into detail for each step, describing our thought process and explanations.


## Step 1:

Our first step was to build an Entity Relationshp Diagram, or ERD, which outlines the table structure and relationships between tables. Our data was stored in 40 csv files, which are contained in the `SourceData` folder. Within `SourceData`, there are more folders for each semester and term, and for each of these folders, there are two .csv files: `course_meetings.csv`, and `courses.csv`. Here is the structure of each file:

- `course_meetings.csv`: information regarding all courses and their respective meetings during the term. Columns are crn, location, day, start end
- `courses.csv`: information regarding all courses offered during a term and their respective components, such as building, professor, timecodes, etc. Columns are: term, crn, catalog_id, section, credits, title, meetings, timecodes, primary_instructor, cap, act, rem. 


Additionally, there are two more .csv files used for data, found in the Catalogs Folder. For these two files, there is information about different programs in the University. These columns are: program_code, program_name, catalog_id, course_title, credits, prereqs, coreqs, fees, attributes, description.

From this data, we designed a database architecture that is modeled in our `CourseDataERD.PDf`. It is posted to the docs folder Here is our file.
![ERD for Our Database](docs/CourseDataERD.PDF)

The contents for each column of data are described in our **[`CourseDataDictionary`]('docs/CourseDataDictionary.md')**. 

From the diagram, our entities are the following:
 - COURSE: information regarding the university's courses from Fairfield's (combined undergraduate and graduate) catalogs.
 - COURSE_OFFERING: information about the unique undergraduate and graduate courses offered at Fairfield.
 - CLASS_MEETINGS: information about the actual meetings that classes have. 
 - LOCATION: information about where university courses take place.
 - FACULTY: information about the instructors/faculty of the university.
 - PROGRAMS: information about the programs in which courses are associated with that the university offers.


## Step 2:

Our second step was to transition the ERD entities into tables in the `CourseData.db` file. To begin, we create the actual database file. In subsequent cells, for reproducability, we drop tables first and then create the table with its corresponding columns. Code for these actions is found in cells 4-9 in the **[CourseDataETL]('`CourseDataETL.ipynb`')** notebook. 

## Step 3a:

The first part of our third step was to import our raw data into our database. This acts akin to an intermediate step. In order to populate our database tables with the .csv files, we import the .csv files as a table in our database with the prefix of 'IMPORT_' and then the name of specific .csv file of the differnt folders of the different semester folders. Code for this process can be found in cell 12 of the **[CourseDataETL]('`CourseDataETL.ipynb`')** notebook. 

## Step 3b:

Our second part of our third step was to populate our ERD tables. For this step, we used the data from the 'IMPORT_' tables referenced in Step 3 to populate our ERD tables. Code for this process can be found in cells 18-28 of the **[CourseDataETL]('`CourseDataETL.ipynb`')** notebook. Further, as shown in our cell 29 **[CourseDataETL]('`CourseDataETL.ipynb`')** notebook, we drop the 'IMPORT_' tables to remove the unnecessary tables and thus reduce the size of our file to enable us to 'git push'.

## Step 4:

Our fourth step was test for integrity of our `CourseData.db`. We created a new notebook, `CourseDataTests.ipynb`, which containes examples of SQL SELECT queries, which checks for domain integrity (see cells 5-6), entity integrity (see cells 7-17), and referential integrity (see cells 18-21). Since one of our partners is an instructor at the university, we decided to model our queries to answer some questions she would want to answer. Examples of these queries are in the `CoruseDataTests.ipynb`. 

# Step 5a:

The first part of our fifth step was to design a data warehouse called `CourseDataWarehouse.db`. We utilized a star schema design with CLASS_FACTS_W as our facts table. The 4 dimensions tables we created in our data warehouse database are: 1. TERM_W, which contains attributes for semester, year and term; 2. COURSE_W, which contains attributes for CRN, credits, prerequisites, corequisites, attributes, decription, program name and program code; 3. FACULTY_W, which contains attributes for the last name and first name of each faculty member; and 4. LOCATION_W, which contains attributes for building and room. Our star shema ERD is called `StarSchemeERD.pdf`. It is posted to the docs folder. Here is our file.
![ERD for Our StarSchema](docs/StarSchemaERD.PDF) 

# Step 5b:

The second part of our fifth step was to build a data warehouse called `CourseDataWarehouse.db`. We created and populated the dimension tables first. Note that we have an bug in our FACULTY_W table. Then we created and populated the fact tabke, named: CLASS_FACTS_W.

# Step 6:

Our sixth step was to test our data warehouse called `CourseDataWarehouse.db` for data integrity. We included integrity checks for Domain, Entity and Relational Integrity as we did for the first database. Our work is included in the notebook, `CourseDataWarehouseTests.ipynb`. 

# Step 7:

Our seventh step is to demonstrate our results with useful queries. To do so, we attempted to replicate the queries used by Filip's Angels - but using our faculty member teammate (Dawn Massey), rather than Dr. Huntley. Our work is included in the notebook, `CourseDataWarehouseDemo.ipynb`. Our questions include the following: 1. What course has Massey taught the most? 2. Which semester did Massey teach the most hours? 3. In which classroom has Massey taught the most? 4. On which day has Massey taught the most hours? 

# Step 8:

Our eighth and final step - before going out for some much-deserved drinks with our classmates - is to deliver a walkthrough presentation of our work. We will review this read.me file in class and link to the other files as necessary to demonstrate our work. We also will answer Dr. Huntley's questions about our processes and work.