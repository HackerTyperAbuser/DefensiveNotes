- [Run Keys](https://pentestlab.blog/2019/10/01/persistence-registry-run-keys/):
    - SOFTWARE hive
        - Microsoft\Windows\CurrentVersion\Run
        - Microsoft\Windows\CurrentVersion\RunServices
    - NTUSER.dat hive
        - SOFTWARE\Microsoft\Windows\CurrentVersion\Run
        - SOFTWARE\Microsoft\Windows\CurrentVersion\RunServices  
              
            Programs that launch automatically each time the user logs in.  
             
- [RunOnce Keys](https://pentestlab.blog/2019/10/01/persistence-registry-run-keys/):
    - SOFTWARE hive
        - Microsoft\Windows\CurrentVersion\RunOnce
        - Microsoft\Windows\CurrentVersion\RunOnceEx\0001
        - Microsoft\Windows\CurrentVersion\RunOnceEx\0001\Depend
        - Microsoft\Windows\CurrentVersion\RunServicesOnce
    - NTUSER.dat hive
        - SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
        - Software\Microsoft\Windows\CurrentVersion\RunServicesOnce  
              
            Unlike the 'Run' key, the 'RunOnce' key is designed to execute an application or script only once, the next time the user logs on to the system. After the application or script has been executed, its entry is removed from the 'RunOnce' key. It's typically used for one-time tasks like software installations, updates, or system configuration changes.  
             
- [Services Keys](https://pentestlab.blog/2019/10/07/persistence-new-service/): 
    - SYSTEM hive
        - CurrentControlSet\Services  
              
            Each subkey under CurrentControlSet\Services represents a service on the system and contains various settings related to that specific component. Windows uses the information stored in these subkeys to initialize and manage the respective services during system startup and throughout the system's operation. Focus your analysis on services with the 'auto start' type set to 'automatic' or 'Automatic (Delayed Start).'  
             
- [Scheduled Tasks Keys](https://pentestlab.blog/2019/11/04/persistence-scheduled-tasks/#:~:text=Windows%20operating%20systems%20provide%20a,teams%20as%20a%20persistence%20mechanism.): 
    - SOFTWARE hive
        - Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\Tasks 
        - Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\Tree  
              
            Tasks that run at a specific time or interval. Attackers can create a malicious scheduled task to maintain persistence.  
             
- [AppInit_DLLs Key](https://pentestlab.blog/2020/01/07/persistence-appinit-dlls/): 
    - SOFTWARE hive
        - Microsoft\Windows NT\CurrentVersion\Windows\AppInit_DLLs  
              
            This key can be used for persistence by loading one or more DLLs (Dynamic Link Libraries) into every process that links with User32.dll. By exploiting this functionality, attackers can maintain a persistent presence on a compromised system, as the malicious DLL will be loaded into processes every time they are started.  
              
            To use the `AppInit_DLLs` key for persistence, an attacker would typically follow these steps:
            1. Create a malicious DLL that performs the desired actions, such as keylogging, data exfiltration, or running a backdoor.
            2. Store the DLL in a location on the compromised system, preferably one that appears legitimate, to avoid detection.
            3. Modify the `AppInit_DLLs` registry key to include the path to the malicious DLL. If existing DLLs are listed, the attacker must append the new path to the list, separated by a comma or space.
            4. Ensure that the `LoadAppInit_DLLs` value in the same registry key is set to 1 (enabled). If it is set to 0 (disabled), the DLLs specified in the `AppInit_DLLs` key will not be loaded.  
                 
- [Winlogon Keys](https://pentestlab.blog/2020/01/14/persistence-winlogon-helper-dll/):
    - SOFTWARE hive
        - Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit
        - Microsoft\Windows NT\CurrentVersion\Winlogon\Shell

		The Userinit process is responsible for user initialization, such as running logon scripts and loading the user profile after a user logs on to the system. Attackers can use this registry key for persistence by appending the path of a malicious executable to the Userinit value, separated by a comma. When a user logs on to the system, the malicious executable will run alongside the default userinit.exe, maintaining continued access.  
  
		The Microsoft\Windows NT\CurrentVersion\Winlogon\Shell registry key in the Windows operating system specifies the shell program run when a user logs in. The shell is the primary interface between the user and the operating system, and by default, the value of this key is explorer.exe, the Windows Explorer shell.  
		An attacker can use this registry key for persistence by modifying the Shell value to include a malicious executable and the default explorer.exe. When a user logs on to the system, the malicious executable will run alongside the default shell, allowing the attacker to maintain a persistent presence on the compromised system.