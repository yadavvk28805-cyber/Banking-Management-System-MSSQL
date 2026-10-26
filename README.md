# 🏦 Banking Management System (MS SQL Server / T-SQL)

A robust backend database project built using **MS SQL Server (T-SQL)** implementing core banking operations, automated auditing, constraints, error handling, and business logic using advanced database objects.

---

## 🚀 Key Features & Implementation

1. **Relational Schema Design:**
   - **`customers` table:** Stores client details with unique constraints and primary keys.
   - **`accounts` table:** Linked with a Foreign Key to customers, includes `CHECK` constraints for account types (`SAVINGS`, `CURRENT`) and positive balance enforcement.
   - **`transaction_log` table:** Acts as an immutable audit trail using an auto-incrementing `log_id`.

2. **Automated Audit Logging (DML Trigger):**
   - Implemented an `AFTER UPDATE` trigger (`trg_log_transaction`) on the `accounts` table.
   - Automatically calculates the difference and logs whether a transaction was a **DEPOSIT** or **WITHDRAWAL** into the `transaction_log` table.

3. **Secure Fund Withdrawal (Stored Procedure):**
   - Built a robust Stored Procedure (`withdraw_funds`) utilizing **ACID transactions (`BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK`)**.
   - Features explicit locking (`UPDLOCK`) to prevent race conditions during concurrent balance reads.
   - Includes comprehensive `TRY...CATCH` error handling and custom validations for insufficient funds or negative amounts.

4. **Tier Classification System (User-Defined Function):**
   - Created a scalar function (`get_account_status`) to categorize customer accounts into **PLATINUM**, **GOLD**, or **STANDARD** tiers dynamically based on their live balance.

---

## 🛠️ Tech Stack & Concepts Used
- **Database Management System:** Microsoft SQL Server (MS SQL Server)
- **Language:** T-SQL (Transact-SQL)
- **Core Concepts:** 
  - Primary & Foreign Key Relationships
  - DML Triggers (`inserted` & `deleted` virtual tables)
  - Stored Procedures & Exception Handling (`TRY...CATCH`)
  - Explicit Transaction Management (`RAISERROR`, `ROLLBACK`)
  - User-Defined Functions (UDF)

---

## ⚙️ How to Run This Project

1. Open **SQL Server Management Studio (SSMS)** or any compatible MS SQL query editor.
2. Run the script sequentially to:
   - Create and switch to the `BANKING` database.
   - Setup the relational tables (`customers`, `accounts`, `transaction_log`).
   - Compile the Trigger, Stored Procedure, and Function.
3. Execute the demonstration queries included at the bottom of the script to test deposits, withdrawals, audit logs, and account tier classifications.