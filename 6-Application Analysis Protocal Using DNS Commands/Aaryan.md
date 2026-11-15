# EXPERIMENT 6 – Analysis of Application Layer Packets (DNS) Using DNS Commands and Wireshark

## AIM
To analyze DNS application-layer packets using DNS commands and Wireshark and understand DNS query-response communication.

---

## PART A: DNS COMMAND-LINE EXECUTION

### Step 1: Open Command Prompt

1. Press `Windows + R`.
2. Type `cmd`.
3. Press Enter.

**Output:** Windows Command Prompt will open.

![Command Prompt](images/step1-cmd.png)

### Step 2: Perform Forward DNS Lookup (A Record)

Execute the following command:

```cmd
nslookup www.example.com
```

**Expected Output (Example):**

```text
Server:  dns-server-name
Address:  10.xx.xx.xx

Non-authoritative answer:
Name:    www.example.com
Address:  93.184.216.34
```

**Observation:**
- Server: DNS server used for the query.
- Address: DNS server IP address.
- Name: Requested domain name.
- Address: IP address resolved for the domain.

**Note:** Actual DNS server and resolved IP addresses may differ.

![Forward DNS Lookup](images/step2-forward-lookup.png)

### Step 3: Perform Reverse DNS Lookup (PTR Record)

Execute:

```cmd
nslookup 104.20.23.154
```

**Possible Output:**

```text
Server:  dns-server-name
Address:  10.xx.xx.xx

Name:    example-hostname
Address:  104.20.23.154
```

If no PTR record exists, output may show:

```text
*** dns-server-name can't find 104.20.23.154:
Non-existent domain
```

**Observation:**
- Reverse lookup attempts to find a domain name associated with an IP address.
- It uses PTR records.
- The result depends on whether a PTR record is configured.

![Reverse DNS Lookup](images/step3-reverse-lookup.png)

### Step 4: Perform MX Record Lookup

Execute:

```cmd
nslookup -type=MX example.com
```

**Expected Output (Example):**

```text
Server:  dns-server-name
Address:  10.xx.xx.xx

Non-authoritative answer:
example.com   MX preference = 0, mail exchanger = .
```

**Observation:**
- MX stands for Mail Exchange.
- It identifies the mail servers responsible for receiving email for a domain.
- Preference values indicate mail-server priority.
- A `.` mail exchanger indicates that the domain does not accept email.

![MX Record Lookup](images/step4-mx-lookup.png)

### Step 5: Perform DNS Lookup Again

Execute:

```cmd
nslookup www.example.com
```

Observe the returned IP addresses.

This command can generate another DNS query for Wireshark packet analysis. Some responses may come from the DNS cache.

---

## PART B: WIRESHARK PACKET ANALYSIS

### Step 6: Open Wireshark

1. Open the Windows Start Menu.
2. Search for Wireshark.
3. Open the application.

![Wireshark Home Screen](images/step6-wireshark-home.png)

### Step 7: Select Network Interface

1. Select **Wi-Fi** if connected through Wi-Fi.
2. Select **Ethernet** if connected through a LAN cable.
3. Select the interface showing network activity.
4. Double-click the interface.

**Output:** Live packet capturing will start.

![Wireshark Interface Selection](images/step7-interface.png)

### Step 8: Generate DNS Traffic

Keep Wireshark capturing in the background.

Open CMD and execute:

```cmd
nslookup www.example.com
```

Then execute:

```cmd
nslookup -type=MX example.com
```

**Output:** DNS queries and responses will be generated.

### Step 9: Apply DNS Display Filter

Return to Wireshark.

Enter the following filter in the Display Filter bar:

```text
dns
```

Press Enter.

**Expected Output:** DNS query and response packets will appear.

![Wireshark DNS Filter](images/step9-dns-filter.png)

### Step 10: Analyze DNS Query Packet

1. Select a DNS query packet.
2. Expand **Domain Name System** in the Packet Details section.
3. Observe the following fields:

- Transaction ID
- Flags
- Queries
- Query Name
- Query Type (A / AAAA / MX / PTR)

**Expected Output:** The DNS query details will be displayed.

![DNS Query Packet Details](images/step10-dns-query.png)

### Step 11: Analyze DNS Response Packet

1. Select the corresponding DNS response packet.
2. Expand **Domain Name System**.
3. Expand the Answers section.
4. Observe the resolved IP address or MX record.

**Expected Output:** DNS response details and available resource records will be displayed.

![DNS Response Packet Details](images/step11-dns-response.png)

### Step 12: Stop Packet Capturing

1. Return to Wireshark.
2. Click the red **Stop** button.
3. Observe the captured DNS packets.

---

## IMPORTANT COMMANDS

| Purpose | Command |
|---|---|
| Forward Lookup | `nslookup www.example.com` |
| Reverse Lookup | `nslookup 104.20.23.154` |
| MX Record Lookup | `nslookup -type=MX example.com` |
| DNS Server Details | `ipconfig /all` |
| Wireshark DNS Filter | `dns` |
| UDP Port 53 Filter | `udp.port == 53` |

---

## OBSERVATIONS

1. **Forward Lookup (A / AAAA Record):** Domain names were queried to obtain their corresponding IPv4 and IPv6 addresses.

2. **Reverse Lookup (PTR Record):** Reverse DNS lookup was performed to find the hostname associated with an IP address. The result depends on PTR record availability.

3. **Mail Exchanger (MX Record):** MX records were queried to examine the mail exchange information of a domain.

4. **Wireshark Packet Analysis:** DNS query and response packets were captured and analyzed using the `dns` display filter. Transaction IDs, query names, record types and answers were observed.

---

## CONCLUSION

Successfully analyzed DNS application-layer packets using command-line utilities and Wireshark. Studied forward lookup, reverse lookup, MX records, DNS queries, responses and the working of DNS communication.

---

## NOTE FOR GITHUB SCREENSHOTS

Create a folder named `images` in the same repository and add your screenshots using these filenames:

- `step1-cmd.png`
- `step2-forward-lookup.png`
- `step3-reverse-lookup.png`
- `step4-mx-lookup.png`
- `step6-wireshark-home.png`
- `step7-interface.png`
- `step9-dns-filter.png`
- `step10-dns-query.png`
- `step11-dns-response.png`

The screenshots will automatically appear in the Markdown file once uploaded.
