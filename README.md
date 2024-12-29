# Yara Rules

<h2>Description</h2>
In this Threat Intelligence task, I create yara rules to detect a portable executable that contains a string to a mimikatz url. 

<h2>Languages and Utilities Used</h2>

- <b>YARA</b>
- <b>Linux CLI</b>

<h2>Environments Used </h2>

- <b>Ubuntu</b> 

<br />
<br />
Listing the mimikatz.exe and its strings. 

![1) strings mimikatz](https://github.com/user-attachments/assets/4990c591-27d3-4f72-8576-aac957eb25b8)

<br />
<br />
Within the mimikatz executable, there is a string: $http://blog.gentilkiwi.com/mimikatz 0.

![2) create detection for this string](https://github.com/user-attachments/assets/109c6f72-69b0-41a7-98c5-04c074658e1a)

<br />
<br />  
In my YARA rules folder, I create a mimikatz.yar rule starting with the rule name and meta data. 

![3) meta data for yara rule](https://github.com/user-attachments/assets/49908b63-861a-4bd3-94da-ad00950db708)

<br />
<br />
I run hexdump on the mimikatz.exe.meow to find its hex header. 

![4) hexdump for mimikatz file](https://github.com/user-attachments/assets/34a70f36-4a6c-4adf-94c9-025426435330)

<br />
<br />
Next I write the strings section of the rule to include the http blog string and a portable executable signature to contain MZ in hexadecimal.

![5) yara rule including hex](https://github.com/user-attachments/assets/3ac1ace1-4a6b-46fc-a7e0-ea4d2d8c4a4b)

<br />
<br />
Finally the condition for the rule is that the portable executable signature is at line 0 and the url string is present. 

![6) yara rule condition](https://github.com/user-attachments/assets/a0b2c6d5-c709-4a85-8f7f-4e122ae75627)

<br />
<br />  
I run this yara rule against the sample file with -s to print matching strings.

![7) rule detected strins in mimikatz meow file](https://github.com/user-attachments/assets/c68f007f-da7e-40b8-924f-0c83d2c81989)

<br />
<br />  
The statement import "pe" at the start of a YARA rule enables the use of the PE (Portable Executable) module functionality within the rule. This import allows YARA to analyze the internal structures of Portable Executable files, which are commonly used in Windows environments.
By importing the PE module, YARA rules can:
Access PE-specific attributes and functions
Examine PE file headers, sections, and other structural elements
Check for specific characteristics within the PE file 
    
![8) cp mimikatz2 yar import pe pe is_pe](https://github.com/user-attachments/assets/0a7eac98-a82c-4911-a3d8-b369b3be7bc7)

<br />
<br />
The output of this new rule. 
    
![9) mimikatz2 detection](https://github.com/user-attachments/assets/2be656ed-11a3-43ad-a70d-c3738c9b2718)

<br />
<br />  
