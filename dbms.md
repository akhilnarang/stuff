# DBMS

## Unit 3
What is 1n form
- Table should have atomic values
    i.e. intersection of row and column should have exactly one values
- Should have primary key

What is 2n form
- 1n and all non key attributes should be fully functionally dependent on key attribute, no partial dependency

What is 3n form
- No transitive dependency

What is a functional dependency (format)
- Based on values, we can decide
  a determines b, a will be a key attribute

Normalization
   - Advantages - Accessibility, Consistency, Integrity, etc. (i.e. attributes of a good relational model)
   - Drawbacks  - There is more decomposition leading to more tables, join and similar queries are tougher



RPT_FORMAT table 

PROJ_NUM PROJ_NAME EMP_NUM EMP_NAME JOB_CLASS CHG_HOUR HOURS

Primary key = PROJ_NUM + EMP_NUM

Functional dependencies - 
    Project name depends on project number
    emp name, job depends on project number and employee number
    CHG_HOUR depends on JOB_CLASS
    ASSIGN_HOURS depends on PROJ_NUM and EMP_NUM

3n form conversion results

Project table - project number and name
Employee table - employee number, name, and class
Charge table - Job class charge
Hours assigned table - Project number, employee number, hours assigned


 ## Unit 4

What is transaction?
Explain ACID properties.
What are different transaction states? Explain with transition diagram.
What is serializability?

A transaction is a unit of program execution that accesses and possibly updates various data items.
To preserve data integrity, a system must ensure:
- Atomicity -> Either all operations are properly reflected in the database or none are
- Consistency -> Execution of a transation in isolation preserves the consistency of the database
- Isolation -> Although multiple transactions may execute concurrently, each must be unaware of other concurrently executing transactions, and results hidden from others.
- Dusrability -> After a transaction completes successfully, 

Transaction State Diagram
```
   _
  | |    |->Partially Committed -----> Committed
  v |   /           |
Active |            |
        \           v
         |->     Failed         -----> Aborted

```
Need for concurrency control
- Lost update problem -> One transaction committing after another and overwriting the data with its own
- Uncommitted dependency problem
- Inconsistent analysis problem


Lab stuff - Triggers

```
create [or replace] trigger trigger_name
[before, after]
[insert, delete, update]
[of column_name]
on table or view EMP_NAME[referencing old as name | new as name]
[for each row]
[when condition]
trigger body;
```

Characteristics of data warehousing :-
- Subject oriented
- Semi structured
- Time variant
- Non volatile
- Integrated

|Data challenges | Process challenges | Management challenges|
-----------------|--------------------|----------------------|
Velocity | Data acquisition and warehousing| Privacy
Variability | Data mining and cleaning | Security
Visualization | Data aggregation and integration | Data governance
Value | Data analysis and modelling | Data and information sharing
