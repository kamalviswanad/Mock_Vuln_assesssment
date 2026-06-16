#Mock_Vulnerability_Assessment.

I used Nessus scanner to identify vulnerabilities on my RaspberryPi device and mitigated them.

There are 6 steps on this project:
1. Target Device discovery
2. External assessment and identifying configurations
3. Installing Nessus
4. Scanning for vulnerabilities and open ports 
5. Documenting Vulnerabilities and Identifying top 3
6. Remidiation and Re-scan

____________________________________________________________________________________________________
STEP 1: Target Device discovery

1. defiing the scope :
   "Scope : Internal devices  Subnet : 10.0.0.0/24 (devices:  RaspberryPi: 10.0.0.140) "

____________________________________________________________________________________________________
STEP 2: External assessment and identifying configurations
This phase is about looking at the network from the outside in without actively attacking anything yet.

1. Checking router configurations to ensure they're secure and up to date:
  
<img width="350" height="400" alt="WhatsApp Image 2026-06-16 at 1 52 15 PM" src="https://github.com/user-attachments/assets/d6ee6c44-2fae-4767-a62e-155b9c055887" />
<img width="350" height="400" alt="WhatsApp Image 2026-06-16 at 1 46 06 PM (1)" src="https://github.com/user-attachments/assets/31f59c33-cce0-4697-8ee8-bd12a5a90bf9" />
 <img width="350" height="400" alt="WhatsApp Image 2026-06-16 at 1 46 07 PM" src="https://github.com/user-attachments/assets/2ec7e384-5091-4463-b599-a703180f3617" />
<img width="350" height="400" alt="WhatsApp Image 2026-06-16 at 1 46 06 PM" src="https://github.com/user-attachments/assets/22bcc5b2-fd52-4336-afd9-f3ba29a3307c" />


2. Checking is my IP address is flagged for any leaks using Shodan
   
    <img width="800" height="550" alt="SHODAN" src="https://github.com/user-attachments/assets/a2c52412-d02e-4437-b73a-ebf48765c249" />
    
  As I found no public activity of my IP address, it's determined my IP is not publicly exposed or malicious.


____________________________________________________________________________________________________
STEP 3: Installing Nessus

1. We need a platform called Nessus to scan for any vulnerabilities on the system. Use the link	https://www.tenable.com/downloads/nessus?loginAttempted=true to install nessus
2. Open terminal on the Ubuntu machiene and run ```cd ~/Downloads```
3. Then run ```sudo dpkg -i Nessus-10.X.X-ubuntu1110_amd64.deb``` to unpack the libraries.
4. And then we start Nessus by running the following commands ```sudo systemctl enable nessusd
                                                                 sudo systemctl start nessusd
                                                                 sudo systemctl status nessusd```
   if it's successfully you'll get a green line indicating Active: active (running) in the command output.
5. Nessus can be accessed at https://localhost:8834.

____________________________________________________________________________________________________
STEP 4: Scanning for vulnerabilities and open ports 

1.  Click on New Scan in the top right corner ->  Select the Basic Network Scan template -> Configure the General Settings (name, IP address) -> Under the Credentials tab, I inputted SSH credentials so Nessus can conduct an internal scan of the device to report vulnerabilities accurately -> SAVE

<img width="800" height="350" alt="image" src="https://github.com/user-attachments/assets/42862868-4040-49ed-927c-845aa9fb4209" />

2. Launch the scan using the play button wait for a few minutes for the scan to run completely 
3. Vulnerabilities on my Raspberry Pi device:
   <img width="550" height="40" alt="image" src="https://github.com/user-attachments/assets/88b97826-ec88-43c0-8924-1e6fd5bf9dc3" />

   Total vulnerabilities identified:  <br>
   Critical: 7 <br> 
   High:22   <br>
   Medium:9  <br>
   Low: 2  <br>
   Info: 145

5.  I also ran an Nmap scan to identify ports that are opened on the raspberryPI to determine if unsafe ports remain closed.
    <img width="500" height="122" alt="image" src="https://github.com/user-attachments/assets/163e3632-b99f-418c-88c1-8778d1361b76" />

____________________________________________________________________________________________________
STEP 5: Documenting Vulnerabilities and Identifying top 3

<img width="1106" height="146" alt="Nessus_Critical" src="https://github.com/user-attachments/assets/5ff2eba5-a119-43a5-ba9e-f3db8542cca8" />
<img width="1102" height="247" alt="Nessus_med" src="https://github.com/user-attachments/assets/000bd9cb-f11b-4ad7-bcb7-29ffeed3145e" />
<img width="1107" height="157" alt="Nessus_low" src="https://github.com/user-attachments/assets/4c2b3415-b3a4-4b5f-abef-6a856779ec0a" />
<img width="1105" height="150" alt="Nessus_High" src="https://github.com/user-attachments/assets/fa1e1507-2c59-4bb2-aaba-992bb2d5db2b" />

TOP 3 vulnerabilities to solve: 

1. Risk category: Outdated Core Debian OS System Packages
   Affected software/packages: Imagemagick, libcrypto3-udeb, libnetsnmptrapd40, libnss3
   CVSS Score: 9.8
   Severity: Critical
   Impact: It allows various attacks like local privilege escalation, arbitrary code execution, and cryptographic bypass via outdated core system binaries.
   Remediation: Run ```sudo apt-get update && sudo apt-get upgrade -y``` to install new versions of packages

2. Risk category: Third-Party Applications
   Affected software/packages: Rclone
   CVSS Score: 9.8
   Severity: Critical
   Impact: Command Injection and Authentication Bypass vulnerabilities allow remote threat actors to take full control of the application.
   Remediation: Run ```sudo rclone selfupdate```

3. Risk category: Outdated Development Libraries
   Affected software/packages: libvpx-dev, libpng-dev, libtiff-dev
   CVSS Score: 8.8
   Severity: High
   Impact: Memory corruption or denial of service (DoS) vulnerabilities within background image and video stream compiling dependencies.
   Remediation: Run ```sudo rclone selfupdate```


____________________________________________________________________________________________________
STEP 6: Remidiation and Re-scan

I've applied the relavant remidiation steps as mentioned in the table above and fixed the above 3 issues, and re-scanned the Nessus on Raspberry Pi to verify if the solutions were implemented properly. 

<img width="1107" height="145" alt="image" src="https://github.com/user-attachments/assets/084dc1e2-59eb-451e-92ef-bca26d519432" />

This shows a low number of vulnerabilities 

 Total vulnerabilities identified: <br>
   Critical: 0 <br>
   High:2 <br>
   Medium:4 <br>
   Low: 1 <br>
   Info: 145 <br>

(A few vulnerabilities have'nt been fixed yet)


^_^

   




   
