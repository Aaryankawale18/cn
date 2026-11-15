# EXPERIMENT 7 – Analysis of DNS & HTTP Packets Using Wireshark

## AIM
To analyze Application Layer Packets (DNS & HTTP) using Wireshark and understand their structure and working.

---

## PART A: DNS PACKET ANALYSIS

### Step 1: Open Wireshark
1. Open the Windows Start Menu.
2. Search for **Wireshark**.
3. Open Wireshark.

### Step 2: Select Network Interface
1. If connected through Wi-Fi, select **Wi-Fi**.
2. If connected through LAN cable, select **Ethernet**.
3. Select the interface showing network activity.
4. Double-click the selected interface.

**Output:** Wireshark packet capturing will start, and packets will appear on the screen.

### Step 3: Open Command Prompt
1. Press `Windows + R`.
2. Type `cmd`.
3. Press Enter.

### Step 4: Execute DNS Command

Run the following command:

```cmd
nslookup www.google.com
```

**Expected Output (Example):**

```text
Server:  dns-server-name
Address:  10.xx.xx.xx

Non-authoritative answer:
Name:    www.google.com
Addresses:  142.250.xxx.xxx
            2404:6800:400x:xxxx::xxxx
```

**Output Explanation:**
- Server: DNS server name.
- Address: DNS server IP address.
- Name: Requested domain name.
- Addresses: IP addresses resolved for the domain.

**Note:** DNS server IP and resolved addresses may differ depending on the network.

### Step 5: Apply DNS Filter in Wireshark

1. Return to Wireshark.
2. Click the Display Filter bar at the top.
3. Enter:

```text
dns
```

4. Press Enter.

**Expected Output:** DNS query and DNS response packets will appear.

### Step 6: Analyze DNS Packet Details

1. Select a DNS query packet.
2. Expand **Domain Name System** in the Packet Details section.
3. Observe the following fields:
   - Transaction ID
   - Flags
   - Queries
   - Domain Name
   - Query Type (A / AAAA)

4. Select the corresponding DNS response packet.
5. Expand the Answers section.

**Expected Output:** The response will display the IP addresses associated with the requested domain.

---

## PART B: HTTP PACKET ANALYSIS

### Step 7: Generate HTTP Traffic

1. Open Google Chrome or Microsoft Edge.
2. Enter the following URL in the address bar:

```text
http://neverssl.com
```

3. Press Enter.
4. Wait for the website to load.

**Expected Output:** The website will generate HTTP traffic over TCP port 80.

**Note:** Use HTTP instead of HTTPS because HTTPS traffic is encrypted.

### Step 8: Apply HTTP Filter in Wireshark

1. Return to Wireshark.
2. Click the Display Filter bar.
3. Enter:

```text
http
```

4. Press Enter.

**Expected Output:** HTTP request and response packets will appear.

If no packets appear, use the alternative filter:

```text
tcp.port == 80
```

### Step 9: Analyze HTTP Request

1. Select an HTTP GET packet.
2. Expand **Hypertext Transfer Protocol** in Packet Details.
3. Observe:

| Field | Description |
|---|---|
| Request Method | GET |
| Host | neverssl.com |
| HTTP Version | HTTP/1.1 |
| User-Agent | Browser information |

**Expected Output:** HTTP GET request details will be displayed.

### Step 10: Analyze HTTP Response

1. Select an HTTP response packet.
2. Expand **Hypertext Transfer Protocol**.
3. Observe:

| Field | Description |
|---|---|
| Status Code | 200 OK (if returned) |
| Content-Type | text/html |
| Content-Length | Response size |

**Expected Output:** HTTP response status and header details will be displayed.

---

## PART C: STOP PACKET CAPTURING

### Step 11: Stop Capturing

1. Return to Wireshark.
2. Click the red **Stop** button in the top toolbar.
3. Observe the captured DNS and HTTP packets.

---

## IMPORTANT COMMANDS AND FILTERS

| Purpose | Command / Filter |
|---|---|
| DNS Query | `nslookup www.google.com` |
| DNS Server Details | `ipconfig /all` |
| DNS Packets | `dns` |
| HTTP Packets | `http` |
| HTTP Alternative Filter | `tcp.port == 80` |
| DNS Port Filter | `udp.port == 53` |
| Generate HTTP Traffic | `http://neverssl.com` |

---

## OBSERVATIONS

### DNS
- DNS queries and responses were captured using Wireshark.
- DNS uses UDP port 53 in the usual case.
- The query contains the requested domain name.
- The response contains the resolved IP address.

### HTTP
- HTTP GET requests and responses were captured.
- HTTP commonly uses TCP port 80.
- Request headers contain Host and User-Agent information.
- Response headers contain status code and content information.

---

## CONCLUSION

Successfully captured and analyzed DNS and HTTP packets using Wireshark. Studied DNS query and response structures, HTTP GET requests, response headers, and the working of Application Layer protocols.
