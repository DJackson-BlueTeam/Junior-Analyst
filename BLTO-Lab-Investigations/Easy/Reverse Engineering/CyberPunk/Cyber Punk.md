![[CyberPunk.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/74875271f9290902c4858f5ad4db2e936e83e8ef/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/CyberPunk.png)


### Scenario

#### Lady Spark is one of the most infamous edge runners in Noir City. Coming from a generic Blue Team role, to later transition into a nefarious hacker has shocked cybersecurity professionals abroad. Her reasons are unknown, but that is why we are paying you to discover them.  
  
#### Noir City is corrupted, infested with crime, and filled with hackers abroad. I can’t see why our best employee chose the side of evil… Anyway, let’s get to work.  
  
**Note: Run all tools and malware as Administrator**


##### Investigation

1. Looking at the Intezer File Scan Report, what was the Module Path for the malware in question? 
- This requires acessing the documents on the machine.

![[CyberPunk/CyberPunkImg/1..png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/74875271f9290902c4858f5ad4db2e936e83e8ef/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/1..png)

![[CyberPunk/CyberPunkImg/1.1.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/74875271f9290902c4858f5ad4db2e936e83e8ef/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/1.1.png)
	
Answer: `C:\Users\<USER>\AppData\Local\Temp\sparksters_https.exe`
	
2. Analyzing the CodeRed Breach, what were the affected systems?
- This is another document that is on the machine

![[2.0.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/74875271f9290902c4858f5ad4db2e936e83e8ef/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/2.0.png)

Answer: `HR Database, Finance Server`

3. What is the bounty on Lady Spark?

![[2.1.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/0e1a967fd882308af8258cc632d762b72c79a92d/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/2.1.png)

![[CyberPunk/CyberPunkImg/2.2.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/7f816c0b13d22554aeaeacdf69e0192770b0eab7/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/2.2.png)

Answer: £6,650,000
	
4. What are the cryptographic hash sums (MD5 & SHA256) for “SparkIT.exe”? This will help reduce the chance of misidentification with malware.
- I ran a Get-FileHash on the executable.

![[4.1.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/7f816c0b13d22554aeaeacdf69e0192770b0eab7/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/4.1.png)

Answer: `427831FF0D8445F110C8EC555DF70395, 4FC37B100E8DBDEA27042487DD94E37CF6A79F2182884231EB1E6E6C2D4A1955`
  
5. The file name for said malware has been altered. Utilizing VirusTotal, what is the TRUE file name for this malware?
  
![[5..png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/0e1a967fd882308af8258cc632d762b72c79a92d/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/5..png)

Answer: `analytics.exe`

6. After running “string.exe” on the file, there seems to be a malicious URL that Lady Spark uses for traffic. What is said URL, defanged with CyberChef?
- I had to do some research on how to run strings in windows and it resulted in powershell is in the `string.exe` directory and then name the file following the directory of the file path.

![[6.1.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/7f816c0b13d22554aeaeacdf69e0192770b0eab7/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/6.1.png)

![[6.2.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/7f816c0b13d22554aeaeacdf69e0192770b0eab7/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/6.2.png)

![[6.3.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/7f816c0b13d22554aeaeacdf69e0192770b0eab7/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/6.3.png)

Answer: `hxxp[://]www1-google-analytics[.]com:8088/analytics[.]exe`

8. Within the same context of the string.exe output, what command does Lady Spark use to recursively delete files and folders starting at the file system's root?

![[CyberPunk/CyberPunkImg/7.1.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/7f816c0b13d22554aeaeacdf69e0192770b0eab7/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/7.1.png)

- In the screenshot above, you will see a command right below the `C:\Windows\System32\AnalyticsBackup.bat` path 

Answer: `cmd.exe /c rd c:\ /s /q`

8. Run Regshot against the “SparkIT-Installer.exe”. In the “Files Added” section, what was the last file—full path? It seems to be a plain text file with groups of scripts.

- I first ran regshot before the execution of the executable and then after the executable.

![[CyberPunk/CyberPunkImg/8.1.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/7f816c0b13d22554aeaeacdf69e0192770b0eab7/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/8.1.png)

- After having a difficult time looking for the file. I reverted to Procom and filtered for CreateFIle

![[8.2.png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/0e1a967fd882308af8258cc632d762b72c79a92d/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/8.2.png)

9. Looking at the Regshot output, how many keys were added? Hackers can modify this to establish persistence. 
	Answer: 16

10. Lady Spark is trying to cover her track. Using the Regshot output, how many files were deleted?.
	- Answer: 2

11. Let’s use Procmon to examine the processing activity of the malware—unlike Regshot which can’t. Filter the entry for “Process Name” is “SparkIT-Installer”. Turn on “Live Capture” and run the malware via PowerShell. Filter for “Process Create”, what is the full path of the first result?

![[CyberPunk/CyberPunkImg/11..png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/7f816c0b13d22554aeaeacdf69e0192770b0eab7/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/11..png)

Answer: C:\Windows\SysWOW64\cmd.exe

13. Staying within Procmon, utilize the Process Tree, what is the process spawned from this path?
![[CyberPunk/CyberPunkImg/12..png]](https://github.com/DJackson-BlueTeam/90-Day-Junior-Analyst-Sprint/blob/7f816c0b13d22554aeaeacdf69e0192770b0eab7/BLTO-Lab-Investigations/Easy/Reverse%20Engineering/CyberPunk/CyberPunkImg/12..png)

Answer: powershell.exe
