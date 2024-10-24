### Contract Monthly Claim System (CMCS) - Claim Track Enterprises  
#### Documentation

---

### 1. Design Decisions

#### 1.1 Essential Functions

1. **Claim Submission**:  
   IC lecturers are required to submit monthly claims detailing hours worked and hourly rates. 
   
2. **Approval Process**:  
   Claims must be reviewed and approved by both the **Academic Manager** and the **Program Coordinator**. 

3. **Document Upload**:  
   IC lecturers have the option to upload supporting documents to validate their claims. 

4. **Reporting**:  
   Administrators can generate summary and detailed reports about claims. 

#### 1.2 Technical Framework

- **Frontend**:  
  The graphical user interface (GUI) is web-based, built using ASP.NET Core with Razor Pages and WPF for rendering dynamic content.

- **Backend**:  
  The application logic and business rules are implemented using C# and .NET Core.

- **Database**:  
  **Microsoft SQL Server** stores user data, supporting documents, and claim specifics.

- **Authentication**:  
  **ASP.NET Identity** manages secure user authentication and role administration.

---

### 2. Database Structure

The CMCS database is designed for efficient storage, retrieval, and management of claim-related data. The following tables are fundamental to the system:

#### 2.1 Tables

1. **Lecturers**  
   Stores information about lecturers submitting claims.

   | Column        | Data Type    | Description                    |
   |---------------|--------------|--------------------------------|
   | LecturerID    | INT (PK)     | Auto-incrementing primary key  |
   | FirstName     | VARCHAR      | Lecturer's first name          |
   | LastName      | VARCHAR      | Lecturer's last name           |
   | Email         | VARCHAR      | Lecturer's email address       |
   | Phone         | VARCHAR      | Lecturer's phone number        |
   | Department    | VARCHAR      | Lecturer's department          |

2. **Claims**  
   Tracks the claims submitted by lecturers.

   | Column        | Data Type    | Description                                             |
   |---------------|--------------|---------------------------------------------------------|
   | ClaimID       | INT (PK)     | Auto-incrementing primary key                           |
   | LecturerID    | INT (FK)     | Foreign key from the `Lecturers` table                  |
   | ClaimDate     | DATETIME     | Date of the claim submission                            |
   | Amount        | DECIMAL      | Total claim amount                                      |
   | Description   | TEXT         | Description or notes on the claim                       |
   | Status        | ENUM         | 'Pending', 'Approved', 'Rejected', 'Settled'            |
   | SubmissionDate| DATETIME     | Date the claim was submitted (using `GETDATE()`)        |

3. **SupportingDocuments**  
   Stores uploaded documents for claims.

   | Column        | Data Type    | Description                                             |
   |---------------|--------------|---------------------------------------------------------|
   | DocumentID    | INT (PK)     | Auto-incrementing primary key                           |
   | ClaimID       | INT (FK)     | Foreign key from the `Claims` table                     |
   | DocumentPath  | VARCHAR      | File path of the uploaded document                      |
   | UploadDate    | DATETIME     | Date the document was uploaded                          |
   | DocumentType  | VARCHAR      | Type of the document (e.g., .pdf, .docx, .xlsx)         |

4. **ProgrammeCoordinators**  
   Contains information about coordinators who verify claims.

   | Column        | Data Type    | Description                                             |
   |---------------|--------------|---------------------------------------------------------|
   | CoordinatorID | INT (PK)     | Auto-incrementing primary key                           |
   | FirstName     | VARCHAR      | Coordinator's first name                                |
   | LastName      | VARCHAR      | Coordinator's last name                                 |
   | Email         | VARCHAR      | Coordinator's email                                     |
   | Phone         | VARCHAR      | Coordinator's phone number                              |
   | Department    | VARCHAR      | Coordinator's department                                |

5. **AcademicManagers**  
   Stores information about managers who approve claims.

   | Column        | Data Type    | Description                                             |
   |---------------|--------------|---------------------------------------------------------|
   | ManagerID     | INT (PK)     | Auto-incrementing primary key                           |
   | FirstName     | VARCHAR      | Manager's first name                                    |
   | LastName      | VARCHAR      | Manager's last name                                     |
   | Email         | VARCHAR      | Manager's email address                                 |
   | Phone         | VARCHAR      | Manager's phone number                                  |
   | Department    | VARCHAR      | Manager's department                                    |

6. **ClaimApprovals**  
   Tracks the approval process of claims by academic managers.

   | Column        | Data Type    | Description                                             |
   |---------------|--------------|---------------------------------------------------------|
   | ApprovalID    | INT (PK)     | Auto-incrementing primary key                           |
   | ClaimID       | INT (FK)     | Foreign key from the `Claims` table                     |
   | ApproverID    | INT (FK)     | Foreign key from the `AcademicManagers` table           |
   | ApprovalDate  | DATETIME     | Date the claim was approved/rejected                    |
   | ApprovalStatus| ENUM         | 'Pending', 'Approved', 'Rejected'                       |
   | Comments      | TEXT         | Additional comments from the approver                   |

#### 2.2 Relationships

- **Lecturers ↔ Claims**:  
  One lecturer can submit multiple claims (One-to-Many).

- **Claims ↔ SupportingDocuments**:  
  One claim can have multiple supporting documents (One-to-Many).

- **Claims ↔ ClaimApprovals**:  
  One claim can have one approval record by one academic manager (One-to-One or One-to-Many).

- **AcademicManagers ↔ ClaimApprovals**:  
  One academic manager can approve multiple claims (One-to-Many).

---

### 3. GUI Design

#### 3.1 User Dashboard

- **Login Page**: Secure user authentication.
- **Home Page**: Options based on the user’s role (submit claim, view claims, etc.).
- **Claim Submission Form**:  
  - Fields for entering month/year, hourly rate, and hours worked.
  - Ability to upload supporting documents.
  - Prominent "Submit" button for claim validation.

#### 3.2 Claim Management

- **List of Claims**:  
  - Displays claims with status indicators.
  - Filters for user, date range, or claim status.
  
- **Claim Details Page**:  
  - Displays specific claim details (hours, total cost, supporting documents).
  - Approve/Reject buttons for Academic Manager and Program Coordinator.

#### 3.3 Reporting

- Ability to generate reports based on user, claim status, or date range.
- Export options for Excel and PDF.

#### 3.4 User Management (Admin Only)

- **User List**:  
  - View and manage users' roles and details.
  - Add or delete users.

---

### 4. Assumptions and Constraints

#### 4.1 Assumptions

1. Lecturers are responsible for submitting their own claims.
2. Both the Program Coordinator and Academic Manager review claims.
3. Basic validation will be performed (e.g., ensuring the number of hours is reasonable).

#### 4.2 Constraints

1. The system must be user-friendly, minimizing the need for training.
2. Sensitive data (lecturer info, claim amounts) must be secured.
3. The system should scale to accommodate increasing users and claims.

---

### Conclusion

The **Contract Monthly Claim System (CMCS)** aims to streamline the submission and approval process for IC lecturers’ claims. Built on .NET, with a well-structured database and user-friendly GUI, it provides efficient management of claim data, approval workflows, and reporting while ensuring security and scalability.
