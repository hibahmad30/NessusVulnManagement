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
<img src="https://i.imgur.com/xCn6H4G.png" height="60%" width="60%" alt="Uncredentialed Scan"/> 
<br />
<br />
<img src="https://i.imgur.com/00b4WGs.png" height="60%" width="60%" alt="Uncredentialed Scan"/> 
<h2>Credentialed scan:</h2> 
 <p align="center">
In order to run a credentialed scan, the virtual machine must be configured to accept authenticated scans. The following link provided by Tenable describes how to configure the virtual machine for credentialed scans: https://community.tenable.com/s/article/Scanning-with-non-default-Windows-Administrator-Account?language=en_US. Some of the steps include enabling 'Remote Registry' and ensuring that 'File and Printer Sharing' is turned on in 'Advanced Sharing Settings.'
 <br/>
 <br/>
 <img src="https://i.imgur.com/chTgvEo.png" height="70%" width="70%" alt="Remote Registry"/>
  <br/>
   <br/>
 <img src="https://i.imgur.com/3V8BHiM.png" height="70%" width="70%" alt="File and Printer Sharing"/>
 <br/>
 <br/>
In Nessus, select the previous scan that was created, click 'More,' and then 'Configure.' Navigate to the 'Credentials' tab to the right of 'Settings.' The 'Authentication method' should be set to 'Password.' Enter the username and password of the target Windows 10 virtual machine. After saving these credentials, launch the scan. The image below displays the results of the first credentialed scan:
 <br/>
 <br/>
 <img src="https://i.imgur.com/6OoK2N3.png" height="60%" width="60%" alt="Credentialed Scan Results"/>
  <br/>
 <br/>
 <img src="https://i.imgur.com/AFDXeDE.png" height="60%" width="60%" alt="Credentialed Scan Detailed Results"/>
  <br/>
 <br/>
In the previous uncredentialed scan, the highest severity was 'Medium,' with only 1 vulnerability in this category. In this credentialed scan, there are 7 'Medium' level vulnerabilities, 34 'High,' and 8 'Critical' vulnerabilities. These results further highlight the significance of performing credentialed scans. The two images below are a direct comparison of the results of the uncredentialed scan (left) and the credentialed scan (right). 
 <br/>
 <br/>
 <img src="https://i.imgur.com/25bx2Ph.png" height="30%" width="30%" alt="Uncredentialed Scan Results"/>     <img src="https://i.imgur.com/WjAcm6L.png" height="30%" width="30%" alt="Credentialed Scan Results"/>
  <br/>
 <br/>
For further analysis, I have downloaded a deprecated version of Firefox on the Windows 10 virtual machine. When installing deprecated software, it is vital to ensure that it is done in a sandboxed environment. I then relaunched the scan and got the following results:
 <br/>
 <br/>
 <img src="https://i.imgur.com/nFye7ok.png" height="60%" width="60%" alt="Credentialed Scan Results w/ Firefox"/>
  <br/>
 <br/>
 <img src="https://i.imgur.com/KLqflvy.png" height="50%" width="50%" alt="Credentialed Scan Detailed Results w/ Firefox"/>
  <br/>
 <br/>
Rather than having 7 'Medium' level vulnerabilities as in the first credentialed scan, there are now 23. The 'High' severity vulnerabilities increased from 34 to 108, and the 'Critical' level vulnerabilities increased from 8 to 86. These scan results emphasize the importance of ensuring that all third-party software are fully patched and up-to-date. Depicted below is a comparison of the first credentialed scan (left) to the second credentialed scan with the deprecated version of Firefox installed (right):
 <br/>
 <br/>
 <img src="https://i.imgur.com/WjAcm6L.png" height="30%" width="30%" alt="Credentialed Scan Results"/>     <img src="https://i.imgur.com/FcqpzOC.png" height="30%" width="30%" alt="Credentialed Scan Results w/ Firefox"/>
<h2>Remediation:</h2> 
 <p align="center">
