# DATABASED-SYSTEM
EXAMPLE 1: 
 








// CREATE THE TABLES 

USE StudentNumberDB; 
 
CREATE TABLE Qualification ( 
    QualificationID INT AUTO_INCREMENT PRIMARY KEY, 
    QualificationName VARCHAR(100) NOT NULL, 
    Faculty VARCHAR(100) NOT NULL, 
    Level VARCHAR(50) NOT NULL, 
    Duration INT NOT NULL 
); 
 
CREATE TABLE Subject ( 
    SubjectID INT AUTO_INCREMENT PRIMARY KEY, 
    SubjectName VARCHAR(100) NOT NULL, 
    Code VARCHAR(20) NOT NULL, 
    Credits INT NOT NULL, 
    Semester VARCHAR(10) NOT NULL 
); 
 
CREATE TABLE Student ( 
    StudentID INT AUTO_INCREMENT PRIMARY KEY, 
    FirstName VARCHAR(50) NOT NULL, 
    LastName VARCHAR(50) NOT NULL, 
    DateOfBirth DATE NOT NULL, 
    Gender ENUM('Male', 'Female', 'Other') NOT NULL 
); 
 
CREATE TABLE Enrollment ( 
    EnrollmentID INT AUTO_INCREMENT PRIMARY KEY, 
    StudentID INT, 
    QualificationID INT, 
    SubjectID INT, 
    EnrollmentDate DATE NOT NULL, 
    FOREIGN KEY (StudentID) REFERENCES Student(StudentID), 
    FOREIGN KEY (QualificationID) REFERENCES Qualification(QualificationID), 
    FOREIGN KEY (SubjectID) REFERENCES Subject(SubjectID) ); 

// POPULATE THE TABLES 

INSERT INTO Qualification (QualificationName, Faculty, Level, Duration) VALUES  
('Computer Engineering', 'Electrical, Electronic and Computer Engineering', 'Bachelor', 4), 
('Electrical Engineering', 'Electrical, Electronic and Computer Engineering', 'Bachelor', 4), 
('Mechanical Engineering', 'Mechanical Engineering', 'Bachelor', 4), 
('Civil Engineering', 'Civil Engineering', 'Bachelor', 4), 
('Chemical Engineering', 'Chemical Engineering', 'Bachelor', 4);  
INSERT INTO Subject (SubjectName, Code, Credits, Semester) VALUES  
('Database Systems 3', 'DSS370S', 15, '1'), 
('Embedded Systems', 'ES320S', 15, '2'), 
('Network Systems', 'NS300S', 15, '1'), 
('Mathematics 2', 'MTH200S', 10, '1'), 
('Physics 1', 'PHY100S', 10, '2'); 
 
INSERT INTO Student (FirstName, LastName, DateOfBirth, Gender) VALUES  
('John', 'Doe', '1990-01-01', 'Male'), 
('Jane', 'Smith', '1985-05-12', 'Female'), 
('Emily', 'Davis', '1978-11-20', 'Female'), 
('Michael', 'Brown', '1992-07-08', 'Male'), 
('Sarah', 'Wilson', '1989-03-15', 'Female'); 
 
INSERT INTO Enrollment (StudentID, QualificationID, SubjectID, 
EnrollmentDate) VALUES  
(1, 1, 1, '2024-02-01'), 
(2, 2, 2, '2024-02-02'), 
(3, 3, 3, '2024-02-03'), 
(4, 4, 4, '2024-02-04'), 
(5, 5, 5, '2024-02-05'); 

 // SELECT COUNT (*) AS NumberOf Qualifications FROM Qualification;
 

// create a view to output information from any two tables 

CREATE VIEW StudentEnrollments AS 
SELECT s.FirstName, s.LastName, q.QualificationName, e.EnrollmentDate FROM Student s 
JOIN Enrollment e ON s.StudentID = e.StudentID 
JOIN Qualification q ON e.QualificationID = q.QualificationID;  


// create the query that uses the order by clause 


SELECT * FROM Student ORDER BY LastName; 



// create a query that uses the group by clause 


SELECT Gender, COUNT(*) AS NumberOfStudents 
FROM Student 
GROUP BY Gender; 



// EXAMPLE 2 :

THE GOVERNMENT DEPARTMENT HAS APPROCAHED YOU WITH THE REQUEST TO DESIGN AND IMPLIMENT A DATABASED SOLUTION . THERE ARE A NUMBER OF ENTITES IMPLIMENT DIRECTLY FROM THE GIVEN SCENARION . EACH OF THE ENTINTIES MUST HAVE AT LEAST FIVE ATTRIBUTES 


