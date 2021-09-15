# Fictional-Database-Design
This database was created for fictional car rental company that wants to shift their database from paper to digital. Relational database methods are used with use of the cardinality principals.  

## The Scenario
“CAR RENTAL - YYC” is a branch of a car rental company in Calgary, Alberta, Canada. The branch is franchised to an owner by a corporate company. The same owner reports to a separate corporate office. “CAR RENTAL - YYC” is identified by their business identification (BID), year the branch was established, number of employees, and it’s location. The branch, “CAR RENTAL - YYC,” owns ten (10) cars which they rent to customers. Vehicles owned by the branch are identified primarily by their VIN (Vehicle Identification Number). The vehicles also have properties such as make, model, type, year. The branch’s ownership of the cars has properties including purchase date and purchase price. The vehicles are rented to customers with properties such as rental price and rental dates.

The owner of “CAR RENTAL - YYC” wants to move from recording their operations on paper to recording digitally. Additionally, the owner would also like to keep track of how much each of their vehicles are used so they can understand the life span of their vehicles and when they need service. For insurance and registration purposes, the owner needs the database to also indicate the company’s ownership of the vehicles including how much and when the company paid for the cars.

## The Design Diagrams
![Diagram 1](/image1/db1.PNG)

![Diagram 2](/image1/db2.PNG)

![Diagram 3](/image1/db3.PNG)

## Use SQL to Create Database
### NOTE:
The following lines of code were used in PostgreSQL. A University of Calgary server was used and was discontinued prior to this repo being built. The results section provides proof of usages and validity of code.

#### Make Branch Table
CREATE TABLE BRANCH(
	BID BIGINT NOT NULL,
	YEAR_EST INT,
	NO_EMPLOYEES INT,
	COUNTRY VARCHAR(15) NOT NULL,
	PROVINCE VARCHAR(3) NOT NULL,
	CITY VARCHAR(15) NOT NULL,
	STREET VARCHAR(15) NOT NULL,
	UNIT_NO INT NOT NULL,
	PRIMARY_PHONE VARCHAR(10) NOT NULL,
	PRIMARY KEY(BID));

#### Make Vehicle Table
CREATE TABLE VEHICLE(
	VIN VARCHAR(17) NOT NULL,
	MAKE VARCHAR(20) NOT NULL,
	MODEL VARCHAR(20) NOT NULL,
	YEAR_BUILT INT NOT NULL,
	V_TYPE VARCHAR(12) NOT NULL,
	COLOUR VARCHAR(12) NOT NULL,
	PURCHASE_DATE DATE NOT NULL,
	PURCHASE_PRICE BIGINT NOT NULL,
	BRANCH BIGINT NOT NULL,
	PRIMARY KEY(VIN),
  FOREIGN KEY (BRANCH) REFERENCES BRANCH(BID));
  
 #### Make Customer Table
 CREATE TABLE CUSTOMER(
	ACCOUNT_NO BIGINT NOT NULL,
	SURNAME VARCHAR(15) NOT NULL,
	PHONE VARCHAR(10) NOT NULL,
	DOB DATE NOT NULL,
	COUNTRY VARCHAR(15) NOT NULL,
	PROVINCE VARCHAR(3),
	CITY VARCHAR(15),
	STREET VARCHAR(15),
	HOUSE_NO INT,
	RENTAL_DATE DATE NOT NULL,
	RENTAL_PRICE INT,
	VEHICLE VARCHAR(17) NOT NULL,
	PRIMARY KEY(ACCOUNT_NO),
	FOREIGN KEY(VEHICLE) REFERENCES VEHICLE(VIN));

#### Create Owners Table
CREATE TABLE OWNERS(
	BLN BIGINT NOT NULL,
	PHONE VARCHAR(10) NOT NULL,
	FRANCHISE_PURCHASE_DATE DATE NOT NULL,
	EMAIL VARCHAR(30),
	BRANCH BIGINT NOT NULL,
	PRIMARY KEY (BLN),
	FOREIGN KEY (BRANCH) REFERENCES BRANCH(BID));

#### Create Individuals Table
CREATE TABLE INDIVIDUAL(
	SURNAME VARCHAR(15) NOT NULL,
	FIRST_NAME VARCHAR(15) NOT NULL,
	DOB DATE NOT NULL,
	OWNERS BIGINT NOT NULL,
	PRIMARY KEY(OWNERS),
	FOREIGN KEY(OWNERS) REFERENCES OWNERS(BLN));

#### Create Group Investor Table
CREATE TABLE GROUP_INVESTOR(
	TRADEMARK VARCHAR(15) NOT NULL,
	COUNTRY VARCHAR(15) NOT NULL,
	PROVINCE VARCHAR(15),
	CITY VARCHAR(15),
	OWNERS BIGINT NOT NULL,
	PRIMARY KEY(OWNERS),
	FOREIGN KEY(OWNERS) REFERENCES OWNERS(BLN));


## Add Data 
### Note:
Data is fictional and entered manually. Preferably a python script would have been used with a csv or txt file. An exampe of this script is in a file of the repo.

INSERT INTO BRANCH
VALUES ('111111111','2016','18','CANADA','AB','EDMONTON','MOOSE RD','1313','4034448274');
INSERT INTO BRANCH
VALUES ('111222333','2017','30','CANADA','BC','VANCOUVER','8TH STREET','4753','6049894616');
INSERT INTO BRANCH
VALUES ('987654321','2011','22','CANADA','AB','CALGARY','CITADEL DRIVE','2121','4038471717');
INSERT INTO BRANCH
VALUES (‘123456789’,’2002’,’32’,’CANADA’,’BC’,’VICTORIA’,’HUNTING RD’,’3333’,’6049994321’);

