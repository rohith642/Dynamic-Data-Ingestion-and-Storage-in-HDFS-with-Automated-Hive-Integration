✅ Prerequisites
Hadoop and Hive installed and running on your system

You have superuser access or Hadoop CLI access

File: com_data.csv present in your local machine

📁 Step 1: Prepare Your CSV File
Create a CSV file named com_data.csv:

csv
Copy
Edit
emp_id,name,department,salary
101,Alice,Engineering,75000
102,Ramesh,Marketing,60000
103,Charlie,Finance,72000
104,David,Engineering,80000
105,James,Engineering,90000
106,Richard,Marketing,10000
Make sure the file is saved in the directory where you're executing Hadoop commands.

📤 Step 2: Upload File to HDFS
Open terminal and run the following:

bash
Copy
Edit
sudo su

# Create HDFS directory (only once)
hadoop fs -mkdir -p /rohith/cloudera/datapro

# Upload CSV to HDFS
hadoop fs -put -f com_data.csv /rohith/cloudera/datapro/

# Verify upload
hadoop fs -ls /rohith/cloudera/datapro/
Expected output:

swift
Copy
Edit
-rw-r--r--   1 root supergroup ... /rohith/cloudera/datapro/com_data.csv
🐝 Step 3: Create Hive Database and Table
Start Hive shell:

bash
Copy
Edit
hive
Then run the following commands:

sql
Copy
Edit
-- Create and use a database
CREATE DATABASE IF NOT EXISTS rohii;
USE rohii;

-- Create a table
CREATE TABLE IF NOT EXISTS dedata (
    emp_id INT,
    name STRING,
    department STRING,
    salary INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
TBLPROPERTIES ("skip.header.line.count"="1");
🧩 Step 4: Load Data from HDFS to Hive
sql
Copy
Edit
LOAD DATA INPATH '/rohith/cloudera/datapro/com_data.csv' INTO TABLE dedata;
If the above fails, check with:

bash
Copy
Edit
hadoop fs -ls /rohith/cloudera/datapro/
Make sure the file name is exactly com_data.csv.

🔎 Step 5: Query the Table
sql
Copy
Edit
SELECT * FROM dedata;
Expected output:

python-repl
Copy
Edit
101    Alice     Engineering     75000
102    Ramesh    Marketing       60000
...
🧠 Notes
Common Error:

Invalid path → File not uploaded to HDFS properly or wrong filename

Hive is case-sensitive for file paths

If you change the file name, update it everywhere

📂 Project Folder Structure
Copy
Edit
your-folder/
├── com_data.csv
└── README.md