Step 1: Design the Database 
Entities and Attributes: 
Let's assume the government department is related to managing citizen services. We'll identify five entities: Citizen, Service, Department, Employee, and ServiceRequest. 
1.	Citizen: 
o	CitizenID (Primary Key) 
o	FirstName o 	LastName o 	DateOfBirth o 	Gender 
2.	Service: 
o	ServiceID (Primary Key) o 	ServiceName o 	Description 
o	DepartmentID (Foreign Key) o 	Cost 
3.	Department: 
o	DepartmentID (Primary Key) o 	DepartmentName o 	Location 
o	HeadOfDepartment (Foreign Key) o 	Budget 
4.	Employee: o EmployeeID (Primary Key) o FirstName o LastName o Position 
o	DepartmentID (Foreign Key) 
5.	ServiceRequest: 
o	RequestID (Primary Key) o 	CitizenID (Foreign Key) o 	ServiceID (Foreign Key) o 	RequestDate o 	Status 
Relationships: 
•	A citizen can request multiple services. 
•	Each service is managed by one department. 
•	Each department has multiple employees. 
•	Each service request is linked to a specific citizen and service. 
ERD: 
You need to draw an Entity-Relationship Diagram (ERD) showing the entities, primary keys, foreign keys, and relationships. Include at least one ternary relationship and an example of generalisation/specialisation if applicable. 
 
Step 2: Implement the Database 
2.1 DDL for Implementing the Database 

 
CREATE DATABASE YourLastNameDB; 
 
USE YourLastNameDB; 
 
CREATE DATABASE Smith_Government_Department; 
 
USE Smith_Government_Department; 
 
CREATE TABLE Department ( 
    DepartmentID INT AUTO_INCREMENT PRIMARY KEY, 
    DepartmentName VARCHAR(100) NOT NULL, 
    Location VARCHAR(100) NOT NULL, 
    HeadOfDepartment INT, 
    Budget DECIMAL(15, 2) NOT NULL 
); 
 
CREATE TABLE Employee ( 
    EmployeeID INT AUTO_INCREMENT PRIMARY KEY, 
    FirstName VARCHAR(50) NOT NULL, 
    LastName VARCHAR(50) NOT NULL, 
    Position VARCHAR(50) NOT NULL, 
    DepartmentID INT, 
    FOREIGN KEY (DepartmentID) REFERENCES Department(DepartmentID) 
); 
 
CREATE TABLE Citizen ( 
    CitizenID INT AUTO_INCREMENT PRIMARY KEY, 
    FirstName VARCHAR(50) NOT NULL, 
    LastName VARCHAR(50) NOT NULL, 
    DateOfBirth DATE NOT NULL, 
    Gender ENUM('Male', 'Female', 'Other') NOT NULL 
); 
 
CREATE TABLE Service ( 
    ServiceID INT AUTO_INCREMENT PRIMARY KEY, 
    ServiceName VARCHAR(100) NOT NULL, 
    Description TEXT, 
    DepartmentID INT, 
    Cost DECIMAL(10, 2) NOT NULL, 
    FOREIGN KEY (DepartmentID) REFERENCES Department(DepartmentID) 
); 
 
CREATE TABLE ServiceRequest ( 
    RequestID INT AUTO_INCREMENT PRIMARY KEY, 
    CitizenID INT, 
    ServiceID INT, 
    RequestDate DATE NOT NULL, 


    Status VARCHAR(20) NOT NULL, 
    FOREIGN KEY (CitizenID) REFERENCES Citizen(CitizenID), 
    FOREIGN KEY (ServiceID) REFERENCES Service(ServiceID) 
); 

2.2 populate the database 

 
INSERT INTO Department (DepartmentName, Location, HeadOfDepartment, Budget) VALUES 
('Health', 'Building A', 1, 1000000.00), 
('Education', 'Building B', 2, 2000000.00), 
('Transport', 'Building C', 3, 1500000.00), 
('Finance', 'Building D', 4, 3000000.00), 
('Housing', 'Building E', 5, 2500000.00);  
INSERT INTO Employee (FirstName, LastName, Position, DepartmentID) VALUES 
('Alice', 'Taylor', 'Manager', 1), 
('Robert', 'Jones', 'Supervisor', 2), 
('Maria', 'Garcia', 'Officer', 3), 
('James', 'Martinez', 'Clerk', 4), 
('Linda', 'Rodriguez', 'Analyst', 5); 
 
INSERT INTO Citizen (FirstName, LastName, DateOfBirth, Gender) VALUES 
('John', 'Doe', '1990-01-01', 'Male'), 
('Jane', 'Smith', '1985-05-12', 'Female'), 
('Emily', 'Davis', '1978-11-20', 'Female'), 
('Michael', 'Brown', '1992-07-08', 'Male'), 
('Sarah', 'Wilson', '1989-03-15', 'Female'); 
 
INSERT INTO Service (ServiceName, Description, DepartmentID, Cost) VALUES 
('Medical Checkup', 'General health checkup', 1, 500.00), 
('School Enrollment', 'Enroll in public school', 2, 200.00), 
('Bus Pass', 'Monthly public transport pass', 3, 50.00), 
('Tax Filing', 'Annual tax return filing', 4, 100.00), 
('Housing Assistance', 'Help with housing applications', 5, 0.00);  
INSERT INTO ServiceRequest (CitizenID, ServiceID, RequestDate, Status) VALUES 
(1, 1, '2024-01-10', 'Pending'), 
(2, 2, '2024-01-11', 'Completed'), 
(3, 3, '2024-01-12', 'In Progress'), 
(4, 4, '2024-01-13', 'Pending'), 
(5, 5, '2024-01-14', 'Completed'); 
 

