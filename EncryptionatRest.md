

## 🔐 What is “Encryption at Rest”?

**Encryption at Rest** means your **data is encrypted while stored** on disk – in files, backups, or logs – so that even if someone steals your hard drive, they **cannot read your data** without the right keys.

> ✅ It protects data **not in use** (just sitting/stored on disk)

---

### 🧠 Real-Life Analogy:

Imagine your **diary**:
- **Without encryption**: Anyone can open and read it.
- **With encryption at rest**: Your diary is locked in a safe with a unique key. Even if someone steals it, they **can’t read it** unless they unlock the safe.

---

## 🗄️ In MySQL: What Gets Encrypted?

When **Encryption at Rest** is enabled in MySQL, these things can be encrypted:

| Component | What It Is | Encryption? |
|----------|------------|-------------|
| Tables | Your actual data (InnoDB tables) | ✅ Yes |
| Logs | Binary logs, redo logs, undo logs | ✅ Yes |
| Temporary Files | Created during query execution | ✅ Yes |
| Backups | Full or partial DB dumps | ✅ Yes (with extra setup) |

---

## ⚙️ How It Works in MySQL (Simplified)

1. **You enable encryption** in MySQL settings (via `my.cnf`)
2. MySQL generates **encryption keys**
3. These keys are managed securely (using **keyring plugin** or external service like AWS KMS)
4. MySQL uses the keys to encrypt/decrypt data automatically during read/write.

> MySQL uses **AES-256** encryption under the hood (very secure).

---

## 📦 Example: Enable Encryption at Rest in MySQL

Let’s walk through a basic setup using **MySQL 8.0** and **InnoDB** tables.

---

### 1️⃣ Enable Keyring Plugin (to store encryption keys)

Edit your MySQL config file (`my.cnf`):

```ini
[mysqld]
early-plugin-load = keyring_file.so
keyring_file_data = /var/lib/mysql-keyring/keyring
```

Restart MySQL:

```bash
sudo systemctl restart mysqld
```

---

### 2️⃣ Create Encrypted Tablespace

```sql
CREATE TABLE secret_data (
    id INT,
    message TEXT
) ENGINE=InnoDB ENCRYPTION='Y';
```

✅ This table is encrypted on disk!

---

### 3️⃣ Enable Default Encryption (Optional)

```sql
SET GLOBAL innodb_encrypt_tables = ON;
SET GLOBAL innodb_encrypt_log = ON;
```

---

## 🔐 How to Verify?

You can check if a table is encrypted:

```sql
SELECT TABLE_SCHEMA, TABLE_NAME, CREATE_OPTIONS
FROM INFORMATION_SCHEMA.TABLES
WHERE CREATE_OPTIONS LIKE '%ENCRYPTION%';
```

---

## 🔐 Where are Encryption Keys Stored?

- If using `keyring_file`, they’re stored securely on disk
- You can also use external key management like:
  - **AWS KMS**
  - **HashiCorp Vault**
  - **Azure Key Vault**

---

## 🧾 Summary for Beginners

| Concept | Explanation |
|--------|-------------|
| **Encryption at Rest** | Encrypts data **on disk** (when not being used) |
| **In MySQL** | Tables, logs, temp files are stored in encrypted form |
| **Why?** | Protects your data even if someone steals the server or disk |
| **Keyring Plugin** | Securely stores encryption keys |
| **Good To Know** | MySQL does encryption/decryption automatically once enabled |

---

## ✅ Why It Matters in Real Life

- GDPR, HIPAA, and other compliance laws **require** it
- Prevents data leakage if physical theft happens
- Easy to implement in MySQL 8+

---
