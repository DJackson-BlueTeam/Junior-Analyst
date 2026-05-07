![[z-ero.png]]

You’re a CRISIS responder deployed to the Zeta-9 Bio-Tech facility. Mission: Use Graylog to analyze the Project-Z edge device and confirm whether a breach has occurred. Uncover how it happened — and why. Good luck, responder. The fate of Zeta-9 and possibly the world may depend on what you find.

Scenario

Deep beneath the city, Zeta-9 Corporation’s secret bioweapon project went catastrophically wrong after an explosion released a mind-altering virus into the wild. The company covered it up as a “minor fire,” but leaked internal files from a mysterious hacktivist group told another story — one of containment failure and stolen research. Now, all contact with the facility is lost. As part of Zeta-9’s elite CRISIS unit, you’re deployed on-site to investigate the breach. The complex is silent — lights flicker, systems are offline, and something feels off. Your first task: access your C.R.I.S.I.S workstation. A briefing document on your desktop may provide more information... For this challenge, a GrayLog server is available at: URL: http://localhost:9000 Credentials: admin / Password A config file was obtained and is available at: /home/ubuntu/Documents/backup/backup.conf WARNING: graylog can take a few minutes to load!

Investigation Questions

What is the vendor of the Project Z firewall? _(2 points)_

Looking through the logs in Ubuntu, I seen a Firewall name "FortiFirewall" and look up the potential "Company". 

![[1..png]]

What is the firmware version is running on the firewall? _(2 points)_

- I grep for version and got results 
![[2..png]]

Answer: 7.0.14
The firewall has an administrative user what is their username? _(2 points)_
- I used `-i` since I was not sure if `user` was capitalized or not. 
![[3..png]]
Answer: admin

Recently, the Project Z network has been unstable. The IT team suspects a possible breach. Can you identify if there is any CVE with a public exploit that could compromise the edge device? _(2 points)_

What is the IP address of the Project Z firewall? _(2 points)_
- This question needed a little OSINT routine. 
![[4..png]]
A threat actor attempted to access the management console. What is the attacker’s IP address? _(2 points)_

- I grep for ssh and notice a ping request was made.
- Usually when a ping request is executed, is comes from the ip address that attempting to connect to another ip.
- In this case it was the adversary making the ping request. 
![[5..png]]
Answer: 38.68.134.215

There have been VPN connection attempts. Which user successfully established a connection? _(3 points)_

- The ip had to be similar to the ip of the ip that attempted the access management console. 
- So I pulled all ip's for the config.file "backup.txt" (I coverted it to readable text by decoding the base64). 
![[6..png]]

Answer: 38.68.134.103 (I put what was in the screenshot, maybe the were a minor malfunction within the investigation environment since it is a RETIRED system.)

A specific user added the successful VPN user, what is the users name? _(3 points)_
- I spent alot of time trying to find the user, but kept running into dead ends, so I went to the interface of graylog and pulled the results.
- Evidently, all of the information that was on the GUI interface was not logged in the backup.conf file. 
![[8..png]]
Answer: zeta_admin

What is the source IP address used during the VPN connection? _(2 points)_
![[8. 1.png]]

Answer: 10.1.1.10

Which internal Zeta-9 IP address was the attacker scanning? _(2 points)_
- grep for ping again and got the results on the zeta9 ip. 
![[9..png]]
Which ports was the attacker mainly interested in discovering on the internal network?
- I had a similar issue with searching through the .conf file that was coverted to .txt for readable purposes and couldn't get the ports I end up discovering through the GUI interface of Graylogs. 
![[10..png]]