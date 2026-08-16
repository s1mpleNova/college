# Cyber Security — Step-by-Step Practical Guide
**Subject Code: BE05016041 | 14 Practicals | Windows (Practicals 1–11) + Kali Linux VM (Practicals 12–14)**

---

## Practical 1: Custom Windows Defender Firewall Rule

**Objective:** Create an inbound rule to block a specific port/app and verify it works.

1. Open **Windows Defender Firewall with Advanced Security** (search it in Start menu).
2. In the left pane, click **Inbound Rules** → in the right pane, click **New Rule...**
3. Select **Port** → Next.
4. Choose **TCP**, and under "Specific local ports" enter `23` (Telnet port) → Next.
5. Select **Block the connection** → Next.
6. Keep all profiles (Domain, Private, Public) checked → Next.
7. Name the rule (e.g. "Block Telnet Port 23") → Finish.
8. **Verify:** Open Command Prompt and run:
   ```
   telnet <your-IP> 23
   ```
   The connection should fail/time out, confirming the rule works.
9. To undo: right-click the rule in Inbound Rules → Disable Rule or Delete.

---

## Practical 2: Firewall Logging & Analysis

**Objective:** Enable Defender Firewall logging and analyze dropped/allowed packets.

1. Open **Windows Defender Firewall with Advanced Security**.
2. Right-click **Windows Defender Firewall with Advanced Security on Local Computer** (top of tree) → **Properties**.
3. Go to the **Domain Profile** tab (repeat for Private/Public as needed) → under **Logging**, click **Customize**.
4. Set **Log dropped packets** to **Yes** and **Log successful connections** to **Yes**.
5. Note the log file path shown (default: `%systemroot%\system32\LogFiles\Firewall\pfirewall.log`).
6. Click OK → OK to apply.
7. Generate some traffic (browse the internet, ping a blocked port from Practical 1).
8. Navigate to `C:\Windows\System32\LogFiles\Firewall\pfirewall.log` and open it with Notepad.
9. Analyze columns: date, time, action (ALLOW/DROP), protocol, source/destination IP, port.

---

## Practical 3: netstat & Task Manager Process Mapping

**Objective:** List open ports/connections and map them to processes.

1. Open Command Prompt (as Administrator for full details).
2. Run:
   ```
   netstat -ano
   ```
3. Observe columns: Proto, Local Address, Foreign Address, State, **PID**.
4. Pick a PID with an active (ESTABLISHED) connection.
5. Open **Task Manager** → **Details** tab.
6. Right-click the column header → **Select columns** → ensure **PID** is checked.
7. Sort by PID and locate the matching process name.
8. Document: which process owns which port/connection, and whether it looks legitimate.

---

## Practical 4: Windows Defender Quick Scan & Protection Settings

**Objective:** Run a scan and explore protection features.

1. Open **Windows Security** (search in Start menu).
2. Go to **Virus & threat protection**.
3. Click **Quick scan** and wait for it to complete.
4. Click **Protection history** to review scan results/detections.
5. Click **Manage settings** under "Virus & threat protection settings".
6. Observe and note the status of: **Real-time protection**, **Cloud-delivered protection**, **Automatic sample submission**, **Tamper Protection**.
7. Toggle Cloud-delivered protection off/on (do not disable Real-time protection) to see the setting change, then restore it.

---

## Practical 5: Password & Lockout Policy

**Objective:** Enforce password complexity and account lockout rules.

1. Open **Local Security Policy** by running `secpol.msc`.
2. Navigate to **Account Policies → Password Policy**.
3. Set/observe:
   - Minimum password length → set to `8`
   - Password must meet complexity requirements → **Enabled**
   - Maximum password age → e.g. `90 days`
4. Navigate to **Account Policies → Account Lockout Policy**.
5. Set:
   - Account lockout threshold → e.g. `3` invalid attempts
   - Account lockout duration → e.g. `15 minutes`
6. **Verify:** Create a test user, deliberately enter a wrong password 3 times, and confirm the account locks out.

---

## Practical 6: Standard User vs Admin — UAC Behavior

**Objective:** Compare UAC prompts between account types.

1. Open **Settings → Accounts → Family & other users → Add account**.
2. Create a new local account and set its account type to **Standard User**.
3. Sign in as the standard user.
4. Try an admin action (e.g. opening Task Manager → "Run as administrator", or installing software).
5. Note the **UAC prompt** asks for an administrator's credentials (Standard user cannot proceed without them).
6. Sign back into your Administrator account and repeat the same action.
7. Note the UAC prompt only asks for **confirmation** (Yes/No), not credentials.
8. Document the difference in the security model.

---

## Practical 7: Auditing Failed Logon Attempts

**Objective:** Use Event Viewer to detect failed logon attempts.

1. Open **Event Viewer** (search in Start menu).
2. Navigate to **Windows Logs → Security**.
3. Deliberately attempt to log in with a wrong password once (lock the screen and try) to generate an event.
4. In Event Viewer, click **Filter Current Log...** on the right pane.
5. Enter Event ID `4625` in the "Includes/Excludes Event IDs" field → OK.
6. Review the filtered results — click an event to see details: account name, source IP/workstation, time, failure reason.
7. Document: how this can help detect brute-force login attempts.

---

## Practical 8: PowerShell Network Connection Monitoring

**Objective:** Identify processes making outbound connections.

