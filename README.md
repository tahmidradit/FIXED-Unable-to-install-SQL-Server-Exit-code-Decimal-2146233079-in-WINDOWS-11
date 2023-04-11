# FIXED-Unable-to-install-SQL-Server-Exit-code-Decimal-2146233079-in-WINDOWS-11

Windows 11 based machines using high-end storage devices like SAMSUNG 250GB NVMe M.2 SSD 980 or similar having the system disk sector size(PhysicalBytesPerSectorForAtomicity) is greater than 4KB/4096. This value throws an error while installing Microsoft SQL Server : 
Oops Unable to install  SQL Server Exit code (Decimal) - 2146233079 
Error Description Cannot process request because the process (5220) has exited.


----FIX (Using Command Prompt)----
1. Open Command Prompt as Administrator(Right click and select Run As Administrator)
2. Give the following command written below - 

   > reg add "HKLM\SYSTEM\CurrentControlSet\Services\stornvme\Parameters\Device" /v "ForcedPhysicalSectorSizeInBytes" /t reg_multi_sz /d "* 4095" /f
3. Done. To verify/check the value of PhysicalBytesPerSectorForAtomicity, Give the following command written below -

   > reg add "HKLM\SYSTEM\CurrentControlSet\Services\stornvme\Parameters\Device" /v "ForcedPhysicalSectorSizeInBytes"


See more at https://learn.microsoft.com/en-us/troubleshoot/sql/database-engine/database-file-operations/troubleshoot-os-4kb-disk-sector-size
