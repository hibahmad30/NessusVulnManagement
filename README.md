<h1>Nessus Vulnerability Management and Analysis</h1>

<h2>Description</h2>
Vulnerability management is essential for organizations to identify and mitigate security vulnerabilities in their systems and networks. This project aims to explore the various stages of the vulnerability management lifecycle using Nessus Essentials and an insecure Windows 10 system. Nessus is a powerful tool that provides extensive scanning and remediation capabilities for vulnerability management. The following link provides an overview of the vulnerability management lifecycle: https://www.ibm.com/blog/vulnerability-management-lifecycle/. 
<br />

<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>Oracle VM VirtualBox</b>
- <b>Nessus Essentials Vulnerability Scanner</b>

<h2>Prerequisites:</h2> 

<p align="center">
The Nessus scan will be run on a Windows 10 virtual machine from our host machine. In this analysis the virtual machine will be created using Oracle VirtualBox, however any hypervisor can be used. The download links and instructions are provided as follows:<br /><br />Download Oracle VirtualBox: https://www.virtualbox.org/wiki/Downloads<br />Download Windows 10 Disc Image (ISO File): https://www.microsoft.com/en-us/software-download/windows10<br />Download Nessus Essentials: https://www.tenable.com/products/nessus/nessus-essentials
 <br/>
 <br/>
<img src="https://i.imgur.com/dn9QytA.png" height="35%" width="35%" alt="Install Nessus"/>
<h2>Uncredentialed scan:</h2> 
<p align="center">
Prior to running the first scan, it is important to verify that the host machine can connect to the virtual machine. In the Windows 10 virtual machine, navigate to the command line and use the 'ipconfig' command to gather the IPv4 address of the system. With this IPv4 address, navigate to the command line of the host machine and type in the command 'ping x.x.x.x,' where 'x.x.x.x' is the IPv4 address of the virtual machine. If the host machine is not able to ping the target machine, navigate to the Windows Defender Firewall (wf.msc) and make the appropriate firewall state configuration changes.
<br/>
<br/>
In Nessus, click 'New Scan,' then 'Basic Network Scan,' and provide a name for the scan as well as the virtual machine's IPv4 address in the 'Targets' category. Once the scan is saved, click the 'Launch' icon to begin the scan. The image below depicts the results of the first scan. The vulnerabilities discovered by the scan are primarily in the 'Info' severity, with one being in the 'Medium' severity. To read more about the severity levels assigned by Tenable, refer to the following link: https://docs.tenable.com/nessus/Content/RiskMetrics.htm. Without the use of privileged credentials, the scan is not able to go in-depth and find many vulnerabilities. Therefore, the next step is to perform a credentialed scan. 
<br />
<br />
<img src="https://i.imgur.com/VO6juwB.png" height="55%" width="55%" alt="Uncredentialed Scan"/> 
<h2>Credentialed scan:</h2> 
The next function 'file_check' takes the argument 'fname' again, as well as 'valid_hash' argument, which represents the expected SHA-256 hash value of the file. For example, if I am downloading a software from a vendor that provides the SHA-256 hash of the download file, I would then use the hash value provided by the vendor as the 'valid_hash' value. 
 <br/>
 <br/>
 The variable on line 11, 'file_hash', calls the 'hash_calc' function we defined previously and calculates our file's SHA-256 hash. On line 13, the calculated hash of our file ('file_hash') is then compared to the expected hash value ('valid_hash'), and returns 'True' if they match, and 'False' if they do not.  
 <br/>
 <br/>
<img src="https://i.imgur.com/vCjBM8N.png" height="70%" width="70%" alt="File Integrity Checker"/>
<br />
<br />
The next two lines ask the user for input and assigns the provided input values to the appropriate variables as a string. The variable 'fname' asks for the file name the user would like to check, however if the file is located in a different directory as the python script being run, the user will have to specify the file path rather than just the file name. The variable 'valid_hash' asks the user for the expected hash value and stores the input as a string for validation.  
 <br/>
 <br/>
<img src="https://i.imgur.com/s8bs8Dh.png" height="90%" width="90%" alt="User Input"/>
<br />
<br />
If the user inputs a file name or file path that is not valid, it is important that they are provided with the appropriate error message. The 'try' block calls the 'file_check' function which compares the file hash with the expected hash and returns either a 'True' or 'False' value. This block is the code that will be tested for errors. 
<br />
<br />
 The except block on line 23 allows for error handling of the 'FileNotFoundError' exception, which is a built-in Python exception that is raised when the user attempts to access a file that doesn’t exist. If this error is raised, the user will be informed that the file was not found, and the 'valid_file' value will be set to 'False'. The else block then allows the program to run code when there is no error. 
<br />
<br />
 On line 27, the 'if valid_file' statement will inform the user that their file's integrity is valid. The 'if valid_file' behaves the same as 'if valid_file == True'. On line 29, the 'else' statement will run if 'valid_file' has a 'False' value, and if there was no ‘FileNotFoundError’ present. This statement will be displayed if the hash values do not match, indicating that the file's integrity is not valid. 
 <br/>
 <br/>
 The following link provides more information on the 'FileNotFound' error in Python using try-except blocks: https://www.pylenin.com/blogs/file-not-found-error/. 
 <br/>
 <br/>
<img src="https://i.imgur.com/srCiOgF.png" height="80%" width="80%" alt="Error Handling"/>
<br />

<h2>Program testing:</h2>
<p align="center">
To test the program, I downloaded Mozilla Firefox at https://www.mozilla.org/en-US/firefox/new/. For ease of testing, I renamed the installation file to 'firefox.exe'. I then entered the file name when prompted, as well as the SHA-256 hash of the installation file provided by Mozilla. The program then returned that the file's integrity is valid.
 <br/>
 <br/>
<img src="https://i.imgur.com/zHLbmdC.png" height="90%" width="90%" alt="Valid File and Hash"/>
<br />
<br />
For the second test, I intentionally entered in a random SHA-256 hash that does not match the hash provided by Mozilla. The program then returned that the file's integrity is not valid.  
 <br/>
 <br/>
<img src="https://i.imgur.com/oxN0sN9.png" height="90%" width="90%" alt="Valid File with Invalid Hash"/>
<br />
<br />
For the third test, I entered in the file name as 'firefox.txt' rather than 'firefox.exe', however I entered in the correct hash value. The program then returned that the file 'firefox.txt' was not found.  <br/>
<br/>
<img src="https://i.imgur.com/7IoPt5r.png" height="90%" width="90%" alt="Invalid File with Valid Hash"/>
</p>
<h2>Key takeaways:</h2>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
