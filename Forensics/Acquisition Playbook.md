- [[Disk Acquisition]]
- [[Memory Acquisition]]
```text
- Acquire a memory image. 
    - If the machine is powered on, perform a live memory acquisition.
    - If the machine is powered off, use memory artifacts like hiberfil.sys, pagefile.sys, and crash dumps.
- Acquire a triage image followed by a disk image.
    - If the machine is powered on:
        -  Check for encryption. If there are encrypted drives, acquire a live triage image followed by disk images for logical drives.
        - If the disk is not encrypted, pull off the power cable and acquire a dead triage and disk images. Do not do a graceful shutdown, or you will risk losing essential artifacts. Pulling the cable will save the disk in its current state and preserve evidence, except in SSD drives.
    - If the machine is powered off (not encrypted)
        - Acquire a triage image followed by physical disk acquisition using write-blockers.
- Mount the image and analyze the evidence.
```
