# Cloud-Databases



This project demonstrates how to **create a MySQL database instance on AWS RDS**, connect to it securely (via EC2 ), and perform basic SQL operations.

---

## 🚀 Steps Performed

### 1️⃣ Create Cloud Database Instance
- Logged in to **AWS Management Console → RDS → Create Database**
- Selected:
  - **Engine:** MySQL
  - **Template:** Free Tier
  - **Master Username:** `admin`
  - **Public Access:** Enabled
- Created the DB instance and waited for it to become **Available**.

 
![RDS Instance Running](./images/Screenshot%202025-10-27%20142346.png)

---

### 2️⃣ Configure Access
- Added an inbound rule in the **RDS security group** to allow port `3306` from my EC2 instance or my IP.
- Verified the **Endpoint** (e.g., `database-1.c3s8aeg2svi6.ap-south-1.rds.amazonaws.com`).



---

### 3️⃣ Connect to the Database
Connected from my EC2 instance using:

- Selected:
  - **Amazon Linux 2** (Free Tier)
  - Instance type: `t2.micro`
  - Key pair for SSH
- Allowed **port 22 (SSH)** in the EC2 security group.
- Connected to EC2 using SSH:

  ssh -i "mykey.pem" ec2-user@<EC2-Public-IP>
 
### Install MariaDB/MySQL Client on EC2

   - Once connected via SSH:

    -sudo yum update -y
    -sudo yum install mariadb -y

✅ Verify installation:

- mysql --version


## 4️⃣ Connect to the RDS Database from EC2

Connected using the MariaDB  installed on EC2:

-  mysql -u admin -p -h database-1.c3s8aeg2svi6.ap-south-1.rds.amazonaws.com

Then entered the master password set during RDS creation.

## 5️⃣ Create Database and Table

Once connected, create a new database and table:

CREATE DATABASE intern_demo;

USE intern_demo;

CREATE TABLE students (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50), domain VARCHAR(30), score INT);




## 6️⃣ Insert and View Data

Insert some sample records and display them:

INSERT INTO students (name, domain, score) VALUES ('Aarav', 'Cloud', 95), ('Diya', 'DevOps', 89);
SELECT * FROM students;

![](./images/Screenshot%202025-10-27%20165144.png)


 ## 🧠 What I Learned

How to set up AWS RDS (MySQL) and configure access using Security Groups

How to connect from EC2 via SSH and use MariaDB client

How to create databases, tables, and insert data using SQL commands

Importance of managing network access and credentials securely

  ## 🧩 Tools & Services Used

AWS EC2

AWS RDS (MySQL)

MariaDB Client

SQL
