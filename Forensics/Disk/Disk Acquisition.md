# Playbook
Playbook: [[System Extraction]

# Disk Encryption
Check disk encryption (BitLocker, TrueCrypt...)
- Encrypted Drive Detection
```cmd
EDD.exe
```
If encryption exists, disk forensics must be done live, else cut power and extract hard drive.
![[Pasted image 20260510003235.png]]
# Kroll Actifact Parser and Extractor (KAPE)
KAPE for rapid triaging.
## Target Section
Extracting all files from hard-drive takes too long, KAPE is used to extract important and interesting files.
![[Pasted image 20260510004156.png]]
1. Target drive
2. Target destination: directory to save produced image (USB)
3. Flush options
4. Artifact templates
5. Output format
6. Name of output file
7. Deduplication: remove duplications
8. Process files in Windows backup known as Volume Shadow Copies (VSCs)
9. Save output file to remote network location such as SFTP server or an Azure instance.
10. Transfer options: remote network share configuration
11. Command line 

After Extraction:
![[Pasted image 20260510004718.png]]
1. Collected Artifacts
2. CSV log file for collected and Skip artifacts.

## Module Section
Targets and Modules are independent, module section is to quickly parse specific artifact without actually copying the artifact.
![[Pasted image 20260510005201.png]]
1. Source and Destination
2. Modules to execute
3. Output Format
4. Customize modules scripts
5. Command line
6. Execute command
# Windows
FTK Imager, useful for full disk extraction, dead systems and physical disks
# Linux
Linux Disk extraction
```bash
df -h 
sudo dd if=<FILESYSTEM> of=/home/student/Desktop/disk-image.img bs=512
```