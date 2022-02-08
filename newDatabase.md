use MGFinanceDb
Go
create Table AccountHolderDetails(
ID int identity(1,1),
AdharNumber nvarchar(12) primary key,

);


Go

create Table AdharDetails(
ID int identity(1,1),
AdharNumber nvarchar(12),
PName varchar(20),
PhoneNumber bigint,
PAddress varchar(100),
Email varchar(20),
DOB Date,
AImage Varbinary(Max),
PenCard varchar(20),
FOREIGN KEY (AdharNumber) REFERENCES AccountHolderDetails(AdharNumber)
);

alter table AdharDetails drop column PenCard
Alter table AdharDetails add  PanCard varchar(10)
select * from AdharDetails

Go;




select * from AccountHolderDetails full join AdharDetails On AccountHolderDetails.AdharNumber=AdharDetails.AdharNumber full join BankAccountDetails on AdharDetails.AdharNumber=BankAccountDetails.AdharNumber full join Loan on Loan.AccountNumber=BankAccountDetails.AccountNumber full join EMI on EMI.AccountNumber=BankAccountDetails.AccountNumber

GO;
create Table BankAccountDetails(
AccountNumber nvarchar(14) primary key ,
BankName Varchar(20),
IFSC_Code nvarchar(30),
Branch varchar(20),
AdharNumber nvarchar(12),
DebitedAmount nvarchar(10),
CreditedAmount nvarchar(10),
BankBalance nvarchar(10),
FOREIGN KEY (AdharNumber) REFERENCES AccountHolderDetails(AdharNumber)
);
GO;
select * from BankAccountDetails
GO;
alter table BankAccountDetails drop column Branch 
Go;
alter table BankAccountDetails add  Branch Varchar(100)
Go;

insert into BankAccountDetails values('89000022334488','HDFC_Bank','HDFC1234BTC12','989898989898','0','0','1000000','Malleswaram Bangalore 589909 india')
GO;
insert into AdharDetails values('989898989898','Goutam',9481248848,'BTC Bangalore 581337','Goutam@gmail.com','2021-01-01',Cast('wahid' As varbinary(max)),'xyz12345')
GO;
select * from AccountHolderDetails

Go;
create table Loan(

AccountNumber nvarchar(14) primary key ,
LoanAmount int,
LoanStatus varchar(20),

FOREIGN KEY (AccountNumber) REFERENCES BankAccountDetails(AccountNumber)

)
Go;
insert into Loan values('89000022334488',20000,'approved')
GO;
create table EMI(
AccountNumber nvarchar(14) primary key ,
EMIAmount nvarchar(16),
StartEMIAmount nvarchar(16),
StartEMIDate  Date,
EndEMIAmount nvarchar(16),
EndEMIDate Date,
InterestRate int,
LoanTenure int,


FOREIGN KEY (AccountNumber) REFERENCES BankAccountDetails(AccountNumber)

)
GO;
drop table EMI
GO;
insert into EMI values('89000022334488','100000','1000','2022-01-01','1000','2022-11-01',10,1)
GO;

select * from EMI


/* Stored procedure */
CREATE PROCEDURE ACCOUNT
@AccountNumber nvarchar(14)
AS
BEGIN
SELECT AdharDetails.AdharNumber,BankAccountDetails.AccountNumber,BankAccountDetails.BankBalance,Loan.LoanAmount
FROM AccountHolderDetails full join AdharDetails On AccountHolderDetails.AdharNumber=AdharDetails.AdharNumber full join BankAccountDetails on AdharDetails.AdharNumber=BankAccountDetails.AdharNumber full join Loan on Loan.AccountNumber=BankAccountDetails.AccountNumber full join EMI on EMI.AccountNumber=BankAccountDetails.AccountNumber where BankAccountDetails.AccountNumber=@AccountNumber
END

Execute ACCOUNT '89000022334488'
DROP PROCEDURE ACCOUNT



CREATE PROCEDURE FullACCOUNTDetails
@AccountNumber nvarchar(14)
AS
BEGIN
select AccountHolderDetails.AdharNumber,AdharDetails.PName,AdharDetails.PAddress,AdharDetails.Email,AdharDetails.PhoneNumber,BankAccountDetails.AccountNumber,Loan.LoanAmount,Loan.LoanStatus,EMI.EMIAmount from AccountHolderDetails full join AdharDetails On AccountHolderDetails.AdharNumber=AdharDetails.AdharNumber full join BankAccountDetails on AdharDetails.AdharNumber=BankAccountDetails.AdharNumber full join Loan on Loan.AccountNumber=BankAccountDetails.AccountNumber full join EMI on EMI.AccountNumber=BankAccountDetails.AccountNumber
where BankAccountDetails.AccountNumber=@AccountNumber
END

Execute FullACCOUNTDetails '89000022334488'
DROP PROCEDURE FullACCOUNTDetails


CREATE PROCEDURE EMIDETAILS
@AccountNumber nvarchar(14)
AS
BEGIN
select BankAccountDetails.AccountNumber,EMI.EMIAmount from BankAccountDetails full join EMI on EMI.AccountNumber=BankAccountDetails.AccountNumber
where BankAccountDetails.AccountNumber=@AccountNumber
END

Execute EMIDETAILS '89000022334488'
DROP PROCEDURE EMIDETAILS


create procedure AdharDetailsPro
@AdharNumber nvarchar(12)
AS
BEGIN
Select * from AdharDetails 

END

EXECUTE AdharDetailsPro '989898989898'


create procedure BankAccountDetailsPro
@AccountNumber nvarchar(14)
AS
BEGIN
Select * from BankAccountDetails
END

EXECUTE BankAccountDetailsPro '89000022334488'

Create Procedure LoanPro
@AccountNumber nvarchar(14)
AS 
BEGIN
Select * from Loan
END

EXECUTE LoanPro '89000022334488'

create procedure EMIPro
@AccountNumber nvarchar(14)
AS
BEGIN
Select * from EMI
END

EXECUTE EMIPro '89000022334488'
