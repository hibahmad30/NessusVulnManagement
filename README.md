<h1>SHA-256 File Integrity Checker in Python</h1>

<h2>Description</h2>
File integrity checks are essential when downloading files to ensure that data has not been tampered with, and to prevent the execution of malicious payloads. This program automates file integrity checks using the SHA-256 hashing algorithm, a robust algorithm that is resistant to collision attacks. For more information on implementing secure hashing algorithms, please refer to the following link: https://csrc.nist.gov/Projects/Hash-Functions/NIST-Policy-on-Hash-Functions. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>Python</b>
- <b>Hashlib</b>

<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>Visual Studio Code</b>

<h2>Program walk-through:</h2>

<p align="center">
Begin by importing the 'hashlib' module, a widely-recognized Python module used for cryptographic hashing. This module includes a wide range of secure hash and message digest algorithms. The following link contains extensive documentation on the 'hashlib' module: https://docs.python.org/3/library/hashlib.html
 <br/>
 <br/>
<img src="https://i.imgur.com/o3MrBNP.png" height="30%" width="30%" alt="Import Module"/>
<br />
<br />
The first function 'hash_calc' takes the argument 'fname', which represents the name of the file that we will be checking. Next, the file is opened and read in binary mode ('rb'), and stored into the variable 'bytes'. Line 7 follows the 'hashlib' syntax 'hash.hexdigest()', which returns a hash of the file as a string object. As a result, this function calculates and returns the SHA-256 hash of a file, and will be called later in the script.   
<br/>
<br/>
<img src="https://i.imgur.com/yPNYZSX.png" height="65%" width="65%" alt="Hash Calculator"/>
<br />
<br />
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
