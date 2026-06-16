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
STEP 3: Scanning using Nessus

1. We need a platform called Nessus to scan for any vulnerabilities on the system. Use the link	https://www.tenable.com/downloads/nessus?loginAttempted=true to install nessue -> then set everything up.
  after successfully setting everything, this platform is usually hosted at : https://localhost:8834.

2. 



   
