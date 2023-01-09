# KangarooFitness
The following information is included in my group's report of our project which can also be viewed in the report files.
The database and queries can be viewed within our Microsoft Access File. 
We were assigned to create a database based off of our selected business proposal. 
All prinouts are able to be viewed within the file itself. 

Phase I – Proposal/Introduction
Narrative Description (Business, Problem, Opportunity)

The biggest challenges facing gyms on both the client and business sides are impersonal environments, long waits for equipment, and high-maintenance locations. Kangaroo Fitness aims to deliver bespoke personal training services by matching specialized trainers with our customers. Even better, this is all done through our supply system which brings any requested equipment necessary to the training location of the customer’s choice.
The appointments are the focal point of our data collection, as they track the training location and bidirectional ratings for the trainers and users. The appointments will also track which services and equipment were requested. One appointment may have more than one service and more than one equipment needed. We want basic information from our trainers and users.
We need to know our trainers’ specializations and hourly rates. We want to know the workout service types, subtypes, and which equipment they require. Our workout services will also have a rate associated with them as trainers will be able to charge on top of it. We want to know the equipment name, manufacturer, type, and subtype. The equipment will be stored at shipping facilities, which will have their basic information stored.


Information Needs
-	Customer and Trainer Reviews
-	Trainer specializations and rates
-	Equipment type and subtypes
-	Storage facilities
-	Service types
-	Appointment location and services rendered


Initial List of Entities Identified
-	Locations
-	Customers
-	Equipment
-	Trainers
-	Other Employees
-	Departments
-	Appointments
-	Vehicles
 
Final List of Entities
-	Appointments
-	Trainers
-	Users
-	Shipping Facilities
-	Equipment
-	Workout Services
-	AppointmentEquipment (intersection)
-	AppointmentServices (intersection)


Roles and Duties
-	Group Spokesperson (David, Victor)
o	Responsible for communication with professor
o	Email by 11:30 PM of due dates
-	Systems Analyst (Victor, Kazi)
o	Entity Relationship diagram
o	Convert to a relationship model
o	Normalization
-	Database (Kelvin)
o	Implement tables SQL CREATE TABLE
-	Application Developer (Kelvin, Calvin)
o	Forms, reports, queries, menus, navigation
o	Example printouts of forms
-	Documentation Writer (David, Victor)
o	Responsible for writing final report
o	Screenshots

Phase II – Systems Analysis

Comments

·	No relationship lines cross in any way. They either are going horizontally or vertically.

·	We decided on not allowing overlapping appointments with services rendered and trainers to make it easier.

·	Trainers and users would rate each other after every appointment.

·	Clients are charged a flat rate for any service and trainers charge an hourly rate based on their expertise.
Relationship Sentences


One USER may be booking one or more APPOINTMENTS.

One APPOINTMENT must be assigned to one and only one USER.
One APPOINTMENT may be a reservation to provide one or more SERVICES RENDERED. One SERVICE RENDERED must be a specific service rendered by one and only one
APPOINTMENT.

One APPOINTMENT must select one and only one TRAINER. One TRAINER may be assigned to one or more APPOINTMENTS.
One TRAINER may be assigned to one or more SHIPPING FACILITIES. One SHIPPING FACILITY may serve one or more TRAINERS.
One SHIPPING FACILITY may hold one or more VEHICLES.

One VEHICLE must be stored in one and only one SHIPPING FACILITY. One SHIPPING FACILITY may store one or more EQUIPMENT.
One EQUIPMENT must be stored in one or more SHIPPING FACILITIES. One EQUIPMENT must be assigned to one or more SERVICE RENDERED. One SERVICE RENDERED may require one or more EQUIPMENTS.
One SERVICE RENDERED must be a rendering of one and only one WORKOUT SERVICE.

One WORKOUT SERVICE may be a service rendered as one or more SERVICE RENDERED.
Phase III – Logical and Physical Modeling

Normalization

Trainers(TrainerID (key), FirstName, LastName, PhoneNumber, EmailAddress, Gender, ServiceSpecialization, HourlyRate)

Key: TrainerID

FD1: TrainerID -> FirstName, LastName, PhoneNumber, EmailAddress, Gender, ServiceSpecialization, HourlyRate

1NF: Meets the definition of a relation 2NF: No partial key dependencies 3NF: No transitive dependencies
 

ShippingFacilities(FacilityID (key), Street, City, State, PostalCode, PhoneNumber, EmailAddress)

FD1: FacilitiesID -> Street, City, State, PostalCode, PhoneNumber, EmailAddress FD2: PostalCode -> City, State
1NF: Meets the definition of a relation 2NF: No partial key dependencies
3NF: Transitive dependency exists: PostalCode -> City, State

Solution: Split Trainers relation into two new relations named ShippingFacilitiesData and PostalCode:

ShippingFacilitiesData(FacilityID (key), Street, PostalCode (fk), PhoneNumber, EmailAddress) FD1: FacilitiesID -> Street, PostalCode, PhoneNumber, EmailAddress
1NF: Meets the definition of a relation 2NF: No partial key dependencies 3NF: No transitive dependencies
 
