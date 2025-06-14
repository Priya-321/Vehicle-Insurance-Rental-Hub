Day 1: Added finalized DFD, DB schema, ER diagram, and project design

Data Flow Diagram

![Customer (2)](https://github.com/user-attachments/assets/acb5ad33-0071-425e-8264-3bf39a018611)

FINAL DB SCHEMA

Admin
id INT PK
name VARCHAR
email VARCHAR
password VARCHAR

Staff
id INT PK
name VARCHAR
email VARCHAR UNIQUE
phone VARCHAR
address TEXT
role ENUM('rental', 'insurance') -- defines their function

RentalCustomer
id INT PK
name VARCHAR
email VARCHAR UNIQUE
phone VARCHAR
address TEXT
staff_attending INT FK -> Staff(id)

RentalVehicle
id INT PK
model VARCHAR
number_plate VARCHAR UNIQUE
type VARCHAR
status ENUM('available', 'booked')

BookingHistory
id INT PK
vehicle_id INT FK -> RentalVehicle(id)
customer_id INT FK -> RentalCustomer(id)
staff_id INT FK -> Staff(id)
booking_date DATE
expected_return_date DATE
actual_return_date DATE NULLABLE
status ENUM('booked', 'returned')
late_fee DECIMAL(10,2) DEFAULT 0

InsurancePolicy
id INT PK
type VARCHAR
coverage_amount DECIMAL
premium DECIMAL
validity INT -- in months

CustomerInsurance
id INT PK
name VARCHAR
phone VARCHAR
email VARCHAR
address TEXT
policy_id INT FK -> InsurancePolicy(id)
issue_date DATE
expiry_date DATE
claim_status ENUM('active', 'claimed', 'expired')
