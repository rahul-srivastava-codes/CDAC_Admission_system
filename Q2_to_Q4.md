2. Study database constraints in depth: PRIMARY KEY, FOREIGN-KEY, UNIQUE, CHECK, DEFAULT
Apply appropriate constraints in CDAC admission system.
3. Learn about composite keys and candidate keys
Identify keys in CDAC admission system.
4. Explore AUTO_INCREMENT / SEQUENCES
Use appropriate AUTO_INCREMENT keys in CDAC admission system

CREATE DATABASE CDAC_Admission_system;
USE CDAC_Admission_system;

CREATE TABLE CCAT_Result (
    form_no CHAR(6) PRIMARY KEY,
    name VARCHAR(30) NOT NULL,
    ccat_rank INT UNIQUE,
    CHECK (ccat_rank > 0)
);

CREATE TABLE Address (
    address_id INT AUTO_INCREMENT PRIMARY KEY,
    street VARCHAR(50),
    city VARCHAR(30) NOT NULL,
    state VARCHAR(30) NOT NULL,
    pincode CHAR(6)
);

CREATE TABLE Student_detail (
    form_no CHAR(6) PRIMARY KEY,
    address_id INT NOT NULL,

    FOREIGN KEY (form_no) 
        REFERENCES CCAT_Result(form_no)
        ON DELETE CASCADE,

    FOREIGN KEY (address_id) 
        REFERENCES Address(address_id)
);

CREATE TABLE Courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(40) UNIQUE NOT NULL,
    course_fees DECIMAL(10,2) NOT NULL,
    CHECK (course_fees > 0)
);

CREATE TABLE Cdac_Centre (
    centre_id INT AUTO_INCREMENT PRIMARY KEY,
    centre_name VARCHAR(40) NOT NULL,
    centre_pincode CHAR(6),
    centre_capacity INT,
    CHECK (centre_capacity > 0)
);

CREATE TABLE Preferences (
    preference_id INT AUTO_INCREMENT PRIMARY KEY,
    form_no CHAR(6) NOT NULL,
    centre_id INT NOT NULL,
    course_id INT NOT NULL,
    preference_no INT NOT NULL,
    freeze BOOLEAN DEFAULT FALSE,

    CHECK (preference_no > 0),

    UNIQUE (form_no, preference_no),

    FOREIGN KEY (form_no) 
        REFERENCES CCAT_Result(form_no)
        ON DELETE CASCADE,

    FOREIGN KEY (centre_id) 
        REFERENCES Cdac_Centre(centre_id),

    FOREIGN KEY (course_id) 
        REFERENCES Courses(course_id)
);