PostalCode(PostalCode (key), City, State) FD1: PostalCode -> City, State
1NF: Meets the definition of a relation 2NF: No partial key dependencies 3NF: No transitive dependencies
 

Appointments(AppointmentID (key), StartDateTime, EndDateTime, Street, ApartmentSuite, City, State, PostalCode, TrainerRating, UserRating)

FD1: AppointmentID -> StartDateTime, EndDateTime, Street, ApartmentSuite, City, State, PostalCode, TrainerRating, UserRating

FD2: PostalCode -> City, State

1NF: Meets the definition of a relation 2NF: No partial key dependencies
3NF: Transitive dependency exists: PostalCode -> City, State

Solution: Split Trainers relation into two new relations named AppointmentData and PostalCode. PostalCode has already been created:

AppointmentsData(AppointmentID (key), StartDateTime, EndDate, TimeStreet, ApartmentSuite, City, State, PostalCode (fk), TrainerRating, UserRating)

FD1: AppointmentID -> StartDateTime, EndDateTime, Street, ApartmentSuite, PostalCode, TrainerRating, UserRating

1NF: Meets the definition of a relation 2NF: No partial key dependencies 3NF: No transitive dependencies
 

Equipment(EquipmentID (key), Name, Manufacturer, Type, Subtype) FD1: EquipmentID -> Name, Manufacturer, Type, Subtype
1NF: Meets the definition of a relation
 

2NF: No partial key dependencies 3NF: No transitive dependencies
 

WorkoutServices(ServiceID (key), Type, Subtype, ServicePrice, EquipmentType) FD1: ServiceID -> Type, Subtype, ServicePrice, EquipmentType
1NF: Meets the definition of a relation 2NF: No partial key dependencies 3NF: No transitive dependencies
 

Users(UserID (key), FirstName, LastName, PhoneNumber, EmailAddress, Birthdate, Gender) FD1: UserID -> FirstName, LastName, PhoneNumber, EmailAddress, Birthdate, Gender 1NF: Meets the definition of a relation
2NF: No partial key dependencies 3NF: No transitive dependencies
 

AppointmentsEquipment (AppointmentID (key), EquipmentID (fk)) FD1: AppointmentID -> EquipmentID
1NF, 2NF, 3NF: All key


AppointmentsServices (AppointmentID (key), ServiceID (fk)) FD1: AppointmentID -> ServiceID
1NF, 2NF, 3NF: All key

 
Final Set of Relations

Trainers(TrainerID (key), FirstName, LastName, PhoneNumber, EmailAddress, Gender, ServiceSpecialization, HourlyRate)

ShippingFacilitiesData(FacilityID (key), Street, PostalCode (fk), PhoneNumber, EmailAddress) PostalCode(PostalCode (key), City, State)
AppointmentsData(AppointmentID (key), StartDateTime, EndDate, TimeStreet, ApartmentSuite, City, State, PostalCode (fk), TrainerRating, UserRating, UserID (fk), TrainerID (fk))

Equipment(EquipmentID (key), Name, Manufacturer, Type, Subtype) WorkoutServices(ServiceID (key), Type, Subtype, ServicePrice, EquipmentType) Users(UserID (key), FirstName, LastName, PhoneNumber, EmailAddress, Birthdate, Gender) AppointmentEquipment (AppointmentID (key), EquipmentID (fk))
AppointmentServices (AppointmentID (key), ServiceID (fk))


Comments

-	Due to the E-R model revision removing the “Vehicles” entity, we decided to remove the “Weight” attribute from the “Equipment” entity because it was analogous to cargo load.

-	In the “Trainers” entity, we considered a functional dependency between
“ServiceSpecialization” and “HourlyRate” but our business will allow trainers to choose the rate that they charge and we will take a percentage of it. This will allow more experienced trainers to earn what they believe they deserve.

-	PostalCode entity is shared between “ShippingFacilitiesData” and “AppointmentsData”.

-	Two intersection relations were created per E-R model revision.
Phase IV – Database Implementation

SQL CREATE TABLE and ALTER TABLE Statements

CREATE TABLE trainers(
trainerID INTEGER NOT NULL PRIMARY KEY,
first_name VARCHAR(20) NOT NULL, last_name VARCHAR(20) NOT NULL, phone_number VARCHAR(20) NOT NULL, email_address VARCHAR(40) NOT NULL, gender VARCHAR(20), service_specialization VARCHAR(30), hourly_rate CURRENCY NOT NULL
);

CREATE TABLE appointments(
appointmentID INTEGER NOT NULL PRIMARY KEY,
start_date_time DATETIME, end_date_time DATETIME, street VARCHAR(20), appartment_suite VARCHAR(20), city VARCHAR(20),
state VARCHAR(2), postal_code VARCHAR(10), trainer_rating NUMBER, user_rating NUMBER, trainerID INTEGER NOT NULL, userID INTEGER NOT NULL
);

