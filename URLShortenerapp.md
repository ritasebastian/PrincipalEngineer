Great! Here's a **complete step-by-step guide** to deploy a **URL Shortener app** using **Python + Flask + MySQL** with a simple **HTML UI** on your **MacBook**.

---

## 🧰 What You'll Build

- Backend: Python + Flask  
- Database: MySQL (local)  
- Frontend: Basic HTML form  
- Output: Shorten long URLs and redirect using short codes.

---

## ✅ Prerequisites on MacBook

### 1. ✅ Install MySQL
If you haven’t installed MySQL:
```bash
brew install mysql
brew services start mysql
```

Login to MySQL:
```bash
mysql -u root
```

### 2. ✅ Create Database & Table
```sql
CREATE DATABASE url_shortener;
USE url_shortener;

CREATE TABLE urls (
    id INT AUTO_INCREMENT PRIMARY KEY,
    short_code VARCHAR(10) NOT NULL UNIQUE,
    long_url TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Insert sample data:
```sql
INSERT INTO urls (short_code, long_url) VALUES
('abc123', 'https://www.google.com'),
('xyz789', 'https://www.github.com');
```

---

### 3. ✅ Create Python Virtual Environment
```bash
python3 -m venv venv
source venv/bin/activate
```

### 4. ✅ Install Flask + MySQL Connector
```bash
pip install flask mysql-connector-python
```

---

## 🧠 Project Structure

```
url_shortener/
├── app.py
├── templates/
│   └── index.html
```

---

## 🖥️ 5. `app.py` – Flask Application

```python
from flask import Flask, request, redirect, render_template
import mysql.connector
import string, random

app = Flask(__name__)

db = mysql.connector.connect(
    host="localhost",
    user="root",
    password="",  # add password if needed
    database="url_shortener"
)

cursor = db.cursor()

def generate_code(length=6):
    return ''.join(random.choices(string.ascii_letters + string.digits, k=length))

@app.route('/', methods=['GET', 'POST'])
def home():
    if request.method == 'POST':
        long_url = request.form['long_url']
        short_code = generate_code()
        cursor.execute("INSERT INTO urls (short_code, long_url) VALUES (%s, %s)", (short_code, long_url))
        db.commit()
        short_url = request.host_url + short_code
        return render_template('index.html', short_url=short_url)
    return render_template('index.html')

@app.route('/<short_code>')
def redirect_url(short_code):
    cursor.execute("SELECT long_url FROM urls WHERE short_code = %s", (short_code,))
    result = cursor.fetchone()
    if result:
        return redirect(result[0])
    return "URL not found", 404

if __name__ == '__main__':
    app.run(debug=True)
```

---

## 🌐 6. `templates/index.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>URL Shortener</title>
</head>
<body>
    <h1>Simple URL Shortener</h1>
    <form method="POST">
        <input type="text" name="long_url" placeholder="Enter long URL" required>
        <button type="submit">Shorten</button>
    </form>
    {% if short_url %}
        <p>Short URL: <a href="{{ short_url }}" target="_blank">{{ short_url }}</a></p>
    {% endif %}
</body>
</html>
```

---

## ▶️ 7. Run the App

```bash
python app.py
```

Open your browser and go to:  
[http://127.0.0.1:5000](http://127.0.0.1:5000)

---

## 📦 Sample Data You Can Insert into MySQL

```sql
INSERT INTO urls (short_code, long_url) VALUES
('abc001', 'https://openai.com'),
('abc002', 'https://apple.com'),
('abc003', 'https://netflix.com');
```

---

## ✅ Test It

- Enter a long URL in the form.
- You’ll get a shortened version like `http://127.0.0.1:5000/abcXYZ`
- Visit that short URL in your browser → it redirects to the original one.

---

