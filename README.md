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
Relationships 

Lecturers ↔ Claims 

One-to-Many: One Lecturer can have multiple Claims. 

Claims ↔ SupportingDocuments 

One-to-Many: One Claim can have multiple SupportingDocuments. 

Claims ↔ ClaimApprovals 

One-to-One or One-to-Many: One Claim can have one Approval record by one Academic Manager 

AcademicManagers ↔ ClaimApprovals 

One-to-Many: One Academic Manager can approve multiple Claims. 

3. GUI Design 

The main pages and elements of the GUI's design are as follows: 

3.1 The Dashboard for Users 

Secure user authentication on the login page. 

Home Page: Provides options (such as submit claim, view claims, etc.) according to the role of the user. 

Form for Claim Submission: 

⦁	inputs for month/year, hourly rate, and hours worked. 

⦁	The ability to upload supporting papers. 

⦁	Click the "Submit" button to validate. 

3.2 Handling of Claims 

List of Claims: 

⦁	table showing filed claims along with status indications. 

⦁	filters to display claims according to the user, date range, or status. 

Page of Claim Details: 

⦁	a thorough look at a particular claim, complete with hours performed, total cost, and any supporting documentation. 

⦁	The Academic Manager and Program Coordinator positions have approve/reject buttons. 

3.3 Reporting:  

⦁	Select a report generation option based on a user, claim status, or date range. 

⦁	The ability to export reports in Excel or PDF format. 

3.4 User Administration (Administrators Only) 

List of Users: 

⦁	View and control the roles and details of users. 

⦁	choices for adding or deleting people. 

3.5 Important Elements 

⦁	Submit Claims: After providing the required information and attaching supporting documentation, lecturers can quickly and simply submit their claims with a single click. 

⦁	Verify and Approve Claims: Using a simplified interface, program coordinators and academic managers can expeditiously verify and approve claims. 

⦁	Lecturers can include supporting documentation with their assertions by uploading them, which makes sure that all the information needed is accessible for examination. 

⦁	Track Claim Status: The system lets lecturers monitor the status of their submissions until they are settled, offering clear tracking of claim statuses. 

⦁	Consistent and Reliable Information: By guaranteeing that all data shown is correct and current, the system improves consistency and dependability. 
