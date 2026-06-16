#Mock_Vulnerability_Assessment.

I used Nessus scanner to identify vulnerabilities on my RaspberryPi device and mitigated them.

There are __ steps on this project:
1.
2.
3.
4.
5.

____________________________________________________________________________________________________
STEP 1: Target Device discovery

1. defiing the scope :
   "Scope : Internal devices  Subnet : 10.0.0.0/24 (devices:  RaspberryPi: 10.0.0.140) "

2. Network topology diagram

{insert diagram later on}

____________________________________________________________________________________________________
STEP 2: External assessment and identifying configurations
This phase is about looking at the network from the outside in without actively attacking anything yet.

1. Checking router configurations:
   {insert photos from iphone}

2. Checking is my IP address is flagged for any leaks using Shodan
   {do it and insert any images}

____________________________________________________________________________________________________
STEP 3: Installing Nessus

1. We need a platform called Nessus to scan for any vulnerabilities on the system. Use the link	https://www.tenable.com/downloads/nessus?loginAttempted=true to install nessus
2. Open terminal on the Ubuntu machiene and run ```cd ~/Downloads```
3. Then run ```sudo dpkg -i Nessus-10.X.X-ubuntu1110_amd64.deb``` to unpack the libraries.
4. And then we start Nessus by running the following commands ```sudo systemctl enable nessusd
                                                                 sudo systemctl start nessusd
                                                                 sudo systemctl status nessusd```
   if it's successfully you'll get a green line indicating Active: active (running) in the command output.
5.   Nessus can be accessed at https://localhost:8834.

____________________________________________________________________________________________________
STEP 4: Scanning for vulnerabilities and open ports 

1.  Click on New Scan in the top right corner ->  Select the Basic Network Scan template -> Configure the General Settings (name, IP address) -> Under the Credentials tab, I inputted SSH credentials so Nessus can conduct an internal scan of the device to report vulnerabilities accurately -> SAVE

<img width="1648" height="707" alt="image" src="https://github.com/user-attachments/assets/42862868-4040-49ed-927c-845aa9fb4209" />

2. Launch the scan using the play button wait for a few minutes for the scan to run completely 
3. Vulnerabilities my Raspberry Pi device:
   <img width="1097" height="81" alt="image" src="https://github.com/user-attachments/assets/88b97826-ec88-43c0-8924-1e6fd5bf9dc3" />

   Total vulnerabilities identified:
   Critical: 7
   High:22
   Medium:9
   Low: 2
   Info: 145

4.  I also ran an Nmap scan to identify ports that are opened on the raspberryPI to determine is unsafe ports remain closed.
    <img width="1052" height="247" alt="image" src="https://github.com/user-attachments/assets/163e3632-b99f-418c-88c1-8778d1361b76" />

____________________________________________________________________________________________________
STEP 5: Documenting Vulnerabilities and Identifying top 3

1. <img width="1106" height="146" alt="Nessus_Critical" src="https://github.com/user-attachments/assets/5ff2eba5-a119-43a5-ba9e-f3db8542cca8" />
<img width="1102" height="247" alt="Nessus_med" src="https://github.com/user-attachments/assets/000bd9cb-f11b-4ad7-bcb7-29ffeed3145e" />
<img width="1107" height="157" alt="Nessus_low" src="https://github.com/user-attachments/assets/4c2b3415-b3a4-4b5f-abef-6a856779ec0a" />
<img width="1105" height="150" alt="Nessus_High" src="https://github.com/user-attachments/assets/fa1e1507-2c59-4bb2-aaba-992bb2d5db2b" />

2. | Tool Name | Purpose | Status |
| --- | --- | --- |
| Nmap | Port scanning and network discovery | Completed |
| Nessus | Vulnerability scanning | In Progress |
| Wazuh | SIEM telemetry aggregation | Planned |







   
