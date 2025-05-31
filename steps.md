#  Detailed Firewall Testing Steps (UFW on Kali Linux)

This document outlines the step-by-step process of testing the UFW firewall on Kali Linux. It includes configuration, live testing with HTTP and Netcat, and analysis of behavior based on different rule sets.

---

## ✅ Step 1: Enable UFW and View Current Rules

###  Command Used:
```bash
sudo ufw enable
sudo ufw status 
```

🔍 What Happened:
- UFW was successfully enabled. We reviewed the existing firewall rules to see which ports were already allowed or denied.

 ![](https://github.com/deepthiii33/Elavate_Labs_task-4/blob/main/screenshots/UFW_Status.png)

## ✅ Step 2: Test Open Port (8080) Using Python HTTP Server

### Command Used:
```bash
python3 -m http.server 8080
```
Accessed via browser: ```http://127.0.0.1:8080```

🔍 What Happened:
- The HTTP server successfully ran on port 8080. I was able to access it via browser at 127.0.0.1:8080


## ✅ Step 3: Block Port 8080 via UFW and Re-Test

###  Command Used:
```bash
sudo ufw deny 8080
```
Then tested again: http://<my-kali-ip>:8080

🔍 What Happened:
- Even after blocking port 8080 with UFW, the server was still accessible locally. This shows that UFW doesn’t block traffic on 127.0.0.1 by default (loopback traffic is exempt unless explicitly filtered).