TEST THE INTEGRITY OF YOUR Databes
Show tables 

SHOW TABLES; 


// example 3 

CREATE DATABASE Smith_Sports_Club; 
 
USE Smith_Sports_Club; 
 
CREATE TABLE Smith_Disciplines ( 
    Smith_DisciplineID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_DisciplineName VARCHAR(100) NOT NULL, 
    Smith_Description TEXT, 
    Smith_NumberOfTeams INT NOT NULL, 
    Smith_Popularity VARCHAR(50) NOT NULL 
); 
 
CREATE TABLE Smith_Coaches ( 
    Smith_CoachID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_FirstName VARCHAR(50) NOT NULL, 
    Smith_LastName VARCHAR(50) NOT NULL, 
    Smith_ExperienceYears INT NOT NULL, 
    Smith_CertificationLevel VARCHAR(50) NOT NULL 
); 
 
CREATE TABLE Smith_Teams ( 
    Smith_TeamID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_TeamName VARCHAR(100) NOT NULL, 
    Smith_DisciplineID INT, 
    Smith_CoachID INT, 
    Smith_NumberOfPlayers INT NOT NULL, 
    FOREIGN KEY (Smith_DisciplineID) REFERENCES 
Smith_Disciplines(Smith_DisciplineID), 
    FOREIGN KEY (Smith_CoachID) REFERENCES Smith_Coaches(Smith_CoachID) 
); 
 
CREATE TABLE Smith_Players ( 
    Smith_PlayerID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_FirstName VARCHAR(50) NOT NULL, 
    Smith_LastName VARCHAR(50) NOT NULL, 
    Smith_TeamID INT, 
    Smith_Position VARCHAR(50) NOT NULL, 
    Smith_Age INT NOT NULL, 
    FOREIGN KEY (Smith_TeamID) REFERENCES Smith_Teams(Smith_TeamID) 
); 
 
CREATE TABLE Smith_Fields ( 
    Smith_FieldID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_FieldName VARCHAR(100) NOT NULL, 
    Smith_Location VARCHAR(100) NOT NULL, 
    Smith_Capacity INT NOT NULL, 
    Smith_SurfaceType VARCHAR(50) NOT NULL 
); 
 
CREATE TABLE Smith_TeamFields ( 
    Smith_TeamID INT, 
    Smith_FieldID INT, 
    PRIMARY KEY (Smith_TeamID, Smith_FieldID), 
    FOREIGN KEY (Smith_TeamID) REFERENCES Smith_Teams(Smith_TeamID), 
    FOREIGN KEY (Smith_FieldID) REFERENCES Smith_Fields(Smith_FieldID) ); 
 
 
2.2 Populate the Database 
 
INSERT INTO Smith_Disciplines (Smith_DisciplineName, Smith_Description, 
Smith_NumberOfTeams, Smith_Popularity) VALUES 
('Soccer', 'Team sport played with a spherical ball', 10, 'High'), 
('Basketball', 'Team sport played on a rectangular court', 8, 'High'), 
('Tennis', 'Racket sport played individually or in pairs', 6, 'Medium'), 
('Swimming', 'Individual or team sport that involves moving through water', 
5, 'Medium'), 
('Athletics', 'Collection of sports events including running, jumping, and throwing', 7, 'Medium'); 
 
INSERT INTO Smith_Coaches (Smith_FirstName, Smith_LastName, 
Smith_ExperienceYears, Smith_CertificationLevel) VALUES 
('John', 'Smith', 10, 'Level 3'), 
('Jane', 'Doe', 8, 'Level 2'), 
('Robert', 'Johnson', 15, 'Level 4'), 
('Emily', 'Brown', 12, 'Level 3'), 
('Michael', 'Davis', 5, 'Level 1'); 
 
INSERT INTO Smith_Teams (Smith_TeamName, Smith_DisciplineID, Smith_CoachID, 
Smith_NumberOfPlayers) VALUES 
('Tigers', 1, 1, 25), 
('Dragons', 2, 2, 20), 
('Eagles', 3, 3, 10), 
('Sharks', 4, 4, 15), 
('Panthers', 5, 5, 12); 
 
INSERT INTO Smith_Players (Smith_FirstName, Smith_LastName, Smith_TeamID, Smith_Position, Smith_Age) VALUES 
('Alice', 'Taylor', 1, 'Forward', 22), ('Bob', 'Miller', 1, 'Defender', 24), 
('Charlie', 'Wilson', 2, 'Guard', 21), 
('David', 'Moore', 2, 'Forward', 23), 
('Eva', 'Martin', 3, 'Player', 20); 
 
