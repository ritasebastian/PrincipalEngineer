---

## How to design a **URL shortening service** (like Bitly or TinyURL) that can handle **billions of requests per day**.

---

## 🚀 What is a URL Shortener?

A URL shortener converts long URLs into shorter, easy-to-share links.

Example:  
```
Long URL: https://www.amazon.com/electronics/deals/mega-sale-2025  
Short URL: https://sho.rt/abc123
```

When someone clicks the short URL, it redirects to the original long URL.

---

## ✅ Functional Requirements

1. Accept a long URL and return a short one.
2. Redirect short URLs to their original long URLs.
3. (Optional) Track the number of clicks or other analytics.
4. (Optional) Set expiration time for short links.

---

## ⚙️ Non-Functional Requirements

- **High Availability**: Always available and working.
- **Scalability**: Can handle billions of requests daily.
- **Low Latency**: Redirects must be super fast.
- **Consistency**: A short URL should always return the same long URL.

---

## 🧱 High-Level Architecture Components

1. **API Service** – Accepts user requests and returns short URLs.
2. **Database** – Stores short <-> long URL mappings.
3. **Cache** (e.g., Redis) – Speeds up lookups.
4. **Load Balancer** – Distributes requests across servers.
5. **Monitoring** – Tracks performance and errors.

---

## 🔑 How to Generate Short URLs?

### Option 1: Base62 Encoding
- Store a unique ID (e.g., 123456) in the database.
- Convert it to a Base62 string (`abc123`) using 0-9, a-z, A-Z.

This gives billions of combinations in just 6 characters.

### Option 2: Hashing
- Use a hash function (like MD5) on the long URL.
- Take the first 6-8 characters of the hash.
- Handle hash collisions (when two URLs generate the same code).

### Option 3: Random Strings
- Generate a random string and check if it already exists.
- If it exists, retry.

---

## 🗃️ Database Design

You can use SQL (PostgreSQL, MySQL) or NoSQL (Cassandra, DynamoDB).

Example table schema:
```
Table: url_mapping
-----------------------------
short_code | long_url | created_at
abc123     | https://... | 2025-03-29
```

---

## ⚡ Use Caching (Redis)

To make redirects faster:
- First check the cache for the short code.
- If found, redirect immediately.
- If not found, query the database and update the cache.

---

## 🔁 Redirect Flow

1. User visits `sho.rt/abc123`.
2. Server checks Redis cache for `abc123`.
3. If found → redirect to long URL.
4. If not → check DB → cache it → redirect.

---

## 📊 Handling Billions of Requests

To support high scale:
- Deploy multiple API servers (horizontal scaling).
- Use a load balancer (e.g., NGINX, AWS ALB) to distribute traffic.
- Store frequently accessed URLs in Redis cache.
- Use a distributed database or shard the data across many DB instances.

---

## 🔐 Optional Features

- **Analytics**: Track how many people clicked each short link.
- **Rate Limiting**: Prevent spam or abuse.
- **Expiration**: Auto-delete links after a time.
- **Custom short URLs**: Let users choose their code (like `/my-link`).

---

## 🛠️ Example Tech Stack

| Layer         | Technology                 |
|---------------|----------------------------|
| Frontend/API  | Flask, FastAPI, Express.js |
| Cache         | Redis                      |
| Database      | PostgreSQL, DynamoDB       |
| Load Balancer | NGINX, AWS ALB             |
| Hosting       | AWS, GCP, Azure            |
| Monitoring    | Prometheus, Grafana        |

---

## 🧠 Summary

- Use Base62 encoding or random strings to create unique short URLs.
- Store mapping in a database.
- Use Redis to speed up redirects.
- Use load balancers and multiple servers to handle high traffic.
- Add optional features like analytics, expiration, and custom URLs.

---
