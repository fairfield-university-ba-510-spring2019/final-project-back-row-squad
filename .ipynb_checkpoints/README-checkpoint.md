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

From this data, we designed a database architecture that is modeled in our `CourseDataERD2.PDf`. Here is our file.
![ERD for Our Database](docs/CourseDataERD2.PDF)

The contents for each data are described in our **[`CourseDataDictionary`]('docs/CourseDataDictionary.md')**. 

From the diagram, our entities are the following:
 - Course: information regarding the university's courses 
 - Course_Offering: information about ???
 - CLASS_MEETINGS: information about the actual meetings that classes have. 
 - LOCATION: information about where university courses take place.
 - FACULTY: information about the instructors/faculty of the university.
 - PROGRAMS: information about the programs in which courses are associated with that the university offers.


## Step 2:

Our second step was to transition the ERD entities into tables in the `CourseData.db` file. To begin,we create the actual database file. In subsequent cells, for reproducability, we drop tables first and then create the table with its corresponding columns. Code for these actions is found in cells ??? in the **[CourseDataETL]('`CourseDataETL.ipynb`')** notebook. 

## Step 3:

Our third step was to import our raw data into our database. This acts akin to a intermediate step. In order to populate our database tables with the .csv files, we import the .csv files as a table in our database with the prefix of 'IMPORT_' and then the name of specific .csv file of the differnt folders of the different semester folders. Code for this process can be found in cells ??? of **[CourseDataETL]('`CourseDataETL.ipynb`')** notebook. 

## Step 4:

Our fourth step was test for integrity of our `CourseData.db`. We created a new notebook, `CourseDataTests.ipynb`, which are examples of SQL SELECT queries, which checks for ???, entity integrity, and referential integrity. Since one of our partners is an instructor at the university, we decided to model our queries to answer some questions she would want to answer. Examples of these queries are in the `CoruseDataTests.ipynb`. 

## Step 5:
