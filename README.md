# Reverse-Engineering-APk-file
This Android Malware Analysis using by APK file. In this I perform reverse engineering using of Ghidra and Jadx.

A comprehensive analysis and reverse engineering of an Android APK file suspected of containing malware or security vulnerabilities. The primary goal was to understand the application's security posture and identify any malicious code or security risks.

# Objective

Establish an environment for reverse engineering Android APK files using industry-standard tools.

Thoroughly inspect the APK's source code, resources, and manifest files for suspicious or malicious behavior.

Identify any exposed sensitive information, such as credentials, permissions, or configuration data.

# Tools Used

### JADX	
Open-source decompiler to convert APK bytecode into readable Java source code for inspection.

### Apktool	
Utility used for decoding and rebuilding APK resources and manifest files for deeper analysis.

### Keytool	
A certification reader tool used to read public/private keys and associated certificates.

### Ghidra	
A software reverse engineering (SRE) framework for analyzing compiled code without the original source code.

### Unzip utility	
Employed to decode Android APK resources and disassemble Dalvik bytecode into human-readable smali files for static analysis.

# Methodology
Step 1 : After downloading the APK file,we need decompile it by using APKtool.

       sudo apt install apktool
       apktool d filename.apk

<img width="1580" height="615" alt="apktool" src="https://github.com/CharanCSE02/Reverse-Engineering-APk-file/blob/main/Screenshot%202025-11-25%20123752.png" />

Step 2 : Check sha and md5 values of apk file with apk file permission usage.

         file filename.apk
         md5sum filename.apk
         shasum filename.apk
         aapt dump badging filename.apk | grep "uses-permission"

<img width="1580" height="615" alt="apktool" src="https://github.com/CharanCSE02/Reverse-Engineering-APk-file/blob/main/Screenshot%202025-11-25%20133151.png" />

Step 3 : If we want check more details of apk file without opening means.After completation of decompile few files create in apk file name directory.In that directory we check apktool.yml file is holding information of apk files.

     cat apktool.yml

<img width="1580" height="615" alt="apktool" src="https://github.com/CharanCSE02/Reverse-Engineering-APk-file/blob/main/Screenshot%202025-11-25%20132445.png" />

Step 4 : After gather information of apk file we quickly jump in to certification part like public key/private keys usages.

    sudo apt install keytool
    keytool -printcert -jarfile filename.apk

 <img width="1580" height="615" alt="apktool" src="https://github.com/CharanCSE02/Reverse-Engineering-APk-file/blob/main/Screenshot%202025-11-25%20134110.png" />   

Step 5 : Setting Jadx tool for reverse engineering means loading apk file into it.It providing an interactive platform for exploring the APK’s internal structure, including source code, resources, and manifest files. 

 <img width="1580" height="615" alt="apktool" src="https://github.com/CharanCSE02/Reverse-Engineering-APk-file/blob/main/Screenshot%202025-11-25%20170536.png" /> 
    
Step 6 : Decompiling hidden file in apk file like resource.rsrc etc.We known that after decompilation of apktool,some files not be decompiled by this.For that we are using unzip tool.

    sudo apt install unzip
    unzip -l filename.apk
    unzip filename.apk

<img width="1580" height="615" alt="apktool" src="https://github.com/CharanCSE02/Reverse-Engineering-APk-file/blob/main/Screenshot%202025-11-25%20132307.png" />     

Step 7 : Setting Ghidra tool for reverse engineering means loading apk file into it.It providing an interactive platform for exploring the APK’s internal structure, classes.dev.

<img width="1580" height="615" alt="apktool" src="https://github.com/CharanCSE02/Reverse-Engineering-APk-file/blob/main/Screenshot%202025-11-25%20164924.png" />    

# Key findings

APK signature was intact, confirming no post-signing tampering.

### The application requested unnecessary and high-risk permissions, such as:

Camera access

External storage read/write

### Decompiled code revealed the app:

Accessed internal storage without proper permissions.

Connected to suspicious websites and email addresses.

Potentially transmitted GPS data to an external mail account.

Certain certificates showed security risks or weak configurations.