INSERT INTO Smith_Fields (Smith_FieldName, Smith_Location, Smith_Capacity, Smith_SurfaceType) VALUES 
('Main Stadium', 'Central Park', 5000, 'Grass'), 
('Court A', 'Sports Complex', 2000, 'Hardwood'), 
('Court B', 'Sports Complex', 2000, 'Hardwood'), 
('Swimming Pool', 'Aquatic Center', 1000, 'Water'), 
('Athletics Track', 'Sports Complex', 3000, 'Synthetic');  
INSERT INTO Smith_TeamFields (Smith_TeamID, Smith_FieldID) VALUES 
(1, 1), 
(2, 2), 
(2, 3), 
(3, 4), 
(4, 4), 
(5, 5); 
 
 
Step 3: Test the Integrity of Your Database 


show tables 
 3.1 SHOW TABLES;
 
 
3.2 Foreign Keys 
Foreign keys are also defined in the table creation SQL. 
 
DESC Smith_Disciplines; 
DESC Smith_Coaches; DESC Smith_Teams; 
DESC Smith_Players; 
DESC Smith_Fields; 
DESC Smith_TeamFields; 
 
3.3 Normalisation 
Ensure your tables are in at least 3NF. The provided structure should already follow the 3NF principles. 
 
SELECT * FROM Smith_Disciplines; 
SELECT * FROM Smith_Coaches; SELECT * FROM Smith_Teams; 
SELECT * FROM Smith_Players; 
SELECT * FROM Smith_Fields; 
SELECT * FROM Smith_TeamFields; 
 
4 Generate Reports 
4.1 Chairperson Report 
 
SELECT d.Smith_DisciplineName, COUNT(t.Smith_TeamID) AS TotalTeams 
FROM Smith_Disciplines d 
JOIN Smith_Teams t ON d.Smith_DisciplineID = t.Smith_DisciplineID 
GROUP BY d.Smith_DisciplineName; 

4.2 Team Manager Report 
 
SELECT t.Smith_TeamName, c.Smith_FirstName AS CoachFirstName, 
c.Smith_LastName AS CoachLastName, COUNT(p.Smith_PlayerID) AS TotalPlayers 
FROM Smith_Teams t 
JOIN Smith_Coaches c ON t.Smith_CoachID = c.Smith_CoachID 
JOIN Smith_Players p ON t.Smith_TeamID = p.Smith_TeamID 
GROUP BY t.Smith_TeamID; 

 Step 5: Integrity Tests 
5.1 Entity Integrity 
 
-- Attempt to insert a Player without a primary key (should auto-increment)
INSERT INTO Smith_Players (Smith_FirstName, Smith_LastName, Smith_TeamID, 
Smith_Position, Smith_Age) VALUES ('Test', 'User', 1, 'Test Position', 20); 
 
5.2Referential Integrity 
 
-- Attempt to insert a Player with an invalid TeamID (should fail) 
INSERT INTO Smith_Players (Smith_FirstName, Smith_LastName, Smith_TeamID, 
Smith_Position, Smith_Age) VALUES ('Test', 'User', 999, 'Test Position', 
20); 
 

// EXAMPLE 4 .
1. Database Creation DDL 
1.1 Create the Database 
Assuming your surname is "Smith", the database name will be Smith_Sports_Club. 
 
CREATE DATABASE Smith_Sports_Club; 
 
 
1.2 Show Databases 
 
SHOW DATABASES; 
 
 
  
2. Create the Tables 
2.1 Table for Disciplines Attribute Domain Table: 
Attribute 	Data Type 	Constraints 
Smith_DisciplineID 	INT 	PRIMARY KEY, AUTO_INCREMENT 
Smith_DisciplineName 	VARCHAR(100) 	NOT NULL 
Smith_Description 	TEXT 	NULL 
Smith_TeamCount 	INT 	NOT NULL 
Smith_Popularity 	VARCHAR(50) 	NOT NULL 
Create Table: 
 
USE Smith_Sports_Club; 
 
CREATE TABLE Smith_Disciplines ( 
    Smith_DisciplineID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_DisciplineName VARCHAR(100) NOT NULL, 
    Smith_Description TEXT, 
    Smith_TeamCount INT NOT NULL, 
    Smith_Popularity VARCHAR(50) NOT NULL 
); 
 
 
 
2.2 Table for Teams Attribute Domain Table: 
Attribute 	Data Type 	Constraints 
Smith_TeamID 	INT 	PRIMARY KEY, AUTO_INCREMENT 
Smith_TeamName 	VARCHAR(100) 	NOT NULL 
Smith_DisciplineID 	INT 	FOREIGN KEY 
Smith_CoachID 	INT 	FOREIGN KEY 
Smith_PlayerCount 	INT 	NOT NULL 
Create Table: 
 