CREATE TABLE users(
userID INTEGER NOT NULL PRIMARY KEY,
first_name VARCHAR(20) NOT NULL, last_name VARCHAR(20) NOT NULL, phone_number VARCHAR(20) NOT NULL, email_address VARCHAR(40) NOT NULL, birth_date DATE,
gender VARCHAR(20)
);

CREATE TABLE shipping_facilities(
facilityID INTEGER NOT NULL PRIMARY KEY,
street VARCHAR(20), city VARCHAR(20),
state VARCHAR(2),
 
postal_code VARCHAR(10), phone_number VARCHAR(20) NOT NULL, email_address VARCHAR(40) NOT NULL
);

CREATE TABLE equipment(
equipmentID INTEGER NOT NULL PRIMARY KEY, name VARCHAR(20),
manufacturer VARCHAR(20), type VARCHAR(20),
subtype VARCHAR(20), facilityID INTEGER NOT NULL
);

CREATE TABLE workout_services(
serviceID INTEGER NOT NULL PRIMARY KEY, type VARCHAR(20),
subtype VARCHAR(20), service_price CURRENCY NOT NULL, equipment_type VARCHAR(20)
);

CREATE TABLE appointment_equipment( appointmentID INTEGER NOT NULL, equipmentID INTEGER NOT NULL
);

CREATE TABLE appointment_services( appointmentID INTEGER NOT NULL, serviceID INTEGER NOT NULL
);


ALTER TABLE appointment_equipment ADD CONSTRAINT fk_appointmentequip
FOREIGN KEY (appointmentID) REFERENCES appointments(appointmentID);

ALTER TABLE appointment_equipment ADD CONSTRAINT fk_equipment FOREIGN KEY (equipmentID) REFERENCES
equipment(equipmentID);

ALTER TABLE appointment_services ADD CONSTRAINT fk_appointmentserv
FOREIGN KEY (appointmentID) REFERENCES appointments(appointmentID);
 
ALTER TABLE appointment_services ADD CONSTRAINT fk_service FOREIGN KEY (serviceID) REFERENCES
workout_services(serviceID);

ALTER TABLE appointments ADD CONSTRAINT fk_appointmenttrainer FOREIGN KEY (trainerID) REFERENCES trainers(trainerID);

ALTER TABLE appointments ADD CONSTRAINT fk_appointmentuser FOREIGN KEY (userID) REFERENCES users(userID);

ALTER TABLE equipment ADD CONSTRAINT fk_facility FOREIGN KEY (facilityID) REFERENCES
shipping_facilities(facilityID);

Phase VII - Conclusion

Software and Services

The group used Discord for primary communication and file sharing. Work was done on Discord both synchronously and asynchronously. Outlook was used to submit project stages and for secondary communication and file sharing. Google Docs was used to collaborate on text files.

Experience

The Systems Analysis (Entity Relationship Model) phase was probably the most difficult step due to the conceptualization of logistics and functionality of the trainer matching service. At first glance, a service might resemble a delivery business like UberEats or Doordash because of equipment. However, there was the extra factor of the selection of trainer and service. One interesting aspect of the service was the realization that trainers were not normal employees of the company, but would also be users. The best way for our group to meet that challenge was to imagine how such a service would work in web or mobile application form on the consumer side.

We had a more complete idea of how we wanted the final database to look because a great deal of time was spent at the first phase. This made the Logical and Physical Modeling phase much easier. We had simplified our list of entities, attributes, and relationships to the point where most of the relations already satisfied Third Normal Form, or needed a simple relation for Postal Codes, or were intersections.

Overall, the project was a great experience in learning how collaboration works in practice and how databases are used to serve an organization or business. Another difficult aspect of the project was attempting to figure out which business idea we wanted to go forward with and refining that idea. Asking questions about how the business collects revenue and what are the consumers looking for in the service created a better project outcome. This type of exercise is great for entrepreneurial thinking because it is easy to come up with ideas but obstacles come when giving structure to the idea.

If given another chance to do the project, we would have spent more time on the business concept, which would have probably produced a more unique idea. However, Professor Holowczak was quick to suggest a better idea than a simple gym business.
 
Business Solution

Our database allows customers to train at locations of their choosing with trainers and equipment on demand. Hopefully, this business model will allow customers to meet their training needs through ultimate convenience. The biggest challenge to this business overall is the trainer and equipment logistics, which we had determined to be addressed if the trainer uses a vehicle provided by the company to bring the equipment to the appointment. We believe that our database is structured in a way that allows scalability and flexibility to the business if we were to for example: implement brick and mortar training locations, track our vehicles, or hold group sessions.

Final Comments

The biggest contributor to the success of the project was the group members’ mature attitude and commitment to see each phase through to completion. We respected our roles and responsibilities, but also helped each other even in responsibilities that we did not claim. Formal in-person meetings ended but we continued our work asynchronously and made sure to stay on track to meet deadlines.

