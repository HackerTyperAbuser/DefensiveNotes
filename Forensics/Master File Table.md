Database with an entry for every file and folder on the drive, each record includes metadata about the file, such as size, name, access timestamps and file data. Each entry has a maximum size of 1024 bytes.
- Exists on the disks but Windows regularly reads it, the content of MFT may be on the memory at any given time.
![[Pasted image 20260510183325.png]]
\$FILE_NAME (\$FN): name of file or directory with additional metadata like timestamps, allocated size, and parent directory reference.
\$STANDARD_INFORMATION (\$SI): essential metadata about a file or directory: file ownership, permissions and detailed timestamps.
\$DATA: actual content of a file in an NTFS file system.