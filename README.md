# Analyze-FTP-Credentials-with-Wireshark
In this lab I will be using Wireshark to capture and filter out FTP packets, to find out what user(s) have been using the unsecure protocol.
---
# Scenario
I am the security analyst for a small corporate network. I am concerned that several employees may still be using the unsecured FTP protocol against company policy. I have decided to run a test to see if FTP is being used. If any FTP packets are found, I need to determine information about who is using this protocol.
# Step 1: Capture Packets using the enp2s0 interface on Wireshark
1. Open Wireshark
2. Select the enp2s0 interface
3. Click on the blue fin button on the top left to start capturing packets
4. Let it run for a few seconds
5. Press the red square button to stop the capture of packets
<img width="1657" height="426" alt="image" src="https://github.com/user-attachments/assets/27ae3f53-a816-40ea-a91e-71ff45de110d" />

# Step 2: Filter for FTP packets
Enter "FTP" into the display filter field.
<img width="1650" height="467" alt="image" src="https://github.com/user-attachments/assets/f1e07902-a546-433d-8ca1-4c7988cf498a" />

# Step 3: Finding the user
Enter "ftp.request.command==USER" into the display filter field.
<img width="1635" height="492" alt="image" src="https://github.com/user-attachments/assets/cd2a4d6c-a6f9-4cfc-847b-cb0a13e7750a" />
**The Guest account is the user using the unsecure FTP protocol.**

# Step 4: Finding the users password
Enter "ftp.request.command==PASS" into the display filter field.
<img width="1635" height="456" alt="image" src="https://github.com/user-attachments/assets/6218b577-26c7-445a-ad46-bf7b99cb52e6" />
**The users account password was easily captured and found, which is the main reason they shouldn't be using the FTP protocol.**

# Step 5: Finding out what file was retrieved during the FTP session
Enter "ftp.request.command==RETR" into the display filter field.
<img width="1649" height="523" alt="image" src="https://github.com/user-attachments/assets/f1398413-b81c-47ce-ac99-020cbbcf5be5" />
**Not only are you leaving your credentials vulnerable, the contents that you are accessing while using unsecure protocols are also susceptible to interceptions.**

# Final Step: Finding the IP of the computer using FTP
1. Enter "FTP" into the display filter field.
2. Analyze the IPs in the source and destination columns
3. Read the information under the Info column
4. Determine which source IP the request FTP packets are coming from
<img width="1644" height="456" alt="image" src="https://github.com/user-attachments/assets/8067bfa7-583b-46fc-af25-6c3fba3ee4d5" />

**The IP address of the computer using the FTP protocol is 192.168.0.50.**

# Conclusion
**Data Found:**

-User: Guest

-Password: Fr33to@ll

-File downloaded: SalesContacts.txt

-IP address: 192.168.0.50

**This lab demonstrates the risks of using the FTP protocol for file transfers within our company. The FTP protocol lacks encryption which poses significant security threats. FTP transmits data in plaintext leaving it vulnerable to interception. Users need to be using secure alternatives like SFTP or FTPS per our policy to ensure data confidentiality and integrity.**