CREATE TABLE Smith_Teams ( 
    Smith_TeamID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_TeamName VARCHAR(100) NOT NULL, 
    Smith_DisciplineID INT, 
    Smith_CoachID INT, 
    Smith_PlayerCount INT NOT NULL, 
    FOREIGN KEY (Smith_DisciplineID) REFERENCES 
Smith_Disciplines(Smith_DisciplineID), 
    FOREIGN KEY (Smith_CoachID) REFERENCES Smith_Coaches(Smith_CoachID) ); 
 
2.3 Table for Coaches Attribute Domain Table: 
Attribute 	Data Type 	Constraints 
Smith_CoachID 	INT 	PRIMARY KEY, AUTO_INCREMENT 
Smith_FirstName 	VARCHAR(50) 	NOT NULL 
Smith_LastName 	VARCHAR(50) 	NOT NULL 
Smith_Experience 	INT 	NOT NULL 
Smith_Certification 	VARCHAR(50) 	NOT NULL 
Create Table: 
 
CREATE TABLE Smith_Coaches ( 
    Smith_CoachID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_FirstName VARCHAR(50) NOT NULL, 
    Smith_LastName VARCHAR(50) NOT NULL, 
    Smith_Experience INT NOT NULL, 
    Smith_Certification VARCHAR(50) NOT NULL 
); 
 
2.4 Table for Players Attribute Domain Table: 
Attribute 	Data Type 	Constraints 
Smith_PlayerID 	INT 	PRIMARY KEY, AUTO_INCREMENT 
Smith_FirstName 	VARCHAR(50) 	NOT NULL 
Smith_LastName 	VARCHAR(50) 	NOT NULL 
Smith_TeamID 	INT 	FOREIGN KEY 
Smith_Position 	VARCHAR(50) 	NOT NULL 
Smith_Age 	INT 	NOT NULL 
Create Table: 
 
CREATE TABLE Smith_Players ( 
    Smith_PlayerID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_FirstName VARCHAR(50) NOT NULL, 
    Smith_LastName VARCHAR(50) NOT NULL,     Smith_TeamID INT, 
    Smith_Position VARCHAR(50) NOT NULL, 
    Smith_Age INT NOT NULL, 
    FOREIGN KEY (Smith_TeamID) REFERENCES Smith_Teams(Smith_TeamID) 
); 
 
 
2.5 Table for Fields Attribute Domain Table: 
Attribute 	Data Type 	Constraints 
Smith_FieldID 	INT 	PRIMARY KEY, AUTO_INCREMENT 
Smith_FieldName 	VARCHAR(100) 	NOT NULL 
Smith_Location 	VARCHAR(100) 	NOT NULL 
Smith_Capacity 	INT 	NOT NULL 
Smith_SurfaceType 	VARCHAR(50) 	NOT NULL 
Create Table: 
 
CREATE TABLE Smith_Fields ( 
    Smith_FieldID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_FieldName VARCHAR(100) NOT NULL, 
    Smith_Location VARCHAR(100) NOT NULL, 
    Smith_Capacity INT NOT NULL, 
    Smith_SurfaceType VARCHAR(50) NOT NULL 
); 
 
3. Insert Data into the Tables 
3.1 Insert Data into Disciplines 
 
INSERT INTO Smith_Disciplines (Smith_DisciplineName, Smith_Description, 
Smith_TeamCount, Smith_Popularity) VALUES 
('Soccer', 'Team sport played with a spherical ball', 10, 'High'), 
('Basketball', 'Team sport played on a rectangular court', 8, 'High'), 
('Tennis', 'Racket sport played individually or in pairs', 6, 'Medium'), 
('Swimming', 'Individual or team sport that involves moving through water', 
5, 'Medium'), 
('Athletics', 'Collection of sports events including running, jumping, and throwing', 7, 'Medium'); 
 
 
3.2 Insert Data into Coaches 
 
INSERT INTO Smith_Coaches (Smith_FirstName, Smith_LastName, 
Smith_Experience, Smith_Certification) VALUES 
('John', 'Smith', 10, 'Level 3'), 
('Jane', 'Doe', 8, 'Level 2'), 
('Robert', 'Johnson', 15, 'Level 4'), 
('Emily', 'Brown', 12, 'Level 3'), 
('Michael', 'Davis', 5, 'Level 1'); 
 
 
3.3 Insert Data into Teams 
 
INSERT INTO Smith_Teams (Smith_TeamName, Smith_DisciplineID, Smith_CoachID, 
Smith_PlayerCount) VALUES 
('Tigers', 1, 1, 25), 
('Dragons', 2, 2, 20), 
('Eagles', 3, 3, 10), 
('Sharks', 4, 4, 15), 
('Panthers', 5, 5, 12); 
 
 
 
 
3.4 Insert Data into Players 
 
INSERT INTO Smith_Players (Smith_FirstName, Smith_LastName, Smith_TeamID, 
Smith_Position, Smith_Age) VALUES 
('Alice', 'Taylor', 1, 'Forward', 22), 
('Bob', 'Miller', 1, 'Defender', 24), 
('Charlie', 'Wilson', 2, 'Guard', 21), 
('David', 'Moore', 2, 'Forward', 23), 
('Eva', 'Martin', 3, 'Player', 20); 
 
 
3.5 Insert Data into Fields 
 
