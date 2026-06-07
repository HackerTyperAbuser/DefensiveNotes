# Event Log
- Tools: Event Log Explorer, Windows Event Log
Windows Event Logs: (`C:\Windows\system32\winevt\logs`)
Default location can be changed by `HKLM\SYSTEM\CurrentControlSet\Services\EventLog\`
- System: Logged by operating sytem
- Application: Logged by third-party applications installed on Windows.
- Security: Events to the system's security, such as account logins, file deletion...
(Get-WinEvent) Return all event logs
```powershell
Get-WinEvent -ListLog * | Select-Object LogName, RecordCount, IsClassicLog, IsEnabled, LogMode, LogType | Format-Table -AutoSize
```

## Types
![[Pasted image 20260510013100.png]]
1. Error: failure of something
2. Warning: not significant, however, may lead to future problems.
3. Information: Describes successful operation of a task.
4. Success Audit: Successful completion of audited security event. User logs onto computer.
5. Failure Audit: failed security events. User login failed
## Event
![[Pasted image 20260510013429.png]]
Event type: https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/
## Parsing Wi-Fi Connections
https://www.nirsoft.net/utils/wifi_history_view.html
Add: `Microsoft-Windows-WLAN-AutoConfig%4Operational.evtx`
![[Pasted image 20260510134554.png]]
## Hunting Events

| EventID | Description                                                                                   |
| :------ | --------------------------------------------------------------------------------------------- |
| 4624    | Successful Logon Event                                                                        |
| 4625    | Failed logon event                                                                            |
| 4634    | Account Logoff, session terminated (RDP closed)                                               |
| 4647    | User initiated logoff. NOT all 4634 is 4647 session can be terminated without logging off.    |
| 4672    | Special privileges assigned to new logon. Admin account logs on                               |
| 4648    | Logon was attempted with explicit credentials. UAC (user have to enter credentials) or Runas. |
| 4720    | Account creation                                                                              |
| 4726    | Account deletion                                                                              |

| EventID | Description                                                               |
| :------ | ------------------------------------------------------------------------- |
| 1       | Process created in memory                                                 |
| 2       | A Process was use to change file creation time (T1070.006 - Timestomping) |
| 3       | Network connection detected                                               |
| 5       | Process Terminated                                                        |
| 11      | File Creation                                                             |
| 12      | Registry event (Object create and delete)                                 |
| 13      | Registry event (Value set)                                                |
| 15      | FileCreateStreamHash (browser file download)                              |
| 22      | DNS Query                                                                 |
| 23      | File Delete                                                               |

