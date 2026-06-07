# Hives, Keys and Values

# Transaction Logs (Cache Registry)
Changing frequently the registry can cause performance issues in Windows. Windows use transaction logs to cache changes and write them all in one shot. Written when:
- system becomes idle
- before a shutdown
- after an hour has passed since last update
- if system failure before written from the log to hive they are written in the next boot.

Written in the same directory as their corresponding hives and use filename as their hives. These are pending updates, until hives are up to date they are known as dirty hives.
![[Pasted image 20260510015527.png]]