INSERT INTO Smith_Fields (Smith_FieldName, Smith_Location, Smith_Capacity, 
Smith_SurfaceType) VALUES 
('Main Stadium', 'Central Park', 5000, 'Grass'), 
('Court A', 'Sports Complex', 2000, 'Hardwood'), 
('Court B', 'Sports Complex', 2000, 'Hardwood'), 
('Swimming Pool', 'Aquatic Center', 1000, 'Water'), 
('Athletics Track', 'Sports Complex', 3000, 'Synthetic');  
 
4. Test the Integrity of Your Database 
4.1 Show Tables 
 
SHOW TABLES; 
 
  
 
4.2 Describe Each Table 
 
DESC Smith_Disciplines; 
DESC Smith_Coaches; DESC Smith_Teams; 
DESC Smith_Players; 
DESC Smith_Fields; 
 
  
 
 
 
4.3 Select All from Each Table 
 
SELECT * FROM Smith_Disciplines; 
SELECT * FROM Smith_Coaches; SELECT * FROM Smith_Teams; 
SELECT * FROM Smith_Players; 
SELECT * FROM Smith_Fields;  
  
 
 
 
 
5. Create Views and Queries 
5.1 Create a View 
 
CREATE VIEW Smith_TeamPlayers AS 
SELECT t.Smith_TeamName, p.Smith_FirstName, p.Smith_LastName, p.Smith_Position 
FROM Smith_Teams t 
JOIN Smith_Players p ON t.Smith_TeamID = p.Smith_TeamID;  
 
 
View Output: 
 
SELECT * FROM Smith_TeamPlayers; 
 
  
5.2 Entity Integrity 
Test Entity Integrity: 
 
-- Attempt to insert a Player without a primary key (should auto-increment) INSERT INTO Smith_Players (Smith_FirstName, Smith_LastName, Smith_TeamID, 
Smith_Position, Smith_Age) VALUES ('Test', 'User', 1, 'Test Position', 20); 
 
 
Output: 
 
SELECT * FROM Smith_Players WHERE Smith_FirstName = 'Test';  
 
 
5.3 Referential Integrity 
Test Referential Integrity: 
 
-- Attempt to insert a Player with 
 
EXAMPLE 5: 
Step-by-Step Solution 
Step 1: Design the Database 
Entities and Attributes: 
1.	Client o 	ClientID (Primary Key) 
o	FirstName o 	LastName o 	DateOfBirth o 	Email 
2.	Video o VideoID (Primary Key) o Title o Genre o ReleaseDate o Stock 
3.	Lease o 	LeaseID (Primary Key) o 	ClientID (Foreign Key) o 	VideoID (Foreign Key) 
o	LeaseDate o 	ReturnDate 
4.	Manager o ManagerID (Primary Key) o FirstName o LastName o Email o Phone 
5.	Clerk o 	ClerkID (Primary Key) 
o	FirstName o 	LastName o 	Email o 	Phone 
Relationships: 
•	A client can lease multiple videos. 
•	Each lease record links a client and a video. 
•	Each video can be leased by multiple clients. 
 
Step 2: Implement the Database 
2.1 DDL for Implementing the Database 
Assuming the surname is "Smith", we will prefix all table names and attributes accordingly. 
 
CREATE DATABASE Smith_Video_Shop; 
 
USE Smith_Video_Shop; 
 
CREATE TABLE Smith_Clients ( 
    Smith_ClientID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_FirstName VARCHAR(50) NOT NULL, 
    Smith_LastName VARCHAR(50) NOT NULL, 
    Smith_DateOfBirth DATE NOT NULL, 
    Smith_Email VARCHAR(100) NOT NULL 
); 
 
CREATE TABLE Smith_Videos ( 
    Smith_VideoID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_Title VARCHAR(100) NOT NULL, 
    Smith_Genre VARCHAR(50) NOT NULL, 
    Smith_ReleaseDate DATE NOT NULL, 
    Smith_Stock INT NOT NULL 
); 
 
CREATE TABLE Smith_Leases ( 
    Smith_LeaseID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_ClientID INT, 
    Smith_VideoID INT, 
    Smith_LeaseDate DATE NOT NULL, 
    Smith_ReturnDate DATE, 
    FOREIGN KEY (Smith_ClientID) REFERENCES Smith_Clients(Smith_ClientID), 
    FOREIGN KEY (Smith_VideoID) REFERENCES Smith_Videos(Smith_VideoID) 
); 
 
CREATE TABLE Smith_Managers ( 
    Smith_ManagerID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_FirstName VARCHAR(50) NOT NULL, 
    Smith_LastName VARCHAR(50) NOT NULL, 
    Smith_Email VARCHAR(100) NOT NULL, 
    Smith_Phone VARCHAR(20) NOT NULL 
); 
 