Prior to running a vulnerability scan, it is essential to ensure that both the operating system and all third-party software are fully up-to-date. This will significantly reduce the number of vulnerabilities present in the scan results and will allow the analyst to have more efficient vulnerability management. To further maximize efficiency, be sure to set up automatic updates on your operating system and third-party software.
 <br/>
 <br/>
<img src="https://i.imgur.com/aMYixCT.png" height="60%" width="60%" alt="Uninstall Firefox"/>
<br />
<br />
 <img src="https://i.imgur.com/2aNsH9T.png" height="60%" width="60%" alt="Windows Updates"/>
 <br />
<br />
After uninstalling the deprecated Firefox and running Windows updates, I recieved the following scan result:
<br />
<br />
<img src="https://i.imgur.com/a1LVKQZ.png" height="60%" width="60%" alt="Windows Update Scan"/>
<br />
<br />
 <img src="https://i.imgur.com/XqWuev6.png" height="60%" width="60%" alt="Windows Update Scan"/>
<br />
<br />
I then investigated more specific vulnerabilities for remediation. I found a few more vulnerabilities related to out-of-date software and installed the necessary software updates.
<br />
<br />
<img src="https://i.imgur.com/lj5Xcv0.png" height="70%" width="70%" alt="3D Viewer Vulnerability"/>
<br />
<br />
 <img src="https://i.imgur.com/vY8a8LB.png" height="70%" width="70%" alt="3D Viewer Update"/>
<br />
<br />
<img src="https://i.imgur.com/Nv8j19h.png" height="70%" width="70%" alt="Onedrive Update"/>
<br />
<br />
Missing or misconfigured registry keys can also cause vulnerabilities on a system. When configuring registry keys, it is crucial to ensure that the changes made align with the intended system or application settings and do not introduce unintended consequences or conflicts with existing configurations. To address the WinVerifyTrust Signature Validation Vulnerability (CVE-2013-3900), refer to the following link: https://msrc.microsoft.com/update-guide/vulnerability/CVE-2013-3900.
<br />
<br />
 <img src="https://i.imgur.com/Zrx2GOj.png" height="70%" width="70%" alt="WinVerifyTrust Vulnerability"/>
<br />
<br />
<img src="https://i.imgur.com/0eXXMzV.png" height="70%" width="70%" alt="WinVerifyTrust Remediation"/>
<br />
<br />
I also addressed the 'SMB Signing not required' vulnerability, which has a 'Medium' severity level. This involved navigating to the 'Local Security Policy' and making the necessary configuration changes. The following link provides more information on how to resolve this vulnerability: https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/microsoft-network-server-digitally-sign-communications-always.
<br />
<br />
<img src="https://i.imgur.com/AtNAkOd.png" height="70%" width="70%" alt="SMB Signing Vulnerability"/>
<br />
<br />
 <img src="https://i.imgur.com/lOaujty.png" height="70%" width="70%" alt="SMB Signing Remediation"/>
<br />
<br />
<img src="https://i.imgur.com/3zNJDy1.png" height="70%" width="70%" alt="SMB Signing Remediation"/>
<br />
<br />
After addressing these more specific vulnerabilities on the target system, I launched the final Nessus scan:
<br />
<br />
<img src="https://i.imgur.com/X4tXd1e.png" height="60%" width="60%" alt="Final Scan Results"/>
<br />
<br />
 <img src="https://i.imgur.com/0rygP8U.png" height="60%" width="60%" alt="Final Scan Results"/>
<br />
<br />
Rather than having 5 'Medium' level vulnerabilities as in the previous scan, there are now 0. The 'High' severity vulnerabilities decreased from 16 to 3, and the 'Critical' level vulnerabilities decreased from 2 to 1. Depicted below is a comparison of the previous scan after Firefox was uninstalled and Windows updates were run (left) to the most recent scan where more specific remediations were also made (right):
<br />
<br />
<img src="https://i.imgur.com/cVK2O89.png" height="35%" width="35%" alt="Update Scan Results"/>     <img src="https://i.imgur.com/229wO2C.png" height="35%" width="35%" alt="Remediation Scan Results"/>
<h2>Key takeaways:</h2>
<p align="center">
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
