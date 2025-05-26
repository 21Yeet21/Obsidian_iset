### Questions

**Question 1:**  
You are a database administrator tasked with setting up a new user named "FinanceManager" with the following requirements:

- The user is authenticated with the password "SecurePwd123".
- Assign the user to the "Finance" tablespace with a quota of 200M.
- Set the temporary tablespace to "TempFinance".
- The password must expire every 60 days, with a 10-day grace period after expiration.
- The user must be able to connect to the database and create tables.
- Grant the user the ability to select and update data in the "Transactions" table owned by the "FinanceDept" user.

Provide the complete SQL commands to accomplish this.

```
CREATE USER FINANCEMANAGER IDENTIFYED BY SecrePwd123
DEFUALT TABLESPACE Finance
QUOTA 200M ON Finance 
TEMPORARY TABPLESPACE TempFinance
;

CREATE PROFILE 
PASSWORD_LIFE_TIME 60
PASSWORD_GRACE_TIME 10;

GRANT CREATE SESSION TO FinanceManager;
GRANT CREATE TABLE TO FinanceManager;
GRANT SELECT ,  UPDATE ON FinanceDept.Transactions TO FinanceManager;
```
---

**Question 2:**  
Explain the difference between system privileges and object privileges in Oracle. Provide one example of each and describe a scenario where you would choose to grant a system privilege instead of an object privilege, and vice versa.

system privilege are connect , create session used on system
object privs are select , alter  ,update used on objects 

when i want a user to connect to the data base i give him sys privs 
and if i want him to create , modify tables i give him object privs

---

**Question 3:**  
Create a role named "Auditor" with the following privileges:

- Select any table in the database.
- Execute any procedure.
- Create and drop users.

Then, assign this role to a user named "AuditUser" and ensure that "AuditUser" can grant this role to other users. Provide all necessary SQL commands to create the role, grant the privileges to the role, assign it to the user, and allow the user to grant the role.

**==SELECT ANY TABLE.**==
==**EXECUTE ANY PROCEDURE==**

```
CREATE ROLE Auditor ;
GRANT SELECT TO Auditor;
GRANT DBA TO Auditor;
GRANT CREATE USER , DROP USER TO Auditor;
```
---

**Question 4:**  
Describe the purpose of profiles in Oracle databases. Then, create a profile named "RestrictedUser" with these settings:
THE PURPOSE IS TO CREATE LIMITATION TO THE USE SO THE DBA ADMIN MANGES HIS PROFILE AND HANDLE HIS SESSION WITH RULES

- Maximum of 3 failed login attempts before the account is locked.
- The account remains locked for 1 day after reaching the failed login attempts limit.
- The password must be changed every 30 days.
- The user is limited to a maximum of 2 concurrent sessions.

Assign this profile to a user named "TempEmployee". Provide the SQL commands to create the profile and assign it to the user.
```
CREATE PROFILE RestrictedUser LIMIT
FAILED_LOGIN_ATEMPTS 3
PASSWORD_LOCK_TIME 1
PASSWORD_LIFE_TIME 30
SESSIONS_PER_USER 2
;

ALTER USER TempEmployee PROFILE RestrictedUser ;
```
==ALTER USER TempEmployee PROFILE RestrictedUser ;==

---

**Question 5:**  
A user named "Developer" has been granted the standard "RESOURCE" role. What privileges does this role typically include? 
CREATING TABLES SEQUENCES VIEWS
If you want to revoke the ability for "Developer" to create sequences without revoking the entire "RESOURCE" role, how would you do it? Provide the necessary SQL command(s).
```
REVOKE CREATE SEQUENCE TO Developer;
```

==Revoking Privilege: REVOKE CREATE SEQUENCE TO Developer; is incorrect because CREATE SEQUENCE is part of the RESOURCE role. You cannot revoke it directly without revoking the role. Instead, you’d revoke RESOURCE and grant individual privileges excluding CREATE SEQUENCE.==

---

**Question 6:**  
Explain the concept of "WITH GRANT OPTION" when granting object privileges in Oracle. Provide an example of its use in an SQL command and discuss one potential risk associated with it.
THE USER CAN GIVE THE PRIV ON THAT OBJECT TO OTHER USERS

FOR EXAMPLE IF WE GRANT TO A  USER THE ABILITY  TO DELETE AN IMPORTANT OBJECT AND HE PASS THAT PRIV TO ANOTHER NORMAL USER OR NEW USER THERE IS A RISK OF LOSING THAT IMPORTANT TABLE IF THE NEW USER DONT KNOW HOW IMPORTANT THAT TABLE IS AND THAT PRIV


---

**Question 7:**  
You need to retrieve information about all users in the database, including their default tablespaces and account lock status. Which data dictionary view should you query, and which specific columns would you select to get this information?
DBA_USERS 
==Correct View: DBA_USERS is sufficient to retrieve usernames, default tablespaces, and account lock status.==

---

**Question 8:**  
Describe the steps to modify the password policy for an existing user who is assigned to a profile named "StandardUser". The new policy requires the password to be changed every 90 days and prevents reuse of any previous password for 180 days. Provide the SQL commands to achieve this.

ALTER PROFILE StandardUser LIMIT 
PASSWORD_LIFE_TIME 90
PASSWORD_REUSE_TIME 180
PASSWORD_REUSE_MAX UNLIMITED

---

**Question 9:**  
What is the difference between dropping a user with the "CASCADE" option versus without it? Provide one scenario where you would use the "CASCADE" option and one where you would not.
WITH CASCADE WILL DROP ALL ROLES AND PRIVS AND OBJECTS ADDED BY THAT USER 
WITHOUT IT WILL ONLY DELETE THE USER IF HE DONT HAVE OBJECT

EXAMPLE IF A MALICIOUS USER HAD ENTERED THE DATABASE SOME HOW 
AND HE DID LOT OF ACTIVITIES WE NEED TO USE CASCADE

IF A NEW USER CREATED BY MISTAKE AND HE DID NOT CREATE AN OBJECT OR ANYTHING WE DONT USE CASCADE



---

**Question 10:**  
Imagine you are managing privileges for a team of 5 developers working on a project. Create a scenario describing their access needs and explain how you would use roles to simplify privilege management for this team. Include at least one SQL command to demonstrate your approach.

I CREATE A ROLE LETTING THOSE DEVS CONSULT AND UPDATE TABLES AND CONNECT TO DB THIS WILL BE EASIER THAN GRANTING TO EACH UUSER ONE BY ONE 

```
CREATE ROLE DEVS;
GRANT SELECT , UPDATE TO DEVS;
, ALTER , DELETE 
GRANT CONNECT TO DEVS;
GRANT DEVS TO dev1;
GRANT DEVS TO dev2;....
```

---

- ==ALTER ANY TABLE, CREATE TABLE, and DELETE ANY TABLE are valid **system privileges**.==
- ==SELECT and UPDATE are **object privileges**, but no specific table is specified (e.g., ON table_name). Without an object, these privileges are invalid in this context.==