CREATE TABLE Smith_Clerks ( 
    Smith_ClerkID INT AUTO_INCREMENT PRIMARY KEY, 
    Smith_FirstName VARCHAR(50) NOT NULL, 
    Smith_LastName VARCHAR(50) NOT NULL, 
    Smith_Email VARCHAR(100) NOT NULL, 
    Smith_Phone VARCHAR(20) NOT NULL 
); 
 
 
2.2 Populate the Database 
 
INSERT INTO Smith_Clients (Smith_FirstName, Smith_LastName, 
Smith_DateOfBirth, Smith_Email) VALUES 
('John', 'Doe', '1990-01-01', 'john.doe@example.com'), 
('Jane', 'Smith', '1985-05-12', 'jane.smith@example.com'), 
('Emily', 'Davis', '1978-11-20', 'emily.davis@example.com'), 
('Michael', 'Brown', '1992-07-08', 'michael.brown@example.com'), 
('Sarah', 'Wilson', '1989-03-15', 'sarah.wilson@example.com');  
INSERT INTO Smith_Videos (Smith_Title, Smith_Genre, Smith_ReleaseDate, 
Smith_Stock) VALUES 
('The Legend of Zelda', 'Adventure', '2017-03-03', 10), 
('Super Mario Odyssey', 'Platformer', '2017-10-27', 8), 
('Minecraft', 'Sandbox', '2011-11-18', 15), 
('Fortnite', 'Battle Royale', '2017-07-25', 12), 
('Call of Duty', 'Shooter', '2003-10-29', 7); 
 
INSERT INTO Smith_Leases (Smith_ClientID, Smith_VideoID, Smith_LeaseDate, 
Smith_ReturnDate) VALUES 
(1, 1, '2023-10-01', '2023-10-08'), 
(2, 2, '2023-10-02', '2023-10-09'), 
(3, 3, '2023-10-03', '2023-10-10'), 
(4, 4, '2023-10-04', '2023-10-11'), 
(5, 5, '2023-10-05', '2023-10-12'); 
 
INSERT INTO Smith_Managers (Smith_FirstName, Smith_LastName, Smith_Email, 
Smith_Phone) VALUES 
('Alice', 'Taylor', 'alice.taylor@example.com', '555-1234'), 
('Robert', 'Johnson', 'robert.johnson@example.com', '555-5678');  
INSERT INTO Smith_Clerks (Smith_FirstName, Smith_LastName, Smith_Email, Smith_Phone) VALUES 
('James', 'Martinez', 'james.martinez@example.com', '555-8765'), 
('Linda', 'Rodriguez', 'linda.rodriguez@example.com', '555-4321'); 
 
Step 3: Test the Integrity of Your Database 
3.1 Show Tables 
 
SHOW TABLES; 
 
 
 
3.2 Describe Each Table 
 
DESC Smith_Clients; 
DESC Smith_Videos; 
DESC Smith_Leases; 
DESC Smith_Managers; 
DESC Smith_Clerks; 
 
  
  
3.3 Select All from Each Table 
 
SELECT * FROM Smith_Clients; 
SELECT * FROM Smith_Videos; 
SELECT * FROM Smith_Leases; 
SELECT * FROM Smith_Managers; 
SELECT * FROM Smith_Clerks; 
 
 
  
  
4. Generate Reports 
4.1 Manager Report 
 
SELECT COUNT(*) AS TotalClients FROM Smith_Clients; 
 
  
4.2 Clerk Report 
 
SELECT c.Smith_FirstName, c.Smith_LastName, l.Smith_LeaseDate, l.Smith_DueDate, l.Smith_ReturnDate 
FROM Smith_Leases l 
JOIN Smith_Clients c ON l.Smith_ClientID = c.Smith_ClientID 
WHERE l.Smith_ReturnDate IS NULL AND l.Smith_DueDate < CURDATE();  
  
Step 5: Integrity Tests 
5.1 Entity Integrity 
 
-- Attempt to insert a Client without a primary key (should auto-increment) 
INSERT INTO Smith_Clients (Smith_FirstName, Smith_LastName, 
Smith_DateOfBirth, Smith_Email) VALUES ('Test', 'User', '2000-01-01', 
'test.user@example.com'); 
 
  
5.2 Referential Integrity 
 
-- Attempt to insert a Lease with an invalid ClientID (should fail) 
INSERT INTO Smith_Leases (Smith_ClientID, Smith_VideoID, Smith_LeaseDate, 
Smith_DueDate, Smith_ReturnDate) VALUES (999, 1, '2023-10-01', '2023-10-08', 
NULL); 




Practice test 2 

Databases _Memo  

Cape Town Municipality SQL Task 

You are hired to create a database system for the Cape Town Municipality. This system will 
manage important data such as residents, municipal services (e.g., water, electricity, waste 
collection), and monthly billing information. 

Task: 

Create a database for the Cape Town Municipality based on the information provided. You must 
decide how many tables are needed, what relationships exist between them, and the 
appropriate fields, keys, and constraints. 

