## Data Dictionary for CourseDataERD

The following is an explanation of tables and columns in our ERD diagram. 

## COURSE

- CID (pk): surrogate key
- Catalog_ID: identifies the department and course number for a particular course.
- Title: official title of the particular course.
- Credits: the number of credits the course offers
- SID (fk): a foreign key referencing SID in SECTION table

## SECTION

- SID (pk): surrogate key
- CRN: the Course Reference Number for a particular course
- Semester: the particular semester component taken from the original attribute 'Term' attribute in 'courses.csv' 
- Year: the particular year component taken from the original attribute 'Term' attribute in 'courses.csv'
- Meetings: information regarding standard meeting times for a particular course, including times of day, building, room numbers, and date ranges.
- Timecodes: standard days of week that course meets and its corresponding meeting times, building, and room number.
- Section: particular section for a given course.
- Cap: the capacity of students that a given course section can enroll.
- Act: the actual number of students enrolled in a given course section.
- Rem: The number of remaining seats available for a given course section.
- FID: foreign key referencing FACULTY table.


## CLASS_MEETINGS

- CMID: surrogate key
- Day: Labels for days of the week. M:Monday, T:Tuesday, W:Wednesday, R:Thursday, F:Friday, S:Saturday
- Start: start time for a particular class meeting, in ISO format.
- End: end time for a particular class meeting, in ISO format.
- SID (fk): foreign key referencing SECTION table
- LID (fk): foreign key referencing LOCATION table

## LOCATION
- LID (pk): surrogate key.
- Building: Building information taken from 'Location' attribute in 'course_meetings.csv' 
- Room_No: specific room number in a particular building taken from 'Location' attribute in 'course_meetings.csv'

## FACULTY

- FID (pk): surrogate key
- LName: last name information taken from 'primary_instructor' attribute in 'courses.csv'
- FName: first name information and middle initial taken from 'primary_instructor' attribute in 'courses.csv'