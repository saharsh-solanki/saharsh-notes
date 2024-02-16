Table of contents 
- What is a Transaction? 
- ACID principles.


- ### What is a Transaction? 
A Transaction is a collection of queries that is treated as a single unit of work.
The key characteristics of a transaction are often summarized by the acronym ACID, which stands for Atomicity, Consistency, Isolation, and Durability.

**For example**:- 
Let's use a simple example to illustrate a transaction involving account debit and credit. Consider two bank accounts: Account A and Account B.

|AccountName|Balance|
|---|---|
|Account A|$500.00 |
|Account B|$300.00 |
To Debit $100 From Account A and credit to B. This transfer can be represented as a transaction:
1. BEGIN Transaction :

	`SELECT BALANCE FROM ACCOUNTS WHERE AccountName='Account A'`
2. Check if the user has enough money 

	`BALANCE >= 100`
3. If yes 

	`UPDATE Accounts SET balance=balace-100 WHERE AccountName='Account A'`

	`UPDATE Accounts SET balance=balace+100 WHERE AccountName='Account b'`
4. Commit the Transaction  

**Lifespan of the transaction** 
1. Transaction BEGIN 
2. Transaction COMMIT 
3. Transaction ROLLBACK
4. Crash 

**Transaction can be used to modify data**

**Transaction can be used For read-only data**

 - ### ACID:- Atomicity
1. All the queries in the transaction must succeed.
2. If one query fails, All prior successful queries in the transaction should be rollback.
3. If the database went down for some reason all the query should be roll back after database restart.

	atomicity ensures that either the entire set of operations within a transaction is applied, or none of them is. If any part of the transaction fails (due to an error, system crash, or any other reason), the entire transaction is rolled back, and the database remains unchanged.

For Example:- Same Example 

|AccountName|Balance|
|---|---|
|Account A|$500.00 |
|Account B|$300.00 |

To Debit $100 From Account A and credit to B. This transfer can be represented as a transaction:
1. BEGIN Transaction :

	`SELECT BALANCE FROM ACCOUNTS WHERE AccountName='Account A'`
2. Check if the user has enough money 

	`BALANCE >= 100`
3. If yes 

	`UPDATE Accounts SET balance=balace-100 WHERE AccountName='Account A'`

4. After running the above query database went down. Account A has $400 we don't that where the $100 was lost.
    
|AccountName|Balance|
|---|---|
|Account A|$400.00 |
|Account B|$300.00|
* **Lack of atomicity leads to inconsistent data.**

- ### ACID:- Isolation



### Question 

**Ques 1. When having the transaction suddenly the database crashes. Is the Database responsible for rollback and How?**

1. **Transaction Logs:**

    - The DBMS maintains transaction logs, which record the sequence of operations performed during transactions.
    - Before making changes to the actual data, the DBMS writes information about the intended changes to the transaction log.
3. **Write-Ahead Logging (WAL):**
    
    - Many DBMSs use a technique called Write-Ahead Logging (WAL) to ensure that the transaction log records are written to stable storage (disk) before the corresponding data modifications are made.
    - This ensures that, in the event of a crash, the database can recover by replaying the logged transactions.
3. **Recovery Process:**
    
    - When the database restarts after a crash, it goes through a recovery process.
    - During recovery, the DBMS examines the transaction logs to determine the state of each transaction at the time of the crash.
4. **Rollback and Undo Operations:**
    
    - If a transaction was not committed at the time of the crash, the DBMS performs rollback and undo operations to revert the changes made by the incomplete transaction.
    - This ensures that the database is brought back to a consistent state.
5. **Commit or Redo Operations:**
    
    - If a transaction was committed before the crash, the DBMS performs commit or redo operations to reapply the changes made by the committed transactions.

**Ques 2. In a scenario involving a transaction with a SELECT query, is the data modification in the UPDATE query applied immediately?**

- No, the changes made by an UPDATE operation within a transaction are typically made in memory or a temporary space and are not immediately committed to the database.
Ques 3
