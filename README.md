# 🏨 Hotel Management Application

This is a Hotel Management Application that helps manage users, rooms, reservations, and payments.  

---

## 📥 Steps to Download & Install

1. Go to the **Files** section of the repository.  
2. Click on **`mysetup.exe`**.  
3. Click on **View Raw**.  
4. The download will start automatically.  
5. After downloading, follow the setup instructions and run the application.  

---

## 🗄️ Database Setup

Before running the application, you need to set up the database.  

### ▶️ Download Database
- [Download Database File](https://drive.google.com/file/d/1_LGZZOL9x2HUSArVoy2M4Sl6eCJ1JZqw/view)  

### 📺 Setup Guide
- [Watch Database Setup Tutorial](https://youtu.be/Fh-1eO8SA9o?si=gCeBVRRMNdB4L38g)

  Keep in mind for using this when you are setting up password set it: 993097(then only it will work. I am working on it soon will update till then...)

### 📜 SQL Code

Copy & paste the following SQL code into your database (Oracle/SQL environment):  

```SQL*PLUS
#Create Users Table
CREATE TABLE Users (
user_id NUMBER PRIMARY KEY,
name VARCHAR2(100) NOT NULL,
contact VARCHAR2(15) NOT NULL,
email VARCHAR2(100) NOT NULL UNIQUE,
password VARCHAR2(100) NOT NULL
); 
```

 ```SQL*PLUS
#Auto-increment for user_id
CREATE SEQUENCE user_id_seq
START WITH 1
INCREMENT BY 1
NOCACHE;
```

```SQL*PLUS
CREATE OR REPLACE TRIGGER user_id_trigger
BEFORE INSERT ON Users
FOR EACH ROW
BEGIN
IF :NEW.user_id IS NULL THEN
SELECT user_id_seq.NEXTVAL INTO :NEW.user_id FROM dual;
END IF;
END;
/
```

```SQL*PLUS
#Create Rooms Table
CREATE TABLE Rooms (
room_id NUMBER PRIMARY KEY,
room_type VARCHAR2(50) NOT NULL,
price NUMBER(10, 2) NOT NULL,
available CHAR(1) DEFAULT 'Y' CHECK (available IN ('Y', 'N'))
);
```
```SQL*PLUS
#Create Reservations Table
CREATE TABLE Reservations (
reservation_id NUMBER PRIMARY KEY,
user_id NUMBER REFERENCES Users(user_id),
room_id NUMBER REFERENCES Rooms(room_id),
check_in_date DATE NOT NULL,
check_out_date DATE NOT NULL,
no_of_guests NUMBER NOT NULL,
total_amount NUMBER(10, 2) NOT NULL
);
```
```SQL*PLUS
#Create Payments Table
CREATE TABLE Payments (
payment_id NUMBER PRIMARY KEY,
reservation_id NUMBER REFERENCES Reservations(reservation_id),
payment_mode VARCHAR2(50) NOT NULL,
payment_status VARCHAR2(50) DEFAULT 'Pending'
);
```
```SQL*PLUS
#Insert Default Rooms
INSERT INTO Rooms VALUES (1001,'Single Room', 1000.00, 'Y');
INSERT INTO Rooms VALUES (1002,'Double Room', 1500.00, 'Y');
INSERT INTO Rooms VALUES (1003,'VIP Room', 3000.00, 'Y');
```

---

## 🚀 Features

- User registration & login  
- Room booking & availability check  
- Manage reservations  
- Process payments  

---

## 📝 Notes

- Ensure your database is correctly set up before running the application.  
- Default rooms are already added to the system.  

---

## 👨‍💻 Author

Developed for demonstration of **Hotel Management System** database and application workflow.

**Made with ❤️ by Manas Shukla**

---

## 🌐 Socials:
[![Portfolio](https://img.shields.io/badge/Portfolio-Website-blue)](https://manas-shukla-portfolio.framer.website) [![Instagram](https://img.shields.io/badge/Instagram-%23E4405F.svg?logo=Instagram&logoColor=white)](https://instagram.com/manas_shukla_101) [![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://linkedin.com/in/manas-shukla-006774370) [![email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:shuklamanas8928@gmail.com) 

---
---

_Created with ♥️ for my senior._
