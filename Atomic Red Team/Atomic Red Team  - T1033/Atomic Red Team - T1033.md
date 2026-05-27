- To further strengthend my understanding of different attack methodologies, I have install the zip file of AtomicRedTeam to test and identify the areas of MITRE ATT&CK ID covers.

The first run I have successfully executed (just to see the execution on my Flare-VM is running) was T1033. 

T1033: System Owner/User Discovery
	Tactic: Discovery
- This is when a adversary will attempt to Identify the primary user, logged in user, set of users that uses a system or a user that is actively using the system. 

Identifying the Prerequisites of the tested executable. 

![[Atomic Red Team/Atomic Red Team  - T1033/Atomic Red Team  - T1033 Img/1.png]]

- After checking the requirements, it sshows that all requirements are met.
- Since this is a simple "whoami" execution, the test executable only needs the powershell command line to run the script. 

- Below shows the details of the tested executable. 
![[Atomic Red Team/Atomic Red Team  - T1033/Atomic Red Team  - T1033 Img/2.png]]

- Now I run the executable. 
![[Atomic Red Team/Atomic Red Team  - T1033/Atomic Red Team  - T1033 Img/3.png]]

- Lets verify the executable on my Splunk Instance. 
- ![[Atomic Red Team/Atomic Red Team  - T1033/Atomic Red Team  - T1033 Img/4.png]]
- ![[Atomic Red Team/Atomic Red Team  - T1033/Atomic Red Team  - T1033 Img/5.png]]
- This shows that the execution was successful. 
- I identified that a commandline was executed `cmd.exe /C whoami` 
- The path that the commandline was executed in was `C:\Windows\System32\WindowPowerShell\v1.0\powershell.exe`
- Now that I identified the whoami command, My Flare-VM will need to be wipe from the execution before proceeding on to another MITRE ATT&CK ID test run . 

- ![[Atomic Red Team/Atomic Red Team  - T1033/Atomic Red Team  - T1033 Img/6.png]]

- Now my Flare-VM is ready for another test. 

### Summary: T1033: Self-Discovery
- MITRE ATT&CK T1033 is a discovery tactic that adversary will use to identify who they are within a system to determine if they are a user, guest user, administrative user, root user, etc. 
- This allows them to know their pivot before moving to the next objective. 
