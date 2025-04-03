

## 🌳 **AWS Load Balancer Decision Tree**

### 🔽 Start Here:

**Q1:** Are you deploying a **new application** or maintaining a **legacy system**?

- 🟢 **New Application** → Go to Q2  
- 🔴 **Legacy App (built before 2016)** → ✅ Use **Classic Load Balancer (CLB)** *(only if already in use)*

---

**Q2:** Does your application use **HTTP/HTTPS**, and need routing based on **URL paths or hostnames**?

- ✅ **Yes** → ✅ Use **Application Load Balancer (ALB)**  
- ❌ **No, it uses TCP/UDP/TLS** → Go to Q3

---

**Q3:** Does your app need **ultra-low latency**, **static IPs**, or handle **millions of requests/sec**?

- ✅ **Yes** → ✅ Use **Network Load Balancer (NLB)**  
- ❌ **No** → Go to Q4

---

**Q4:** Do you need to inspect, analyze, or **mirror network traffic** for **security or monitoring purposes**?

- ✅ **Yes** → ✅ Use **Gateway Load Balancer (GWLB)**  
- ❌ **No** → ✅ **ALB (default for most apps)** or **NLB** if protocol is not HTTP

---

### 💡 Quick Reference:

| Use Case | Recommended LB |
|----------|----------------|
| Web app / REST API (HTTP/HTTPS) | ✅ ALB |
| Microservices with path-based routing | ✅ ALB |
| gRPC / WebSockets | ✅ ALB |
| TCP/UDP protocol, high performance | ✅ NLB |
| TLS passthrough (end-to-end encryption) | ✅ NLB |
| Packet inspection (firewall, IDS) | ✅ GWLB |
| Legacy app with HTTP/TCP | ✅ CLB |

---

## 🎯 Pro Tips

- Use **ALB** if you need:
  - Routing by URL (e.g., `/api`, `/auth`)
  - Authentication via Cognito
  - WebSocket support

- Use **NLB** if you need:
  - Fixed IP or Elastic IP support
  - TLS passthrough (you don’t want SSL termination at LB)
  - Very high performance or real-time traffic (e.g., game servers)

- Use **GWLB** for:
  - Third-party security appliances (Palo Alto, Fortinet, etc.)

---

