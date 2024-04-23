## Introduction
This readme provides instructions for configuring Windows Error Reporting to collect crash dump files (.dmp) for troubleshooting software crashes.

## Instructions
1. **Open Registry Editor**: Press `Win + R` and type `regedit`, then press Enter.
   
2. **Navigate to Windows Error Reporting Key**:
   - Go to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting`.

3. **Backup (Optional)**:
   - Right-click the `Windows Error Reporting` key.
   - Select `Export` and save the .reg file in a safe location as a precaution.

4. **Create LocalDumps Key**:
   - If not already present, create a new key named `LocalDumps` inside the `Windows Error Reporting` key.

5. **Configure Registry Values**:
   - Inside the `LocalDumps` key, create the following three registry values:
   
   - **DumpFolder Registry Value**:
     - Right-click in the blank area on the right side.
     - Select `New` > `Expandable String Value`.
     - Name it as `DumpFolder`.
     - Double-click it and enter `%LOCALAPPDATA%\CrashDumps` in the Value data field.

   - **DumpCount Registry Value**:
     - Right-click in the blank area on the right side.
     - Select `New` > `DWORD (32-bit) value`.
     - Name it as `DumpCount`.
     - Double-click it and enter `10` in the Value data field.

   - **DumpType Registry Value**:
     - Right-click in the blank area on the right side.
     - Select `New` > `DWORD (32-bit) value`.
     - Name it as `DumpType`.
     - Double-click it and enter `2` in the Value data field.

6. **Reproduce Software Crash**:
   - Reproduce the crash of the software.

7. **Collect Dump File**:
   - Navigate to `%LOCALAPPDATA%\CrashDumps` to find the related .dmp file with the software name.

## Note
- Make sure to follow these instructions carefully, as modifying the Windows Registry can have unintended consequences if done incorrectly.
- Always back up registry keys before making changes, especially if you're not familiar with the process.

## Disclaimer
- Use this information at your own risk. We are not responsible for any damage caused by improper use of the Registry Editor or misconfiguration of Windows Error Reporting settings.

Reference: https://kb.acronis.com/content/38195?ckattempt=2
Open the Windows registry editor: Hit Win-R and type in regedit
Navigate to following key: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting
(optional) Back up Windows Error Reporting key as a precaution: right-click the Windows Error Reporting key, select Export and save the .reg file in a safe location.
Select the Windows Error Reporting key and create a new key named LocalDumps if it is not there already;
In LocalDumps key, create three registry values as mentioned below:
DumpFolder Registry Value
Right click in the blank area on the right side and select New > Expandable String Value
Name it as DumpFolder
Double click it and enter %LOCALAPPDATA%\CrashDumps in the Value data field
DumpCount Registry Value
Right click in the blank area on the right side and select New > DWORD (32-bit) value
Name it as DumpCount
Double click it and enter 10 in the Value data field
DumpType Registry Value
Right click in the blank area on the right side and select New > DWORD (32-bit) value
Name it as DumpType
Double click it and enter 2 in the Value data field
Reproduce the crash of the software and collect the related .dmp file with the software name

