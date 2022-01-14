select * from UserDetails;
<br>
select * from Loan;
<br>
select * from Bank_Acc;
<br>
select * from PaymentEmis;
<br>

<h2>USER_DETAIL Table</h2>

<br>
Create Table UserDetails(
<br>
User_id int Identity(1,1) Primary key,
<br>
FirstName varchar(30),
<br>
LastName varchar(30),
<br>
Phone bigint,
<br>
Email varchar(20),
<br>
RegDate Date,
<br>
DOB Date,
<br>
Imag Varbinary(Max),
<br>
Aadhar bigint,
<br>
PenCard varchar(20));
<br>


<h2>Loan Table</h2>
Create table Loan(
<br>
LoanId int Identity(1,1) Primary key,
<br>
Loan_Amt_Applied INT,
<br>
Loan_Status varchar(20),
<br>
Loan_Sanctioned int);
<br>


<h2>Bank_Acc Table</h2>
Create table Bank_Acc(
<br>
Payment_id int identity(1,1) primary key,
<br>
Acct_No bigint,
<br>
Bank_Name varchar(20),
<br>
IFSC_Code varchar(20),
<br>
Branch varchar(20));
<br>


<h2>PaymentEmis Table</h2>
Create table PaymentEmis(
<br>
Paymentemi_id int identity(1,1) primary key,
<br>
Amt nvarchar(16),
<br>
StartEMI nvarchar(30),
<br>
LastEMI  nvarchar(20),
<br>
NextEMI nvarchar(20));
<br>
