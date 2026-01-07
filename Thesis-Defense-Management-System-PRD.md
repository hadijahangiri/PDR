# Product Requirement Document (PRD)

**Feature Name:** Thesis Defense Management System  
**Product Context:** University Academic Administration System  
**Version:** 1.0  
**Date:** January 7, 2026  
**Author:** Product Team

---

## 1. Overview

### Summary
A comprehensive management panel system for university thesis defense administration that manages professors, students, and thesis defense records. The system handles the complete lifecycle of thesis defenses including tracking cooperation types, academic ranks, payment calculations, and financial transfers to professors. It provides role-based access control for administrators, professors, and students while maintaining detailed records of all thesis defense activities with filtering and reporting capabilities.

### Problem Statement
Universities currently lack an integrated system to manage thesis defenses, track professor participation, calculate compensation based on various factors (academic rank, cooperation type, thesis type, position, participation level), and handle financial transactions. Manual processes lead to errors in payment calculations, difficulty in tracking thesis defense records, and challenges in managing professor and student information across multiple universities.

### Goal
Streamline the thesis defense management process by providing a centralized system that:
- Automates compensation calculations based on defined rules
- Maintains accurate records of all thesis defenses
- Provides role-based access for different user types
- Enables efficient filtering and reporting
- Manages financial transfers to professors
- Ensures data integrity and security

---

## 2. Scope & Out of Scope

