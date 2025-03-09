# Hotel-Management-Application

Steps to Download It:
1. Click on mysetup.exe in files section.
2. Click on view raw.
3. Now, download is started.
4. After that follow the instruction for set up then run it.

But firstly you'll have to set-up database for it.
Download it:
https://drive.google.com/file/d/1_LGZZOL9x2HUSArVoy2M4Sl6eCJ1JZqw/view
How to set it up:
https://youtu.be/Fh-1eO8SA9o?si=gCeBVRRMNdB4L38g

Code to copy and paste in database:
CREATE TABLE Users (user_id NUMBER PRIMARY KEY, name VARCHAR2(100) NOT NULL, contact VARCHAR2(15) NOT NULL, email VARCHAR2(100) NOT NULL UNIQUE, password VARCHAR2(100) NOT NULL);
CREATE SEQUENCE user_id_seq
       START WITH 1
       INCREMENT BY 1
       NOCACHE;
CREATE OR REPLACE TRIGGER user_id_trigger
   BEFORE INSERT ON Users
   FOR EACH ROW
   BEGIN
       IF :NEW.user_id IS NULL THEN
           SELECT user_id_seq.NEXTVAL INTO :NEW.user_id FROM dual;
       END IF;
   END;
   /
CREATE TABLE Rooms ( room_id NUMBER  PRIMARY KEY, room_type VARCHAR2(50) NOT NULL, price NUMBER(10, 2) NOT NULL, available CHAR(1) DEFAULT 'Y' CHECK (available IN ('Y', 'N')));
CREATE TABLE Reservations (reservation_id NUMBER  PRIMARY KEY, user_id NUMBER REFERENCES Users(user_id), room_id NUMBER REFERENCES Rooms(room_id), check_in_date DATE NOT NULL, check_out_date DATE NOT NULL, no_of_guests NUMBER NOT NULL, total_amount NUMBER(10, 2) NOT NULL);
CREATE TABLE Payments ( payment_id NUMBER  PRIMARY KEY, reservation_id NUMBER REFERENCES Reservations(reservation_id), payment_mode VARCHAR2(50) NOT NULL, payment_status VARCHAR2(50) DEFAULT 'Pending');
INSERT INTO Rooms VALUES (1001,'Single Room', 1000.00, 'Y');
INSERT INTO Rooms VALUES (1002,'Double Room', 1500.00, 'Y');
INSERT INTO Rooms VALUES (1003,'VIP Room', 3000.00, 'Y');
