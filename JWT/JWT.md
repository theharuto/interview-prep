Let’s strip JWT down to the **absolute simplest mental model**, then build just enough depth for interviews.

---

# 🧠 1. What is JWT (in one line)

👉 JWT (JSON Web Token) is a **secure way to prove “who you are” without storing session on the server**

---

# 📦 2. Real-life analogy

Think of JWT like a **movie ticket** 🎟️

* You log in → system gives you a ticket
* You show ticket every time
* Theater (server) doesn’t need to remember you
* It just checks if the ticket is valid

---

# 🔐 3. Structure of JWT

A JWT has 3 parts:

```
HEADER.PAYLOAD.SIGNATURE
```

### Example:

```
eyJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOjEyM30.abc123signature
```

---

### 🧩 Parts explained

### 1. Header

```json
{
  "alg": "HS256"
}
```

👉 Which algorithm used to sign

---

### 2. Payload (VERY IMPORTANT)

```json
{
  "userId": 123,
  "role": "USER"
}
```

👉 Contains:

* user info
* roles
* expiry time (`exp`)

---

### 3. Signature

👉 Created using:

```
header + payload + SECRET_KEY
```

This is what makes JWT **secure**

---

# 🔄 4. How JWT works (step-by-step)

### Step 1: Login

```
POST /login
username + password
```

Server:

* validates user
* creates JWT
* sends it back

---

### Step 2: Client stores token

Usually in:

* localStorage
* memory
* cookie

---

### Step 3: Client sends token every request

```
Authorization: Bearer <JWT>
```

---

### Step 4: Server verifies JWT

* checks signature
* checks expiry
* extracts user info

👉 No DB lookup needed!

---

# 🔥 5. Why JWT is used

| Traditional Session   | JWT               |
| --------------------- | ----------------- |
| Server stores session | No storage needed |
| Stateful              | Stateless         |
| Scaling is hard       | Easy to scale     |

---

# ⚠️ 6. Important concepts (INTERVIEW GOLD)

### ✅ Stateless

Server does NOT remember user

---

### ✅ Signed, not encrypted

👉 Anyone can decode payload
👉 But cannot change it (signature breaks)

---

### ✅ Expiry (`exp`)

JWT must expire → security

---

### ✅ Secret key

If leaked → system compromised

---

# 🚫 7. Common mistakes

### ❌ “JWT is encrypted”

→ No, it’s just encoded + signed

---

### ❌ “JWT is always secure”

→ Only if:

* HTTPS is used
* token is not leaked

---

### ❌ Storing sensitive data in payload

→ Anyone can decode it

---

# 🔁 8. JWT in microservices (VERY IMPORTANT)

In your project:

```
Client → API Gateway → Microservices
```

👉 Flow:

1. User logs in → gets JWT
2. Gateway validates JWT
3. Gateway forwards request to services
4. Services trust the token

---

# 🧠 9. Short interview answer

> “JWT is a stateless authentication mechanism where the server generates a signed token after login. The client sends this token with every request, and the server verifies it using a secret key without storing session data.”

---

# ⚡ 10. When NOT to use JWT

* Need logout immediately
* Need session invalidation
* Highly sensitive systems

---

If you want next:
✅ I can show **how to implement JWT in Spring Boot (10 min setup)**
✅ Or give **top 10 JWT interview questions + answers**
