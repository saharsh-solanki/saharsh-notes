Table of contents 
- What is a Transaction? 


- ###### What is a Transaction? 
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
