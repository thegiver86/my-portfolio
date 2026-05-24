# 🩻 SIEM Threat Hunt Report: The Digital Autopsy

## 1. Forensic Intelligence Recovered
* **WHO (Threat Actor):** [Data unavailable/destroyed due to lab environment provisioning failure]
* **WHAT (Target File):** `Resume.exe`
* **WHEN (Infection Timestamp):** 2026-05-24 01:41:55 (UTC) - *Timestamp pulled from raw inode creation metadata.*
* **HOW (Persistence Mechanism):** The attacker utilized a hidden process named `rootkit_beacon.exe` (PID: 4444) running actively in volatile memory.

## 2. Technical Summary of Environment Failure
The forensic investigation successfully identified the orphaned pointer for the deleted malware (`Resume.exe` at Inode 582). However, payload extraction failed because the lab's provisioning script (`s29_provision.sh`) failed to flush/sync the mock payload data to the raw disk sectors before unmounting and simulating the deletion. 

As a result, the OS metadata correctly registered the file's deletion (Size 0), but the physical sector assigned to the file (Sector 108) contained only null bytes. Extensive block carving and full-drive string analysis confirmed the payload data was entirely absent from the `compromised_drive.dd` image.

## 3. Execution & Forensic Commands Log
The following forensic methodology was used to verify the missing data:

1. **Locate the Deleted File:** 
   `fls -r compromised_drive.dd`
   *(Identified the deleted `Resume.exe` file at Inode 582).*

2. **Attempt Data Extraction:** 
   `icat compromised_drive.dd 582 > recovered_malware.txt`
   *(Extraction resulted in a 0-byte file).*

3. **Interrogate Metadata:** 
   `istat compromised_drive.dd 582`
   *(Confirmed the file size was zeroed out, but identified the physical data location at Sector 108).*

4. **Raw Sector Verification:** 
   `blkcat compromised_drive.dd 108 | hexdump -C`
   *(Bypassed OS metadata to read the raw binary of the physical sector; confirmed the sector was empty/null).*

5. **Full Drive Carving:** 
   `strings compromised_drive.dd`
   *(Carved the entire raw disk image as a final measure; confirmed the payload text was not present anywhere on the drive).*
