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

![](https://github.com/deepthiii33/Elavate_Labs_task-4/blob/main/screenshots/accessing%20via%20localhost.png)

## ✅ Step 3: Block Port 8080 via UFW and Re-Test

###  Command Used:
```bash
sudo ufw deny 8080
```
![](https://github.com/deepthiii33/Elavate_Labs_task-4/blob/main/screenshots/Deny_port_8080.png)

Then tested again: http://<my-kali-ip>:8080

🔍 What Happened:
- Even after blocking port 8080 with UFW, the server was still accessible locally. This shows that UFW doesn’t block traffic on 127.0.0.1 by default (loopback traffic is exempt unless explicitly filtered).

![](https://github.com/deepthiii33/Elavate_Labs_task-4/blob/main/screenshots/accessing%20via%20IP.png)


## ✅ Step 4: Allow a Custom Port and Test with Netcat

### Commands Used:
```bash
sudo ufw allow 4444

# In one terminal:
nc -lvnp 4444

# In another terminal:
nc 127.0.0.1 4444
```

🔍 What Happened:
- After allowing port 4444, I used nc to establish a listener and a client. Messages were successfully sent between the terminals.

![](https://github.com/deepthiii33/Elavate_Labs_task-4/blob/main/screenshots/Allowing%20Port%204444.png)

## ✅ Step 5: Block Telnet Port (23)

###  Command Used:
```bash
sudo ufw deny 23/tcp
```

🔍 What Happened:
- Port 23 is typically used for Telnet, a legacy and insecure remote access protocol. To simulate firewall protection, I blocked this port using UFW.

![](https://github.com/deepthiii33/Elavate_Labs_task-4/blob/main/screenshots/telnet.png)

## ✅ Step 6: Allow SSH Port (22)

### Commands Used:
```bash
sudo ufw allow 22/tcp
```

🔍 What Happened:
- SSH is a secure method to remotely connect to a Linux system. Ensuring port 22 is open allows safe SSH access. This rule is important for real-world scenarios where remote system management is needed.

![](https://github.com/deepthiii33/Elavate_Labs_task-4/blob/main/screenshots/ssh_allowing.png)


## ✅ Conclusion
Through this project, I gained hands-on experience with Linux firewall management using UFW (Uncomplicated Firewall) on Kali Linux. The primary goals were to:
- Understand how UFW filters incoming traffic.
- Practice allowing and denying specific ports such as:
- Allowing SSH (22) for secure access.
- Blocking Telnet (23) due to its insecurity.
- Experiment with custom services using ports like 4444 and 8080.
- Test and observe real-time network communication using tools like:
     - python3 -m http.server for HTTP testing.
     - netcat (nc) for simulating TCP communication.

## Key Points:
- Just because a port is blocked by UFW doesn’t mean it’s blocked on localhost (127.0.0.1) — the firewall doesn’t stop local apps from talking to each other unless configured.
- You can always check the firewall status and clean up your test rules using simple commands.

-------------
