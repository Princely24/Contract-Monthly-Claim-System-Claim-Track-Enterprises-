# Contract-Monthly-Claim-System-Claim-Track-Enterprises-
Documentation  

1. Design Decisions 

1.1 Essential Functions 

Claim Submission: The ability to submit monthly claims that include information about the number of hours worked and hourly rates is required of IC lecturers. 

Approval Process: The Academic Manager and the Program Coordinator should jointly examine and approve claims. 

Document Upload: IC instructors have the option to upload documents that bolster their assertions. 

Reporting: Claims reports, including summaries and in-depth views, ought to be produced by administrators. 

1.2 The Technical Framework 

Frontend: Razor Pages is used to render dynamic content while developing a web-based graphical user interface with ASP.NET Core WPF. 

Backend: Application logic and business rules are implemented in C# using.NET Core. 

Database: Microsoft SQL Server is used to store user data, supporting documentation, and claim specifics. 

Authentication: Role administration and safe user authentication are provided by ASP.NET Identity. 
2. Structure of Databases 

The CMCS database is made to guarantee effective data administration, retrieval, and storage. It has the following crucial tables: 

2.1. Tables 

1. Lecturers 

Stores information about the lecturers who will be submitting claims. 

LecturerID (Primary Key, INT, Auto Increment) 

FirstName (VARCHAR) 

LastName (VARCHAR) 

Email (VARCHAR) 

Phone (VARCHAR) 

Department (VARCHAR) 

2. Claim 

Tracks the claims submitted by lecturers. 

ClaimID (Primary Key, INT, Auto Increment) 

LecturerID (Foreign Key, INT, references Lecturers.LecturerID) 

ClaimDate (DATETIME) 

Amount (DECIMAL) 

Description (TEXT) 

Status (ENUM: 'Pending', 'Approved', 'Rejected', 'Settled') 

SubmissionDate (DATETIME) 

3. SupportingDocuments 

Stores information about the documents uploaded for each claim. 

DocumentID (Primary Key, INT, Auto Increment) 

ClaimID (Foreign Key, INT, references Claims.ClaimID) 

DocumentPath (VARCHAR) 

UploadDate (DATETIME) 

DocumentType (VARCHAR) 

4. ProgrammeCoordinators 

Information about programme coordinators who verify claims. 

CoordinatorID (Primary Key, INT, Auto Increment) 

FirstName (VARCHAR) 

LastName (VARCHAR) 

Email (VARCHAR) 

Phone (VARCHAR) 

Department (VARCHAR) 

5. AcademicManagers 

Information about academic managers who approve or reject claims. 

ManagerID (Primary Key, INT, Auto Increment) 

FirstName (VARCHAR) 

LastName (VARCHAR) 

Email (VARCHAR) 

Phone (VARCHAR) 

Department (VARCHAR) 

6. ClaimApprovals 

Tracks the approval process for claims. 

ApprovalID (Primary Key, INT, Auto Increment) 

ClaimID (Foreign Key, INT, references Claims.ClaimID) 

ApproverID (Foreign Key, INT, references AcademicManagers.ManagerID) 

ApprovalDate (DATETIME) 

ApprovalStatus (ENUM: 'Pending', 'Approved', 'Rejected') 

Comments (TEXT) 