1. Open **PowerShell** (as Administrator).
2. Run:
   ```powershell
   Get-NetTCPConnection | Where-Object {$_.State -eq "Established"}
   ```
3. Note the `OwningProcess` column (this is the PID).
4. For a specific PID, run:
   ```powershell
   Get-Process -Id <PID>
   ```
5. Combine both in one command:
   ```powershell
   Get-NetTCPConnection | Where-Object {$_.State -eq "Established"} | 
   Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, OwningProcess, 
   @{Name="ProcessName";Expression={(Get-Process -Id $_.OwningProcess).ProcessName}}
   ```
6. Document any unfamiliar remote IPs/processes and how you'd investigate them further.

---

## Practical 9: File Integrity Hashing

**Objective:** Generate and verify a file hash to simulate tamper detection.

1. Create a simple text file, e.g. `test.txt`, with some content.
2. Open Command Prompt and navigate to the file's folder.
3. Generate its hash:
   ```
   certutil -hashfile test.txt SHA256
   ```
4. Note down the hash value shown.
5. Modify the file's content slightly (add a space or character) and save it.
6. Run the hash command again:
   ```
   certutil -hashfile test.txt SHA256
   ```
7. Compare both hash values — they should be completely different even for a tiny change.
8. Document how this technique can detect unauthorized file tampering.

---

## Practical 10: Disabling a Risky Windows Service

**Objective:** Identify and disable an unnecessary/risky service.

1. Open **Services** by running `services.msc`.
2. Locate **Remote Registry** in the list.
3. Right-click → **Properties**.
4. Note the current **Startup type** (often "Disabled" by default on modern Windows — if so, pick another example service your instructor specifies, or use this to confirm it's already secured).
5. If enabled, set **Startup type** to **Disabled** and click **Stop** if the service is running.
6. Click OK to apply.
7. Document why unused services like Remote Registry increase attack surface if left enabled.

---

## Practical 11: Wi-Fi Profile Security Audit

**Objective:** Review saved Wi-Fi passwords and security type.

1. Open Command Prompt.
2. List all saved Wi-Fi profiles:
   ```
   netsh wlan show profiles
   ```
3. Pick one profile name (SSID) from the list.
4. Run:
   ```
   netsh wlan show profile name="<SSID>" key=clear
   ```
5. Locate the **Security key** field — this reveals the saved plaintext password.
6. Also note the **Authentication** and **Cipher** fields (e.g. WPA2-Personal, AES) to assess the network's security type.
7. Document the risk of saved Wi-Fi credentials being exposed this way if a device is compromised.

---

## Practical 12: Nmap Scanning (Kali VM)

**Objective:** Perform basic network scans to identify open ports.

1. Boot your Kali Linux VM and ensure it can reach your target machine (e.g. host machine or another VM) on the same network.
2. Open a terminal in Kali.
3. Find the target's IP (on the target, run `ipconfig` on Windows or `ip a` on Linux).
4. Run a ping scan to check host availability:
   ```
   nmap -sn <target-IP>
   ```
5. Run a basic TCP SYN scan to find open ports:
   ```
   sudo nmap -sS <target-IP>
   ```
6. Review the output — list of open ports and the services running on them.
7. Try scanning a specific port range:
   ```
   sudo nmap -p 1-1000 <target-IP>
   ```
8. Document which ports were open and what services they typically correspond to.

---

## Practical 13: Wireshark Traffic Capture (Kali VM)

**Objective:** Capture and analyze network traffic between Kali and a target VM.

1. Open **Wireshark** on Kali (search in applications menu, or run `wireshark` in terminal).
2. Select the correct network interface (e.g. `eth0`) and click **Start Capturing**.
3. From a terminal, generate some traffic to the target, e.g.:
   ```
   ping <target-IP>
   ```
   or open a shared file/browse a webpage hosted on the target.
4. Let it capture for 15–30 seconds, then click the red **Stop** button.
5. In the filter bar, type `icmp` (if you used ping) and press Enter to filter just that traffic.
6. Click on a packet and expand the panes below to inspect Ethernet, IP, and ICMP/TCP headers.
7. Document: source/destination IP, protocol, and what the packet contents reveal.

---

## Practical 14: Password Hash Cracking (Kali VM)

**Objective:** Demonstrate weak-password risk using John the Ripper or hashcat.

1. Open a terminal in Kali.
2. Generate an MD5 hash of a sample weak password:
   ```
   echo -n "password123" | md5sum
   ```
3. Save the hash into a file:
   ```
   echo "<hash-value>" > hash.txt
   ```
4. Use a small built-in wordlist (or create one with a few common passwords in `wordlist.txt`, one per line, including "password123").
5. Crack it using John the Ripper:
   ```
   john --format=raw-md5 --wordlist=wordlist.txt hash.txt
   ```
   or using hashcat:
   ```
   hashcat -m 0 -a 0 hash.txt wordlist.txt
   ```
6. Observe the cracked password output.
7. Repeat with a longer, more complex password and note how much longer (or whether) it gets cracked with the same wordlist.
8. Document the conclusion: why password complexity and length matter against dictionary/brute-force attacks.

---

### General Notes
- Practicals 1–11 use tools built into Windows — no installation required.
- Practicals 12–14 require your Kali Linux VM with network connectivity to a target machine (host-only or NAT network mode both work; ensure both VMs can ping each other first).
- Always perform scanning/cracking practicals only on machines/networks you own or have explicit permission to test.
