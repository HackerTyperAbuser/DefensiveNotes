# Playbook
Update Sequence Number Journal provides high-level monitoring of file and folder changes, such as creation, deletion and renaming. \$UsnJrnl file is located:
- `[root]\$Extend\$UsnJrnl`
- This file does not hold data, instead it contains two other data streams `$J` (where the most important data reside) and `$Max`
## $J
- Extract using KAPE or `MFTEcmd`, `NTFS Log Tracker`
![[Pasted image 20260520011612.png]]
1. File name
2. File extension
3. Entry Number
4. Parent Entry number: If this record belongs to a file, this field will contain the parent folder entry number. This field will include the host file (that this stream is part of) entry number if it belongs to a data stream (ADS).
5. Update reason contains changes that happened to the object, such as rename and deletion.
6. The file attributes field contains attributes associated with the file (ex., hidden).