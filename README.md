# SQL-Server-Tutorial-6---How-to-configure-Transactional-Replication-with-sa-user-only-in-SQL-Server
SQL Server Tutorial 6 - How to configure Transactional Replication with sa user only in SQL Server


Steps: ---
1. Open Sql Server Management Studio.
2. Connect SQL Server 1 with credentials.
3. Connect SQL Server 2 with credentials.
4. Start "SQL Server Agent" in both SQL Server

 --Run the below script in Server 1
 CREATE DATABASE PROD1
 GO
 USE PROD1
 GO

 CREATE TABLE TEST
 (
  ID VARCHAR(10) PRIMARY KEY NOT NULL,
  NAME VARCHAR(10)
 )
 GO
 INSERT INTO TEST VALUES ('1','A')
 INSERT INTO TEST VALUES ('2','B')
 INSERT INTO TEST VALUES ('3','C')
 INSERT INTO TEST VALUES ('4','D')
 INSERT INTO TEST VALUES ('5','E')


 # database and table PROD1 has been created and inserted the data into "TEST" table.

 # check the data in TEST table.
 SELECT * FROM TEST

 ##  If previously replication in created then please dissable replication..
 Stop "the SQL Server Agent"
 Refresh the database.


 #Disable Publishing and Distribution...
 Right click on "Replication"
 Click on "Disable Publishing and Distribution..."
 -> Next -> Check "Yes" -> Next -> Next

 # Start "SQL Server Agent" for both the server.

 # Create Replication (First configure Distribution) in Server 1
 Right click on Replication in Server 1
 Configure Distribution -> select first checkbox -> Next -> Next -> Next -> Finish -> Close

 # Check in system Databases... distribution is created.

 # Check in "Security"
 distributed_admin


 # Right click on "Local Publications" -create in Server 1
 New Publication -> Next -> "Select DB" -> Next -> Select "Transactional publication" -> Next -> Click on checkbox (Objects to publish) -> Next -> Next -> Checkbox click on [] Create a snapshot.... -> Next

 we will choose "Transaction Replication" type.

 You ll get the list of the table. But you can select only those tables who contains Primary Key. So for the transaction replication Primary key is necessary.

 Click on "Security Settings" -> Radio Button () Run under the SQL Server Agent service account (This is not a recommended security best practive)

 ** in Connect to the Publisher
 Click on () using the following SQL Server login:
 Login : sa
 Password : *********

 Next -> Click on [] Create the publication -> Next

 Publication name : [PROD1_PUB] "your choice."

 Finish

 # Check in SQL Server Agent list.
 "SQL Server Agent" -> Jobs (Refresh)
 You will get the list of the services.
 "Agent history clean up: distribution"
 "Distribution clean up: distribution"
 "Expired subsscription clean up"
 "Reinitialize subscriptions having data validation fail"
 "Replication agents checkup"
 "Replication monitoring refresher for distribution"
 "syspolicy_purge_history"
 "TOJIB-LAPTOP\SQL2014-PROD1_PUB-1"
 "TOJIB-LAPTOP\SQL2014-PROD1_PUB-PUB_3-1"

 #Now check the publisher is created in Server 1
 We dont have error in Publisher so we can continue with Subscriber.


 # Local Subscriptions - create
 Right Click on "Local Subscriptions" -> "New Subscription" -> Next -> Next -> () Run all agents at the Distributor... -> Next -> Dropdown (Add Subscriber) -> Select "Add SQL Server Subscriber.." Select the Second Server (With Login details) -> In List .. In Second server right side (Subscription Database) Select "<New database>" -> Give (Subscription database name) -> OK -> Next -> In next Wizard Click on [...]

 # Next Popup screen..
 Click on () Run under the SQL Server Agent service account (This is not a recommended security best practice.)

 ** Connect to the Distibutor ----
 () By impresonating the process account

 ** Connect to the Subscriber ---
 (0) Using the following SQL Server login
 Login : sa
 Password : ****
 Confirm password : ****
 OK

 Next -> Next -> Next -> Finish

5. Replication is done successfully.
6. Now i am going to check all the monitoring part.
7. Check how the replication is working if i added one data into server 01 and it ll automatic replicated in server 02. So data will be replicated in server 02 automatic.
8. Now check with replication Monitor.
9. Thanks for watching. My contact details are given below. Feel free to contact.


Video URL : https://chittranjanmahto.blogspot.com/2019/08/sql-server-tutorial-6-how-to-configure.html