SQL Queries: 

After creating and populating your database with sample data (at least 5 records per table), 
answer the following questions: 

Creating and populating tables : 

Create Residents table 

CREATE TABLE Residents ( 
ResidentID INT PRIMARY KEY, 
Name VARCHAR(50), 
Surname VARCHAR(50), 
Address VARCHAR(100), 
ContactNumber VARCHAR(20) 
); 
Create Services table 
CREATE TABLE Services ( 
ServiceID INT PRIMARY KEY, 
ServiceName VARCHAR(50), 
CostPerMonth DECIMAL(10,2) 
); 
Create Billing table 
CREATE TABLE Billing ( 
BillID INT PRIMARY KEY, 
ResidentID INT, 
ServiceID INT, 
BillingDate DATE, 
AmountDue DECIMAL(10,2), 
FOREIGN KEY (ResidentID) REFERENCES Residents(ResidentID), 
FOREIGN KEY (ServiceID) REFERENCES Services(ServiceID) 
); 
POPULATING THE TABLES 
Insert into Residents 
INSERT INTO Residents VALUES (1, 'John', 'Smith', 'Khayelitsha', '0123456789'); 
INSERT INTO Residents VALUES (2, 'Mary', 'Adams', 'Bellville', '0987654321'); 
INSERT INTO Residents VALUES (3, 'Lungile', 'Dlamini', 'Mitchells Plain', '0765432198'); 
INSERT INTO Residents VALUES (4, 'Sara', 'Naidoo', 'Durbanville', '0841234567'); 
INSERT INTO Residents VALUES (5, 'Peter', 'Williams', 'Khayelitsha', '0749876543'); -- Insert into Services 
INSERT INTO Services VALUES (1, 'Water', 200.00); 
INSERT INTO Services VALUES (2, 'Electricity', 350.00); 
INSERT INTO Services VALUES (3, 'Waste Collection', 150.00); 
INSERT INTO Services VALUES (4, 'Sewerage', 180.00); 
INSERT INTO Services VALUES (5, 'Street Lighting', 100.00); -- Insert into Billing 
INSERT INTO Billing VALUES (1, 1, 1, '2025-03-01', 200.00); 
INSERT INTO Billing VALUES (2, 1, 2, '2025-03-01', 350.00); 
INSERT INTO Billing VALUES (3, 2, 3, '2025-03-01', 150.00); 
INSERT INTO Billing VALUES (4, 3, 1, '2025-03-01', 200.00); 
INSERT INTO Billing VALUES (5, 3, 2, '2025-03-01', 350.00); 
INSERT INTO Billing VALUES (6, 4, 4, '2025-03-01', 180.00); 
INSERT INTO Billing VALUES (7, 5, 2, '2025-03-01', 350.00); 
a) Use a UNION query to combine and display all unique resident names and service 
names in a single column. 
Answer: 
SELECT Name AS Data FROM Residents 
UNION 
SELECT ServiceName AS Data FROM Services; 
b) Write a query that simulates an INTERSECTION to find all residents who are subscribed 
to both water and electricity services. 
Answer: 
SELECT r.Name 
FROM Residents r 
JOIN Billing b1 ON r.ResidentID = b1.ResidentID 
JOIN Services s1 ON b1.ServiceID = s1.ServiceID AND s1.ServiceName = 'Water' 
JOIN Billing b2 ON r.ResidentID = b2.ResidentID 
JOIN Services s2 ON b2.ServiceID = s2.ServiceID AND s2.ServiceName = 'Electricity'; 
c) UPDATE the relevant table(s) to increase the monthly billing amount by 10% for all 
residents in a specific suburb of your choice. 
Answer: 
UPDATE Billing 
SET AmountDue = AmountDue * 1.10 
WHERE ResidentID IN ( 
SELECT ResidentID FROM Residents WHERE Address LIKE '%Khayelitsha%' 
); 
d) DELETE any resident who is not subscribed to any service (i.e., not found in your billing 
or service subscription table). 
Answer: 
DELETE FROM Residents 
WHERE ResidentID NOT IN (SELECT DISTINCT ResidentID FROM Billing); 
e) ALTER one of your tables to add a new column for Email address for residents. 
Answer: 
ALTER TABLE Residents 
ADD Email VARCHAR(100); 
f) 
Write an aggregate query to display the total revenue generated from each service 
across all residents. 
Answer: 
SELECT s.ServiceName, SUM(b.AmountDue) AS TotalRevenue 
FROM Billing b 
JOIN Services s ON b.ServiceID = s.ServiceID 
GROUP BY s.ServiceName; 
Bonus: Create a view that shows each resident's name, suburb, and their total monthly amount 
due. 
Answer: 
CREATE VIEW ResidentBills AS 
SELECT r.Name, r.Address AS Suburb, SUM(b.AmountDue) AS TotalAmountDue 
FROM Residents r 
JOIN Billing b ON r.ResidentID = b.ResidentID
GROUP BY r.Name,r.Address;