### In Scope
- User management with three distinct roles: Manager (Admin), Professor, Student
- Professor registration and profile management (name, national ID, professor code, bank account, status)
- Student registration and profile management (name, national ID, status)
- University definition and management
- Academic rank definition with supervision percentage (پایش)
- Thesis defense record creation with all required fields:
  - Professor and student selection from active lists
  - University selection
  - Persian calendar date picker for defense date
  - Cooperation type (Type A, Type B, Invited)
  - Academic rank selection
  - Grade (پایه)
  - Thesis type (Master's, Doctorate)
  - Unit count (4 or 6 units)
  - Position (Supervisor, Advisor, Examiner, Observer)
  - Participation level (0.5 or 1)
  - Postal service status (Has/Does not have)
- Comprehensive table listing with filtering capabilities for all fields
- Automatic compensation calculation based on all parameters
- Financial management section for transfers to professor accounts
- Account status tracking

### Out of Scope
- Student thesis content management or document upload
- Online thesis defense video conferencing
- Academic calendar integration
- Email notification system (may be added in future version)
- Mobile application (web-based only in this version)
- Integration with external university systems
- Automated grading or evaluation systems
- Multi-language support (Persian only in this version)

---

## 3. User Personas & Use Cases

### Personas

#### Persona 1: System Administrator (مدیریت)
University administrative staff responsible for managing the entire system, creating and managing professors, students, universities, academic ranks, and thesis defense records. Also handles financial operations and payment processing.

#### Persona 2: Professor (استاد)
University faculty member who participates in thesis defenses in various capacities (supervisor, advisor, examiner, observer). Can view their own defense records and payment status.

#### Persona 3: Student (دانشجو)
Graduate student (Master's or Doctorate) who can view information related to their thesis defense.

### Use Cases

#### UC-001: System Administrator Creates Professor Account
- **Description:** Admin creates a new professor account in the system
- **Pre-conditions:** User is logged in as Administrator
- **Post-conditions:** Professor account is created and set to active status
- **Main Flow:**
  1. Admin navigates to Professor Management section
  2. Admin clicks "Add New Professor"
  3. Admin enters professor details:
     - First and last name (نام و نام خانوادگی)
     - National ID (کد ملی)
     - Professor code (کد استاد)
     - Bank account number (شماره حساب)
  4. System automatically sets password to professor's national ID
  5. System sets role to "Professor" and status to "Active"
  6. Admin saves the record
  7. System validates all required fields
  8. System creates professor account
  9. System displays success message
- **Alternate/Error Flows:**
  - If national ID already exists, display error message
  - If bank account format is invalid, display validation error
  - If required fields are missing, highlight them and prevent submission

#### UC-002: System Administrator Creates Student Account
- **Description:** Admin creates a new student account in the system
- **Pre-conditions:** User is logged in as Administrator
- **Post-conditions:** Student account is created and set to active status
- **Main Flow:**
  1. Admin navigates to Student Management section
  2. Admin clicks "Add New Student"
  3. Admin enters student details:
     - First and last name (نام و نام خانوادگی)
     - National ID (کد ملی)
  4. System automatically sets password to student's national ID
  5. System sets role to "Student" and status to "Active"
  6. Admin saves the record
  7. System validates all required fields
  8. System creates student account
  9. System displays success message
- **Alternate/Error Flows:**
  - If national ID already exists, display error message
  - If required fields are missing, highlight them and prevent submission

#### UC-003: System Administrator Defines University
- **Description:** Admin adds a new university to the system
- **Pre-conditions:** User is logged in as Administrator
- **Post-conditions:** University is added to the system
- **Main Flow:**
  1. Admin navigates to University Management section
  2. Admin clicks "Add New University"
  3. Admin enters university name (نام دانشگاه)
  4. Admin saves the record
  5. System creates university entry
  6. System displays success message
- **Alternate/Error Flows:**
  - If university name already exists, display warning (may allow duplicates if different campuses)

#### UC-004: System Administrator Defines Academic Rank
- **Description:** Admin creates a new academic rank with supervision percentage
- **Pre-conditions:** User is logged in as Administrator
- **Post-conditions:** Academic rank is added to the system
- **Main Flow:**
  1. Admin navigates to Academic Rank Management section
  2. Admin clicks "Add New Academic Rank"
  3. Admin enters rank name (e.g., استادیار, دانشیار, استاد)
  4. Admin enters supervision percentage (درصد پایش)
  5. Admin saves the record
  6. System creates academic rank entry
  7. System displays success message
- **Alternate/Error Flows:**
  - If percentage is not between 0-100, display validation error

#### UC-005: System Administrator Creates Thesis Defense Record
- **Description:** Admin creates a complete thesis defense record with all required information
- **Pre-conditions:** User is logged in as Administrator; At least one active professor, student, university, and academic rank exist in the system
- **Post-conditions:** Thesis defense record is created; Compensation amount is automatically calculated
- **Main Flow:**
  1. Admin navigates to Thesis Defense Management section
  2. Admin clicks "Add New Thesis Defense"
  3. Admin selects professor from dropdown list (showing only active professors)
  4. Admin selects student from dropdown list (showing only active students)
  5. Admin selects university from dropdown list
  6. Admin selects defense date using Persian calendar date picker
  7. Admin selects cooperation type from options:
     - الف (Type A)
     - ب (Type B)
     - مدعو (Invited)
  8. Admin selects academic rank from defined ranks
  9. Admin enters grade (پایه)
  10. Admin selects thesis type:
     - ارشد (Master's)
     - دکتری (Doctorate)
  11. Admin selects unit count:
     - 4 واحد
     - 6 واحد
  12. Admin selects position:
     - راهنما (Supervisor)
     - مشاور (Advisor)
     - داور (Examiner)
     - ناظر (Observer)
  13. Admin selects participation level:
     - 0.5
     - 1
  14. Admin selects postal service status:
     - دارد (Has)
     - ندارد (Does not have)
  15. System automatically calculates compensation amount (مبلغ حق‌الزحمه) based on all parameters and supervision percentage
  16. Admin saves the record
  17. System validates all required fields
  18. System creates thesis defense record
  19. System displays success message with calculated compensation
- **Alternate/Error Flows:**
  - If required fields are missing, highlight them and prevent submission
  - If date is in invalid format, display error
  - If professor or student is inactive, display warning

#### UC-006: System Administrator Filters and Views Thesis Defense Records
- **Description:** Admin filters and searches through thesis defense records using multiple criteria
- **Pre-conditions:** User is logged in as Administrator; Thesis defense records exist in the system
- **Post-conditions:** Filtered list of records is displayed
- **Main Flow:**
  1. Admin navigates to Thesis Defense List section
  2. System displays table with all records showing:
     - Professor name (نام و نام خانوادگی استاد)
     - Professor national ID (کد ملی استاد)
     - Professor code (کد استاد)
     - Student name (نام و نام خانوادگی دانشجو)
     - Professor's faculty/workplace (دانشکده محل خدمت استاد)
     - Defense date (تاریخ دفاع)
     - Bank account (شماره حساب)
     - Cooperation type (نوع همکاری)
     - Academic rank (مرتبه علمی)
     - Grade (پایه)
     - Thesis type (پایان نامه)
     - Unit count (تعداد واحد)
     - Position (سمت)
     - Participation level (میزان مشارکت)
     - Postal service (پست)
     - Supervision percentage (درصد پایش)
     - Compensation amount (مبلغ حق‌الزحمه)
  3. Admin can filter by any column
  4. Admin can sort by any column
  5. Admin can search across multiple fields
  6. System updates table in real-time as filters are applied
- **Alternate/Error Flows:**
  - If no records match filters, display "No records found" message
  - If filter combination is too broad, display count of results

#### UC-007: System Administrator Manages Financial Transfers
- **Description:** Admin processes financial transfers to professor bank accounts
- **Pre-conditions:** User is logged in as Administrator; Thesis defense records with calculated compensation exist
- **Post-conditions:** Transfer is marked as processed; Account status is updated
- **Main Flow:**
  1. Admin navigates to Financial Management section
  2. System displays list of pending payments grouped by professor
  3. Admin selects one or more payments to process
  4. Admin reviews total amount and bank account details
  5. Admin marks payments as processed or initiates bank transfer
  6. System updates payment status to "Paid"
  7. System records transaction date and time
  8. System displays updated account status
- **Alternate/Error Flows:**
  - If bank account is invalid or missing, display error and prevent processing
  - If payment is already processed, display warning
  - Admin can mark payment as pending review if issues found

#### UC-008: Professor Views Personal Defense Records
- **Description:** Professor logs in and views their thesis defense participation records
- **Pre-conditions:** Professor account exists and is active
- **Post-conditions:** Professor sees their defense records and payment status
- **Main Flow:**
  1. Professor navigates to system URL
  2. Professor enters national ID as username
  3. Professor enters national ID as password (initially)
  4. System authenticates professor
  5. System displays professor dashboard showing:
     - List of thesis defenses they participated in
     - Payment status for each defense
     - Total compensation earned
  6. Professor can filter their own records by date, thesis type, position
- **Alternate/Error Flows:**
  - If credentials are invalid, display error message
  - If account is inactive, display "Account is deactivated" message
  - Professor should be prompted to change default password on first login

#### UC-009: Student Views Personal Thesis Defense Information
- **Description:** Student logs in and views information about their thesis defense
- **Pre-conditions:** Student account exists and is active
- **Post-conditions:** Student sees their thesis defense information
- **Main Flow:**
  1. Student navigates to system URL
  2. Student enters national ID as username
  3. Student enters national ID as password (initially)
  4. System authenticates student
  5. System displays student dashboard showing:
     - Their thesis defense record (if exists)
     - Defense date
     - Committee members (professors)
     - Defense status
  6. Student can view basic information but cannot edit
- **Alternate/Error Flows:**
  - If credentials are invalid, display error message
  - If account is inactive, display "Account is deactivated" message
  - Student should be prompted to change default password on first login
  - If no thesis defense is scheduled, display appropriate message

---

## 4. Functional Requirements

- **FR-1:** System shall support three user roles: Manager (Administrator), Professor (استاد), and Student (دانشجو)
- **FR-2:** System shall store professor information including first name, last name, national ID, professor code, bank account number, password, status (active/inactive), and role
- **FR-3:** System shall store student information including first name, last name, national ID, password, status (active/inactive), and role
- **FR-4:** System shall automatically set initial password to user's national ID (کد ملی)
- **FR-5:** System shall set new user accounts to "Active" status by default
- **FR-6:** System shall allow administrators to create, read, update, and delete professor records
- **FR-7:** System shall allow administrators to create, read, update, and delete student records
- **FR-8:** System shall maintain a list of universities with names
- **FR-9:** System shall maintain a list of academic ranks with names and supervision percentages (درصد پایش)
- **FR-10:** System shall allow administrators to create thesis defense records with all required fields
- **FR-11:** System shall display only active professors in the professor selection dropdown
- **FR-12:** System shall display only active students in the student selection dropdown
- **FR-13:** System shall provide Persian calendar (Jalali/Shamsi) date picker for defense date selection
- **FR-14:** System shall support cooperation types: الف (Type A), ب (Type B), مدعو (Invited)
- **FR-15:** System shall support thesis types: ارشد (Master's), دکتری (Doctorate)
- **FR-16:** System shall support unit counts: 4 units, 6 units
- **FR-17:** System shall support positions: راهنما (Supervisor), مشاور (Advisor), داور (Examiner), ناظر (Observer)
- **FR-18:** System shall support participation levels: 0.5, 1
- **FR-19:** System shall support postal service status: دارد (Has), ندارد (Does not have)
- **FR-20:** System shall automatically calculate compensation amount (مبلغ حق‌الزحمه) based on:
  - Cooperation type
  - Academic rank
  - Grade (پایه)
  - Thesis type (Master's/Doctorate)
  - Unit count (4/6)
  - Position (Supervisor/Advisor/Examiner/Observer)
  - Participation level (0.5/1)
  - Supervision percentage (درصد پایش)
- **FR-21:** System shall display comprehensive table of thesis defense records with all fields
- **FR-22:** System shall provide filtering capability on all table columns
- **FR-23:** System shall provide sorting capability on all table columns
- **FR-24:** System shall provide search functionality across multiple fields
- **FR-25:** System shall maintain financial records section for tracking transfers to professor accounts
- **FR-26:** System shall track payment status (Pending, Processed, Paid) for each thesis defense record
- **FR-27:** System shall allow administrators to mark payments as processed
- **FR-28:** System shall record transaction date and time for each payment
- **FR-29:** System shall display account status for each professor showing pending and completed payments
- **FR-30:** System shall allow professors to view their own defense records and payment status
- **FR-31:** System shall allow students to view their own thesis defense information
- **FR-32:** System shall restrict professors from viewing other professors' records
- **FR-33:** System shall restrict students from viewing other students' records
- **FR-34:** System shall validate national ID format and uniqueness
- **FR-35:** System shall validate bank account number format
- **FR-36:** System shall prevent duplicate thesis defense records for the same student-professor-date combination
- **FR-37:** System shall maintain audit log of all administrative actions (create, update, delete)
- **FR-38:** System shall support Persian/Farsi language for all user interface elements
- **FR-39:** System shall allow users to change their password from default national ID
- **FR-40:** System shall require authentication for all operations

---

## 5. Non-Functional Requirements

### Performance
- System must load thesis defense list table with up to 10,000 records within 2 seconds
- Filtering and search operations must return results within 1 second
- Compensation calculation must be instant (< 100ms)
- Date picker must respond within 500ms
- System must support at least 100 concurrent users without performance degradation

### Security
- All passwords must be hashed using bcrypt with minimum cost factor of 12
- System must enforce HTTPS for all connections
- National ID numbers must be validated and sanitized to prevent injection attacks
- Session tokens must expire after 24 hours of inactivity
- Role-based access control must be enforced at both frontend and backend
- Financial data must be encrypted at rest
- Bank account numbers must be partially masked in display (show only last 4 digits)
- Audit logs must be maintained for all financial transactions and cannot be deleted
- Users must be forced to change password on first login

### Reliability & Monitoring
- System uptime must be 99.5% or higher
- All financial transactions must be logged with timestamp and user ID
- System must perform daily automated backups
- Database must maintain referential integrity between professors, students, and thesis defenses
- System must log all failed login attempts
- System must alert administrators of unusual activities (multiple failed logins, large payment amounts)
- System must have rollback capability for financial transactions

### UX & Accessibility
- User interface must be fully in Persian/Farsi with right-to-left (RTL) text support
- Forms must provide clear validation messages in Persian
- Date picker must display Persian calendar months and year names
- Tables must be responsive and usable on tablets (minimum 768px width)
- System must provide keyboard navigation for all forms
- Error messages must be specific and actionable
- Success messages must confirm completed actions clearly
- Loading indicators must be shown for operations taking > 500ms

---

## 6. Integration & API Hints

### API Endpoints

#### POST /api/auth/login
- **Input:** `{national_id, password}`
- **Output:** `{token, user_role, user_name, expires_at}`
- **Purpose:** Authenticate user and return JWT token with role information

#### GET /api/professors
- **Input:** Query params: `{status: "active"/"inactive"/"all", page, limit}`
- **Output:** `{professors: [{id, name, national_id, professor_code, bank_account, status}], total, page}`
- **Purpose:** Retrieve list of professors with optional filtering

#### POST /api/professors
- **Input:** `{first_name, last_name, national_id, professor_code, bank_account}`
- **Output:** `{id, message, created_at}`
- **Purpose:** Create new professor account

#### PUT /api/professors/{id}
- **Input:** `{first_name, last_name, professor_code, bank_account, status}`
- **Output:** `{success, message}`
- **Purpose:** Update professor information

#### GET /api/students
- **Input:** Query params: `{status: "active"/"inactive"/"all", page, limit}`
- **Output:** `{students: [{id, name, national_id, status}], total, page}`
- **Purpose:** Retrieve list of students with optional filtering

#### POST /api/students
- **Input:** `{first_name, last_name, national_id}`
- **Output:** `{id, message, created_at}`
- **Purpose:** Create new student account

#### GET /api/universities
- **Input:** None
- **Output:** `{universities: [{id, name}]}`
- **Purpose:** Retrieve list of all universities

#### POST /api/universities
- **Input:** `{name}`
- **Output:** `{id, message}`
- **Purpose:** Create new university

#### GET /api/academic-ranks
- **Input:** None
- **Output:** `{ranks: [{id, name, supervision_percentage}]}`
- **Purpose:** Retrieve list of academic ranks with supervision percentages

#### POST /api/academic-ranks
- **Input:** `{name, supervision_percentage}`
- **Output:** `{id, message}`
- **Purpose:** Create new academic rank

#### POST /api/thesis-defenses
- **Input:** `{professor_id, student_id, university_id, defense_date, cooperation_type, academic_rank_id, grade, thesis_type, unit_count, position, participation_level, has_postal_service}`
- **Output:** `{id, calculated_compensation, message}`
- **Purpose:** Create thesis defense record and calculate compensation

#### GET /api/thesis-defenses
- **Input:** Query params for filtering: `{professor_id, student_id, university_id, date_from, date_to, cooperation_type, thesis_type, position, page, limit, sort_by, sort_order}`
- **Output:** `{defenses: [{id, professor_name, professor_national_id, professor_code, student_name, university_name, defense_date, bank_account, cooperation_type, academic_rank, grade, thesis_type, unit_count, position, participation_level, has_postal_service, supervision_percentage, compensation_amount, payment_status}], total, page}`
- **Purpose:** Retrieve thesis defense records with comprehensive filtering

#### GET /api/thesis-defenses/{id}
- **Input:** Defense ID
- **Output:** `{defense: {full defense details}}`
- **Purpose:** Retrieve single thesis defense record details

#### POST /api/financial/calculate-compensation
- **Input:** `{cooperation_type, academic_rank_id, grade, thesis_type, unit_count, position, participation_level, supervision_percentage}`
- **Output:** `{compensation_amount, calculation_breakdown}`
- **Purpose:** Calculate compensation amount based on parameters (for preview before saving)

#### GET /api/financial/pending-payments
- **Input:** Query params: `{professor_id (optional), page, limit}`
- **Output:** `{payments: [{defense_id, professor_id, professor_name, bank_account, compensation_amount, defense_date}], total_amount, page}`
- **Purpose:** Retrieve list of pending payments

#### POST /api/financial/process-payment
- **Input:** `{defense_ids: [], transaction_reference (optional)}`
- **Output:** `{success, processed_count, total_amount, transaction_id, message}`
- **Purpose:** Mark payments as processed

#### GET /api/financial/payment-history
- **Input:** Query params: `{professor_id (optional), date_from, date_to, page, limit}`
- **Output:** `{payments: [{defense_id, professor_name, amount, payment_date, transaction_id, status}], total, page}`
- **Purpose:** Retrieve payment history

#### GET /api/professors/{id}/defenses
- **Input:** Professor ID
- **Output:** `{defenses: [{defense details}], total_compensation, pending_amount, paid_amount}`
- **Purpose:** Retrieve all defenses for a specific professor (for professor's own view)

#### GET /api/students/{id}/defense
- **Input:** Student ID
- **Output:** `{defense: {defense details, committee_members: [professors]}}`
- **Purpose:** Retrieve thesis defense information for a specific student

### Dependencies
- **Database:** PostgreSQL or MySQL for relational data storage
- **Authentication Service:** JWT-based authentication system
- **Persian Calendar Library:** For Jalali/Shamsi date conversion and display
- **Reporting Service:** For generating financial reports and payment summaries
- **Backup Service:** For automated daily backups

---

## 7. Analytics & Success Metrics

### Key Metrics
- Number of thesis defenses recorded per semester
- Average compensation amount by cooperation type, thesis type, and position
- Professor participation distribution (how many defenses per professor)
- Student thesis defense completion rate
- Payment processing time (from defense date to payment completion)
- System adoption rate (percentage of university departments using the system)
- User login frequency (administrators, professors, students)
- Data entry error rate (corrections needed after initial entry)

### KPIs
- **Primary KPI:** Reduce administrative time for thesis defense management by 70% compared to manual processes
- **Financial KPI:** Process 100% of payments within 30 days of defense date
- **Accuracy KPI:** Maintain 99% accuracy in compensation calculations
- **User Adoption KPI:** Achieve 80% active professor registration within first 6 months
- **System Usage KPI:** Record at least 95% of all thesis defenses in the system
- **Efficiency KPI:** Reduce average time to create a thesis defense record to under 5 minutes

---

## 8. Risks & Open Questions

### Main Risks

- **Risk 1: Compensation Calculation Complexity**  
  The compensation formula depends on multiple variables and may be complex or change over time based on university policies.  
  **Mitigation:** Design calculation engine as a configurable module; maintain calculation formula documentation; implement audit trail for calculation changes; allow manual override with justification.

- **Risk 2: Data Migration from Existing Systems**  
  Universities may have existing records in spreadsheets or old systems that need to be migrated.  
  **Mitigation:** Provide data import functionality (CSV/Excel); create data validation tools; plan phased rollout with pilot department; provide data entry training.

- **Risk 3: Persian Calendar Date Handling**  
  Persian calendar conversion can be complex and error-prone, especially around year boundaries.  
  **Mitigation:** Use well-tested Persian calendar library; thoroughly test date conversions; display dates in both Persian and Gregorian formats for verification; validate date ranges.

- **Risk 4: Bank Account Security**  
  Storing bank account numbers presents security and compliance risks.  
  **Mitigation:** Encrypt bank account numbers at rest; implement strict access controls; partially mask numbers in display; conduct security audit; comply with financial data regulations.

- **Risk 5: User Adoption and Training**  
  Administrative staff, professors, and students may resist adopting new system or struggle with digital interface.  
  **Mitigation:** Conduct user training sessions; provide user manual in Persian; implement gradual rollout; gather user feedback; provide support hotline; design intuitive interface.

### Open Questions

- [ ] What is the exact formula for calculating compensation (حق‌الزحمه) based on all the parameters?
- [ ] Are there different base rates for different universities or are rates standardized?
- [ ] Should the system support multiple thesis defenses per student (e.g., if they fail first defense)?
- [ ] How should the system handle co-supervisors (multiple supervisors for one thesis)?
- [ ] What is the exact definition of "دانشکده محل خدمت استاد" (professor's workplace faculty) and should it be a required field?
- [ ] Should professors be able to update their own bank account information or only administrators?
- [ ] What is the approval workflow for payments (single approver, multiple approvers, automatic)?
- [ ] Should the system integrate with university's existing financial/ERP system?
- [ ] What reports need to be generated (monthly, annual, by department, by professor)?
- [ ] Should the system support bulk operations (import multiple defenses, bulk payment processing)?
- [ ] What is the data retention policy for historical records?
- [ ] Should there be different permission levels within the administrator role?

---

## 9. Acceptance Criteria

- [ ] Administrator can create professor account with all required fields (name, national ID, professor code, bank account)
- [ ] Administrator can create student account with all required fields (name, national ID)
- [ ] Default password is set to user's national ID for both professors and students
- [ ] New accounts are set to "Active" status by default
- [ ] Administrator can define universities with names
- [ ] Administrator can define academic ranks with names and supervision percentages
- [ ] Administrator can create thesis defense record selecting from active professors only
- [ ] Administrator can create thesis defense record selecting from active students only
- [ ] Persian calendar date picker is available and functional for defense date selection
- [ ] All cooperation types (الف, ب, مدعو) are available for selection
- [ ] All thesis types (ارشد, دکتری) are available for selection
- [ ] Unit count options (4, 6) are available for selection
- [ ] Position options (راهنما, مشاور, داور, ناظر) are available for selection
- [ ] Participation level options (0.5, 1) are available for selection
- [ ] Postal service status options (دارد, ندارد) are available for selection
- [ ] System automatically calculates compensation amount based on all parameters
- [ ] Comprehensive table displays all thesis defense records with all required columns
- [ ] Table supports filtering on all columns
- [ ] Table supports sorting on all columns
- [ ] Table supports search across multiple fields
- [ ] Financial management section displays pending payments grouped by professor
- [ ] Administrator can mark payments as processed
- [ ] System tracks payment status (Pending, Processed, Paid)
- [ ] System records transaction date and time for each payment
- [ ] Professor can log in using national ID and view their own defense records
- [ ] Professor can view their payment status and history
- [ ] Student can log in using national ID and view their thesis defense information
- [ ] System prevents professors from viewing other professors' records
- [ ] System prevents students from viewing other students' records
- [ ] System validates national ID format and enforces uniqueness
- [ ] System validates bank account number format
- [ ] All user interface elements are in Persian/Farsi language
- [ ] System supports right-to-left (RTL) text direction
- [ ] System enforces role-based access control (Manager, Professor, Student)
- [ ] Passwords are securely hashed using bcrypt
- [ ] Bank account numbers are encrypted at rest
- [ ] System maintains audit log of all administrative actions
- [ ] System performs daily automated backups
- [ ] All required fields are validated before saving records
- [ ] Clear error messages are displayed in Persian for validation failures
- [ ] Success messages are displayed after successful operations
- [ ] System loads thesis defense table with 1000+ records within 2 seconds
- [ ] Filtering and search operations return results within 1 second
- [ ] Users are prompted to change password on first login
- [ ] System session expires after 24 hours of inactivity

---

## 10. Technical Architecture Recommendations

### Recommended Tech Stack
- **Backend:** Python with Django or FastAPI framework
- **Database:** PostgreSQL 14+ (for robust relational data and JSON support)
- **Frontend:** React or Vue.js with RTL support
- **Persian Date Library:** persiantools (Python) or moment-jalaali (JavaScript)
- **Authentication:** Django built-in auth or JWT with djangorestframework-simplejwt
- **UI Framework:** Material-UI or Ant Design (both support RTL)
- **Reporting:** ReportLab (Python) for PDF generation in Persian

### Database Schema Highlights

**Users Table:**
- id, first_name, last_name, national_id (unique), password_hash, role (enum: Manager, Professor, Student), status (enum: Active, Inactive), created_at, updated_at

**Professors Table:**
- id, user_id (FK), professor_code (unique), bank_account, faculty_workplace

**Students Table:**
- id, user_id (FK)

**Universities Table:**
- id, name

**AcademicRanks Table:**
- id, name, supervision_percentage

**ThesisDefenses Table:**
- id, professor_id (FK), student_id (FK), university_id (FK), defense_date, cooperation_type (enum), academic_rank_id (FK), grade, thesis_type (enum), unit_count (enum), position (enum), participation_level (decimal), has_postal_service (boolean), calculated_compensation, payment_status (enum), payment_date, transaction_reference, created_at, updated_at, created_by_user_id (FK)

**AuditLog Table:**
- id, user_id (FK), action_type, table_name, record_id, old_values (JSON), new_values (JSON), timestamp, ip_address

---

**Status:** Draft  
**Reviewers:** University Administration, IT Department, Finance Department, Academic Affairs

---

## Appendix A: Persian-English Terminology Mapping

| Persian Term | English Translation | Context |
|--------------|---------------------|---------|
| مدیریت | Manager/Administrator | User role |
| استاد | Professor | User role |
| دانشجو | Student | User role |
| کد ملی | National ID | Identification number |
| کد استاد | Professor Code | Unique identifier |
| شماره حساب | Bank Account Number | Financial |
| وضعیت | Status | Active/Inactive |
| نقش | Role | User role |
| دانشگاه | University | Institution |
| مرتبه علمی | Academic Rank | Faculty rank |
| درصد پایش | Supervision Percentage | Calculation factor |
| دفاع پایان نامه | Thesis Defense | Academic event |
| تاریخ دفاع | Defense Date | Date field |
| نوع همکاری | Cooperation Type | Type of participation |
| الف | Type A | Cooperation type option |
| ب | Type B | Cooperation type option |
| مدعو | Invited | Cooperation type option |
| پایه | Grade | Academic level |
| پایان نامه | Thesis | Student work |
| ارشد | Master's | Degree level |
| دکتری | Doctorate | Degree level |
| تعداد واحد | Unit Count | Credit units |
| سمت | Position | Role in defense |
| راهنما | Supervisor | Position option |
| مشاور | Advisor | Position option |
| داور | Examiner | Position option |
| ناظر | Observer | Position option |
| میزان مشارکت | Participation Level | Contribution amount |
| پست | Postal Service | Delivery status |
| دارد | Has | Status indicator |
| ندارد | Does not have | Status indicator |
| حق‌الزحمه | Compensation | Payment amount |
| دانشکده محل خدمت | Faculty Workplace | Professor's department |

---

**Document End**
