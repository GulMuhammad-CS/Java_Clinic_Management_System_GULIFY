README FOR GULIFY CLINIC MANAGEMENT SYSTEM:
(0) Important information before starting:

0.A
 The system utilizes SQLite to store data in a database. In order to view this data, it is recommended to install DB Browser as a way to access the database directly for any reason, such as that stated in section 6. The official link for installing DB Browser is: https://sqlitebrowser.org/dl/ . To view the database, start DB Browser, click open database, and open the Clinic_database.db which should be present in the project directory.

0.B
 The system is initially empty to allow for a demonstration of the setup chronology, after which the user may input the data in section 6 for testing

(1) SETUP:
1.A
 Open the project folder in IntelliJ IDEA
1.B
 Navigate to the file called ClinicApplication.Java
1.C
 Run the file (automatically creates database and its tables if they don't already exist, within project directory)
1.D
 When running, users may select whether they are a administrator, doctor, or patient. Entering any one of these credentials in another login page would not be accepted and the user would not be able to proceed
Flow of setting up system for first time:
1.D.i
 Admin logs in with Super User credentials as follows (please note that these emails and the domains are purely fictional, and are purely designed for this system's functionality):
1.D.ii.a 
 Email: SystemAdmin@clincare.com
1.D.iii.b 
 Password: SystemSuperAdmin
1.E
 After logging in with super admin details, program will redirect them to registration page, where the admin may register with their own details, name, email, and password
1.F
 Following this the admin is finally prompted to log in with the details they just registered. Important to note is that following this log in, the super admin credentials will be deleted from the database for the sake of security, to ensure that anyone can’t access the system even if they can view the super admin credentials.
1.G
 The purpose of the super admin is simply to provide a first time admin some access to the system so that they may begin setting it up to implement it for their clinic


(2)ADMINS:

 After logging in, admins can work to add the following:

2.A
 Specialties to be offered by their doctors (cardiology, general practitioner, general surgeon, etc)

2.B
 Doctors at the clinic (their respective specialty must be available in the database if it hasn’t already been added)

2.C
 Medicines available in the clinic to be prescribed by doctors to their patients

2.D
 Patients based on any documentation they may have filled out when first visiting the clinic, each patient is automatically assigned to a certain doctor, which may be the first doctor to treat them. Admins may register the same patient under different doctors if they require multiple types of care, but if they try registering a patient again with the same doctor, it will show an error.

2.E
 Admins may also facilitate changing the doctor of a patient by registering them under a new doctor while removing them from the care of the previous doctor.

2.F
 Admins may also remove any of the data by selecting the record on the table and pressing the remove button

2.G
 Lastly, admins may also add new administrators by filling in their basic information in the system

2.H
 Important to note: all employees of the clinic (admins & doctors) would have the special email domain “@clincare.com”. The system will look for this domain when registering or logging in, should the system not see this domain it will alert the user 

(3)DOCTORS:

 Once a doctor’s credentials have been registered in the system, they may use those credentials to log in to the system and do any of the following tasks:

3.A
 Toggle their status, any patient may not request for an appointment for a doctor who has ‘not available’ as their status. Appointment booking system is explained in section 4

3.B
 View the medicines available in the clinic for their own reference, to view the ID so that they may prescribe it to any of their patients for example

3.C
 View past appointments, which may have been cancelled, rejected, or completed (cancelled and rejected appointments share the same status as ‘cancelled’)

3.D
 View appointment requests:

3.D.i 
 This shows 2 more buttons, one to accept and one to reject appointment requests, also done by selecting the appropriate table row and pressing either button to accept or reject

3.E
 View and add patients, doctorID is automatically inputted based on the current doctor using the system

3.F
 View and add prescriptions, done by entering the respective patientID, medicine name (advil, Panadol, Glucophage, etc), and selecting the options which may appear for the medicine for its dosage form and strength

3.G
 View upcoming appointments and book appointments on their own behalf, doctorID is also automatically inputted

3.H
 They may also view their own email, name, and status in the system

3.I
 Doctors may also remove/cancel prescriptions, appointments, or patients, they are not able to remove medicines

(4) 
A doctor may book an appointment on a patients’ behalf, after which (if the slot is available) the status is automatically ‘upcoming’. However a patient may only request an appointment by filling out a form for their desired doctor, date, and time. A doctor  may view these requests from patients and accept/reject them as necessary. They can view any accepted appointments in the upcoming appointments table and rejected appointments in the past appointments table

(5)PATIENTS:

 Patients (once they receive their credentials by an appropriate medium from the clinic) may log into the system to:

5.A 
 View their current prescriptions and which doctor it is from

5.B 
 Request an appointment from a doctor, by:

5.B.i
 Selecting desired specialty

5.B.ii
 Selecting the desired doctor from that specialty

5.B.iii
 selecting a valid date and time

5.C
 change their login password for security

5.D
 patients may also cancel appointments if need be 

(6) SQL QUERIES FOR INSERTING TESTING DATA

recommended to only execute these queries in the SQLite DB Browser once admin has been set up. The purpose of inputting this data is simply for demonstration sake, for example for the sake of demonstrating appointment bookings, or handling prescriptions. The system is also capable of running without this data, it is simply for ease of demonstration. To add this information, click on Execute SQL tab, and copy and paste the code below. It will automatically insert data into all tables save for prescriptions and appointments, as those are added in their own system. Lastly, please note that all the information below regarding any admin, doctor, or patient are purely fictional, and are not meant to resemble any person.

-- Insert Admins:
INSERT INTO Admins (AdminName, AdminEmail, AdminPassword, AccessLevel) VALUES
('alice', 'alice@clincare.com', '12345678', 2),
('bob', 'bob@clincare.com', '12345678', 2),
('charlie', 'charlie@clincare.com', '12345678', 2),
('dave', 'dave@clincare.com', '12345678', 2),
('eve', 'eve@clincare.com', '12345678', 2);

-- Insert Specialties:
INSERT INTO Specialties (Specialty) VALUES
('cardiology'),
('neurology'),
('orthopedics'),
('pediatrics'),
('oncology'),
('dermatology'),
('gastroenterology');

-- Insert Doctors:
INSERT INTO Doctors (DoctorName, DoctorEmail, DoctorPassword, SpecialtyID, Status) VALUES
('dr. alice', 'alice@clincare.com', '12345678', 1, 'available'), 
('dr. bob', 'bob@clincare.com', '12345678', 2, 'available'),
('dr. charlie', 'charlie@clincare.com', '12345678', 3, 'available'),
('dr. dana', 'dana@clincare.com', '12345678', 3, 'available'), 
('dr. emily', 'emily@clincare.com', '12345678', 4, 'available'),
('dr. frank', 'frank@clincare.com', '12345678', 5, 'available'), 
('dr. grace', 'grace@clincare.com', '12345678', 5, 'available'), 
('dr. helen', 'helen@clincare.com', '12345678', 6, 'available'), 
('dr. ian', 'ian@clincare.com', '12345678', 7, 'available');

-- Insert Medicines:
INSERT INTO Medicines (MedicineName, MedicineSalt, MedicineDosageForm, MedicineDosageStrength) VALUES
('lipitor', 'atorvastatin calcium', 'tablet', '10 mg'),
('voltaren', 'diclofenac sodium', 'tablet', '50 mg'),
('norvasc', 'amlodipine besylate', 'tablet', '5 mg'),
('delsym', 'dextromethorphan hydrobromide', 'liquid suspension', '30 mg/5 ml'),
('prozac', 'fluoxetine hydrochloride', 'capsule', '20 mg'),
('augmentin', 'amoxicillin and clavulanic acid', 'tablet', '500 mg/125 mg'),
('zoloft', 'sertraline hydrochloride', 'tablet', '50 mg'),
('advil', 'ibuprofen', 'tablet', '200 mg'),
('synthroid', 'levothyroxine sodium', 'tablet', '100 mcg'),
('tylenol', 'acetaminophen', 'tablet', '500 mg'),
('cipro', 'ciprofloxacin', 'tablet', '250 mg'),
('allegra', 'fexofenadine hydrochloride', 'tablet', '180 mg');


-- Insert Patients:
INSERT INTO Patients (PatientEmail, Password, DoctorID, PatientName, PatientAge, Gender, DateOfBirth) VALUES
('john@gmail.com', '12345678', 1, 'john doe', 35, 'male', 638166000000),
('mary@gmail.com', '12345678', 2, 'mary smith', 29, 'female', -599616000000),
('alex@gmail.com', '12345678', 3, 'alex brown', 40, 'male', 501436800000),
('susan@gmail.com', '12345678', 4, 'susan white', 31, 'female', 776250000000),
('robin@gmail.com', '12345678', 5, 'robin taylor', 25, 'other', 898569600000),
('chris@gmail.com', '12345678', 6, 'chris johnson', 38, 'male', 547953600000),
('lisa@gmail.com', '12345678', 7, 'lisa moore', 45, 'female', -257788800000),
('daniel@gmail.com', '12345678', 3, 'daniel wilson', 50, 'male', 101953920000),
('emma@gmail.com', '12345678', 4, 'emma davis', 27, 'female', 842774400000),
('jamie@gmail.com', '12345678', 5, 'jamie lee', 34, 'other', 602524800000);
