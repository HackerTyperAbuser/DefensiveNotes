- UnpackMe (Yara Hunt > New Hunt)

```yara
rule Ransomware_WannaCry {
	meta:
		author: "Nguyen Nghia Hiep"
		version: "1.0"
		description: "Sample Yara rule for detection"
		reference: "https://test.com"
	
	strings:
		$wannacry_payload_str1 = "tasksche.exe" fullword ascii
        $wannacry_payload_str2 = "www.iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com" ascii
        $wannacry_payload_str3 = "mssecsvc.exe" fullword ascii

	condition:
		filesize < 100KB and (uint16(0) == 0x5A4D or uint16(0) == 0x4D5A)
}
```

(yarGen.py) Automating Yara Rules
```bash
python3 yarGen.py -m /home/htb-student/temp -o htb_sample.yar
```
(yara) YARA scanner 
```bash
yara <RULE> <DIR_TO_SEARCH>
```
### Windows
(yara64.exe) YARA Scanner Windows
- -r recursively searching
```powershell
yara64.exe -s <RULE> <DIR_TO_SEARCH> -r 2>null
```
(yara64.exe) Yara Scanner scan running Windows process
```powershell
Get-Process | ForEach-Object { "Scanning with Yara for meterpreter shellcode on PID "+$_.id; & "yara64.exe" "C:\Rules\yara\meterpreter_shellcode.yar" $_.id }
```
(yara64.exe) Yara Scanner scan a specific Windows process
```powershell
yara64.exe -s <RULE> <PID> --print-strings
```

### Linux

