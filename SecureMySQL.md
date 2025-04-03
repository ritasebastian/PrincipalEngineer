

## 🏛️ What is **NIST**?

**NIST** = **National Institute of Standards and Technology**  
It’s a U.S. government agency that sets **security standards** and **guidelines**.

In cybersecurity, NIST provides trusted frameworks like:
- 🔐 **NIST 800-53**: Security & privacy controls
- 🔐 **NIST 800-171**: For protecting **Controlled Unclassified Information (CUI)**

These help you **secure your systems and data** (like MySQL databases) according to best practices.

---

## 🛡️ NIST Security Objectives

NIST frameworks typically focus on:

1. **Access Control**  
2. **Audit & Accountability**  
3. **Encryption (Data at Rest & in Transit)**  
4. **System & Communication Protection**  
5. **Monitoring & Logging**  
6. **Configuration Management**  
7. **Incident Response**

---

## 🧩 Step-by-Step: Apply NIST Guidelines to **MySQL**

Let’s secure a **MySQL server** using NIST-aligned practices.

---

### ✅ **Step 1: Secure Access to MySQL**

- 🔑 Disable root login from remote:
  ```ini
  bind-address = 127.0.0.1
  ```
- 👤 Create dedicated DB users with **least privilege**:
  ```sql
  CREATE USER 'appuser'@'%' IDENTIFIED BY 'StrongPassword!';
  GRANT SELECT, INSERT, UPDATE ON appdb.* TO 'appuser'@'%';
  ```

- 🚫 Disable anonymous users:
  ```sql
  DELETE FROM mysql.user WHERE User='';
  ```

---

### ✅ **Step 2: Enforce Strong Passwords & Policies**

- Use `validate_password` plugin:
  ```sql
  INSTALL PLUGIN validate_password SONAME 'validate_password.so';
  SHOW VARIABLES LIKE 'validate_password%';
  ```

- Enforce:
  - Minimum length (e.g. 12+)
  - Mixed case, numbers, symbols

---

### ✅ **Step 3: Enable SSL/TLS (Encryption in Transit)**

- 🔐 Configure SSL in `my.cnf`:
  ```ini
  [mysqld]
  require_secure_transport = ON
  ssl-ca = /etc/mysql/ssl/ca.pem
  ssl-cert = /etc/mysql/ssl/server-cert.pem
  ssl-key = /etc/mysql/ssl/server-key.pem
  ```

- ✅ Test:
  ```sql
  SHOW STATUS LIKE 'Ssl_cipher';
  ```

---

### ✅ **Step 4: Enable Encryption at Rest**

- Use InnoDB tables with encryption:
  ```sql
  CREATE TABLE secure_table (
      id INT,
      secret_data TEXT
  ) ENCRYPTION='Y';
  ```

- Enable redo log & binary log encryption:
  ```ini
  innodb_redo_log_encrypt = ON
  binlog_encryption = ON
  ```

- Activate keyring plugin:
  ```ini
  early-plugin-load=keyring_file.so
  keyring_file_data=/var/lib/mysql-keyring/keyring
  ```

---

### ✅ **Step 5: Enable Logging & Auditing**

- Turn on general and slow query logs:
  ```ini
  general_log = ON
  slow_query_log = ON
  ```

- Install MySQL Enterprise Audit plugin (or open-source alternatives):
  ```sql
  INSTALL PLUGIN audit_log SONAME 'audit_log.so';
  ```

- Log who did what and when.

---

### ✅ **Step 6: Regular Patching & Hardening**

- 🔁 Keep MySQL up to date.
- Use tools like **Lynis** or **MySQLTuner** for server hardening.
- Limit OS-level access to the `mysql` user.

---

### ✅ **Step 7: Backup and Recovery with Encryption**

- Use encrypted backups:
  - `mysqldump` + GPG
  - `mysqlpump` with compression + GPG
- Store backups in secure, access-controlled storage.

---

## ✅ Summary: What NIST Controls You Applied

| NIST Goal | MySQL Implementation |
|-----------|----------------------|
| **Access Control** | Role-based DB users, disable root remote |
| **Encryption in Transit** | SSL/TLS setup |
| **Encryption at Rest** | InnoDB encryption + keyring |
| **Audit & Logging** | Enable logs, audit plugin |
| **System Security** | Patch regularly, minimal OS access |
| **Data Recovery** | Secure, encrypted backups |
| **Authentication** | Strong password enforcement |

---
