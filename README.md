# Design DB model for Guvi Zen class.

## Here I create 22 tables, the names are

- courses
- batchTable
- students
- absentRecords
- rolesInfo
- employeesTable
- employeeLeaveRecords
- portFolioTable
- projectTable
- task
- taskComplete
- sessions
- sessionComplete
- feedbackTable
- recLink
- queryTable
- certificates
- mockInterview
- companies
- position
- placementRecords
- salaryRecords

## How I create the tables like using below querys

```sql
create database zenClassDB;

use zenClassDB;

create table courses(
    course_id int primary key,
    course_name varchar(30) not null unique,
    fees float not null,
    duration int not null,
    syllabus text not null
);

create table batchTable (
    batch_id int primary key,
    batch_name varchar(50) not null,
    coordinator_id int not null,
    mentor_id int not null,
    course_id int not null,
    startDate date not null,
    endDate date not null,
    complete boolean not null,
    total_student int not null,
    timing varchar(30)
);

create table students (
    student_id int primary key,
    student_name varchar(50) not null,
    student_email varchar(50) not null,
    mobile_number int(15) not null,
    pass_word varchar(255) not null,
    experience int default 0,
    degree varchar(50) not null,
    CGPA float not null,
    batch_id int(20) not null,
    batch_name varchar(50) not null,
    employee_id int not null
);

create table absentRecords (
    absentee_id int primary key,
    student_id int not null,
    no_of_days int not null,
    from_date date not null,
    to_date date not null,
    reason text not null,
);

create table rolesInfo(
    role_id int primary key,
    role_name varchar(20) not null unique
);

create table employeesTable(
    employee_id int primary key,
    employee_name varchar(50) not null,
    username varchar(20) unique not null,
    pass_word varchar(20) not null,
    mobile varchar(10) unique not null,
    years_of_experience int default 0,
    salary float not null,
    role_id int not null
);

create table employeeLeaveRecords(
    leave_id int primary key,
    employee_id int,
    from_date date,
    to_date date,
    no_of_days int default 1,
    reason text not null,
);

create table portFolioTable(
    portFolio_id int primary key,
    student_id int not null,
    github_link varchar(255) not null,
    portFolio_link varchar(255) not null,
    resume_link varchar(255) not null
);

create table projectTable(
    project_id int primary key,
    student_id int not null,
    project_link varchar(255) not null,
    github_link varchar(255) not null
);

create table task (
    task_id int primary key,
    task_question text not null,
    session_id int(20) not null,
);

create table taskComplete (
    task_id int primary key,
    student_id int not null,
    task_mark int not null,
    complete boolean not null
);

create table sessions (
    session_id int primary key,
    session_name varchar(255) not null,
    meeting_link text,
    pass_word varchar(25) not null,
    task_id int not null,
    contents varchar(1000) not null,
    Pre_read varchar(255) not null
);

create table sessionComplete (
    session_id int primary key,
    employee_id int(20) not null,
    batch_id int(20) not null,
    complete boolean not null
);

create table feedbackTable(
    feedback_id int primary key,
    session_id int not null,
    student_id int not null,
    session_rating float not null,
    session_feedback text not null,
    mentor_rating float not null,
    mentor_feedback text not null,
    key_takeaways text not null
);

create table recLink (
    rec_id int primary key,
    session_id int(20) not null,
    link varchar(255) not null,
    pass_word varchar(255) not null
);

create table certificates (
    certificate_id int auto_increment primary key,
    student_id int not null,
    certificate_url varchar(100) not null
);

create table queryTable (
    query_id int primary key,
    student_id int not null,
    category varchar(255) not null,
    Communication_Language varchar(255) not null,
    query_description varchar(255) not null,
    attachments varchar(255) not null,
    availableFrom time not null,
    availableTill time not null,
    employee_id int(20) not null,
    complete boolean not null
);

create table mockInterview (
    mockinterview_id int primary key,
    employee_id int not null,
    batch_id int not null,
    student_id int not null,
    selectedState boolean not null
);

create table companies (
    company_id int primary key,
    company_name varchar(100) not null unique,
    company_location varchar(100) not null,
    tier int
);

create table position (
    position_id int primary key,
    company_id int not null,
    position_name varchar(100) not null,
    package int not null,
    details text not null,
    no_of_vacancies int not null,
);

create table placementRecords (
    placement_record_id int auto_increment primary key,
    student_id int,
    company_id int,
    position_id int,
    batch_id int
);

create table salaryRecords(
    salary_id int primary key,
    employee_id int not null,
    amount float not null,
    credit_date_time datetime
);
```

## Relationship

- Employees have a leave application
- Employees have a roles info
- Employees have a salary record
- Employees have a session
- Employees have a batch
- Employees have a queries
- Students have a batch
- Students have a leave application
- Students have a portfolio
- Students have a project
- Students have a task complete
- Students have a feedback
- Students have a query's
- Students have a certificate
- Students have a placement record
- Students have a mock interview
- Course have a batch
- Batch have a session
- Session have a recordings
- Session have a task
- Session have a feedback
- Company have a position
- Position have a placement record
