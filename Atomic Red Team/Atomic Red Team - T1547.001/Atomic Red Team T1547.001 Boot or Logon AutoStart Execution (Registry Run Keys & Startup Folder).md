12 
- An adversary can achieve persistence by adding a program in the Startup directory or can be reference with a registry run key. 
- Adding a entry point to the "run keys" in the Registry or startup folder can cause the malicious script to be executed when a user login and can have the account associated level of permission.

Events Associated
- Event ID 12: Object Create and Delete
- Event ID 13: Value Set
- Event ID 14: Object Renamed
- Event ID 11: File Created 

Prerequisites Checking
- all prerequisites have been verified. 
 ![[1.1.png]]
Details Breifing
- What to look for. 
![[2.2.png]]

Splunk Table Live View
- In Splunk, I setup the table statistic chart to look for `ParentImages, Image, ParentCommandLine, CommandLine, Users` and excluded any `splunk.exe` or `splunkd.exe` to reduce noise. 
![[Atomic Red Team/Atomic Red Team - T1547.001/Atomic Red Team T1547.001 Img/3.3.png]]

- Right after executing the Persistence Tactic, there was activities generated immediately.
![[5.5.png]]

- There was a `reg.exe` that was created in the `Windows\System32 Directory`.
- This can be verified going to the path in File Explorer
![[Atomic Red Team/Atomic Red Team - T1547.001/Atomic Red Team T1547.001 Img/6.png]]

- Extending the panel, there were Registry's created; an Registry_Path, and Registry_Value with an `iexplorer.exe` executable that was also created when the `reg.exe` was executed. 
![[7.png]]

Procmon
- By filtering for the events that are associated with reg.exe, I was able to find more details on the activity that occurred within the host.

Kernelbase.DLL

![[8.png]]

Observing here, we can see that a KernelBase.dll file was created . 

KernelBase.DDL
- Is the core Windows file that provides the foundational functions for the operating system. 
- the Reg.exe was able to creat this kernelbase.dll to give itself full access to the operating system.

Reparsing Registry Keys

![[Atomic Red Team/Atomic Red Team - T1547.001/Atomic Red Team T1547.001 Img/9.png]]

- When a malware reparse a Registry Open Key, the malware is manipulating Windows so when there are any attempts to open a specific registry key, it is redirected to a different location. 

### Summary

After executing this sample, I was able to understand the steps that a malware will take to maintain persistence in a infected system. using Registry Keys and reparsing Session Managers allow malware to remain within a system even after a power off or restart.