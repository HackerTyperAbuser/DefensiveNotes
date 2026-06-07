NTFS uses \$LogFile to monitor changes to files/folders, unlike $Usnjrnl it stores detailed low-level changes to provide more resilience to the file system. Low level details mean data stores changes for past hours or a day in best cases.
- `C:\$LogFile`
- `[root]\$LogFile`
- Tool: NTFS Log Tracker (can parse \$MFT, \$UsnJrnl and \$LogFile)
![[Pasted image 20260520012943.png]]