INSERT INTO OWNERS
VALUES ('100000000','4034436548','2018/09/09','TEST@LIVE.CA','111222333');
INSERT INTO OWNERS
VALUES ('323232323','8002881323','2018/03/09','EMAIL@BING.COM','111111111');
INSERT INTO OWNERS
VALUES ('505050501','6049995432','2019/03/03','RENTTHIS@GMAIL.COM','123456789');
INSERT INTO OWNERS
VALUES ('523432111','5433338282','2019/08/02','EXAMPLE@GMAIL.COM','987654321');

INSERT INTO INDIVIDUAL
VALUES ('BRADY','TOM','1977/08/03','323232323');
INSERT INTO INDIVIDUAL
VALUES ('NEWTON','CAM','1989/05/11','100000000');
INSERT INTO GROUP_INVESTOR
VALUES ('HQD','CANADA','AB','EDMONTON','523432111');
INSERT INTO GROUP_INVESTOR
VALUES ('ATB','CANADA','BC','VICTORIA','505050501');

INSERT INTO VEHICLE
VALUES ('PG4697RR23843Q5FG','FORD','F250','2016','TRUCK','WHITE','2020/01/01','45000','987654321');
INSERT INTO VEHICLE
VALUES ('FE3243EE43285E4RX','FORD','F150','2014','TRUCK','BLACK','2018/02/01','41000','987654321');
INSERT INTO VEHICLE
VALUES ('ZQ3777RE23221E4RW','NISSAN','XTERRA','2016','CAR','BLUE','2017/09/13','21000','987654321');
INSERT INTO VEHICLE
VALUES ('PO5566AB73727V4RV','FORD','FOCUS','2019','CAR','GREEN','2019/09/13','29000','123456789');
INSERT INTO VEHICLE
VALUES ('OE4238PD93929T1MV','KIA','FORTE','2019','CAR','BLACK','2019/04/19','28700','123456789');
INSERT INTO VEHICLE
VALUES ('DD8118TE66349L4ML','TESLA','MODELS','2019','CAR','SILVER','2019/08/08','41250','123456789');
INSERT INTO VEHICLE
VALUES ('RR9258GD87541K4MK','TOYOTA','CAMRY','2015','CAR','WHITE','2016/01/12','21250','111222333');
INSERT INTO VEHICLE
VALUES ('BD3351JH67641R6GK','FORD','F150','2018','TRUCK','BLACK','2018/09/22','40250','111222333');
INSERT INTO VEHICLE
VALUES ('CB7371DF55551A6AV','CHEVROLET','IMPALA','2017','CAR','RED','2017/04/26','32150','111222333');
INSERT INTO VEHICLE
VALUES ('KK8877DD45891F2VA','DODGE','DURANGO','2018','CAR','BLUE','2019/04/20','33250','111111111');
INSERT INTO VEHICLE
VALUES ('MN0517YR65690T2TA','HONDA','FIT','2014','CAR','BLUE','2019/05/25','13250','111111111');
INSERT INTO VEHICLE
VALUES ('NM7882QD78890R5RD','GMC','SIERRA','2020','TRUCK','GREY','2020/06/12','53250','111111111');

INSERT INTO CUSTOMER
VALUES ('202020201','DOUGLAS','4035553667','1984/03/11','CANADA','AB','EDMONTON','9TH STREET','9441','2020/09/25','250','FE3243EE43285E4RX');
INSERT INTO CUSTOMER
VALUES ('414141416','SMITH','4032125555','1994/02/18','CANADA','BC','HOPE','CENTER RD','4322','2020/06/22','390','PO5566AB73727V4RV');
INSERT INTO CUSTOMER
VALUES ('888888111','ROGERS','6048865768','1999/01/26','CANADA','BC','GIBSONS','JOE RD','546','2020/02/16','590','RR9258GD87541K4MK');
INSERT INTO CUSTOMER
VALUES ('772888111','MOORE','4032824749','1971/06/12','CANADA','AB','BASSANO','4TH STREET','9911','2020/08/20','330','NM7882QD78890R5RD');

## Results
### Branch
![alt](/image1/db4.PNG)

### Customer
![alt](/image1/db5.PNG)

### Group Investor
![alt](/image1/db6.PNG)

### Indivdual Owner
![alt](/image1/db7.PNG)

### Owners
![alt](/image1/db8.PNG)

### Vehicles
![alt](/image1/db9.PNG)


## Queries
This car company now has the ability to use their data more effectively!

### Query 1: How many branches are there?
SELECT count(*)AS BID
FROM BRANCH;

![alt](/image1/db10.PNG)

### Query 2: Find the addresses of branches established after 2003
SELECT BID, COUNTRY, PROVINCE, CITY ,STREET,UNIT_NO
FROM BRANCH
WHERE YEAR_EST >'2003';

![alt](/image1/db11.PNG)

### Query 3: Find the total cost of all black vehicles
 SELECT SUM(PURCHASE_PRICE) AS BLACK_CAR_VALUE
 FROM VEHICLE
 WHERE COLOUR='BLACK';

![alt](/image1/db12.PNG)

### Query 4: Find the last name, first name, date of birth of the individual owner who has the email “Test@live.ca”
 SELECT INDIVIDUAL.SURNAME, INDIVIDUAL.FIRST_NAME, INDIVIDUAL.DOB 
 FROM INDIVIDUAL, OWNERS
 WHERE INDIVIDUAL.OWNERS = OWNERS.BLN
 AND OWNERS.EMAIL='TEST@LIVE.CA';

![alt](/image1/db13.PNG)

