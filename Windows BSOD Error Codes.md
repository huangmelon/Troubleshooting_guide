# Windows BSOD Error Code List 

|Stop Code| Name | Common Causes | Troubleshooting Steps|
|---------|---------|---------|---------|
| 0x0000000A | IRQL_NOT_LESS_OR_EQUAL | Faulty drivers, memory issues | Update drivers, check RAM |
| 0x0000001A | MEMORY_MANAGEMENT | Corrupted memory | Run Windows Memory Diagnostic |
| 0x0000001E | KMODE_EXCEPTION_NOT_HANDLED| Driver or kernel error | Update or remove problematic drivers|
| 0x00000024 | NTFS_FILE_SYSTEM | Disk or file system corruption | Run chkdsk /f /r |
| 0x0000002E | DATA_BUS_ERROR | Memory or hardware failure | Check RAM, motherboard |
| 0x0000003B | SYSTEM_SERVICE_EXCEPTION | Driver or system service error | Update Windows and drivers |
| 0x0000003D | INTERRUPT_EXCEPTION_NOT_HANDLED | Driver or hardware conflicts | Update drivers | 
| 0x00000050 | PAGE_FAULT_IN_NONPAGED_AREA | Invalid memory access | Check RAM, drivers |
| 0x00000051 | REGISTRY_ERROR | I/O issues or disk corruption | sfc/scannow, fix boot sector | 
| 0x0000007B | INACCESSIBLE_BOOT_DEVICE | Boot device not accessible | Check disk, BIOS, SATA settings |
| 0x0000007E | SYSTEM_THREAD_EXCEPTION_NOT_HANDLED | Driver or system error | Update GPU / device drivers |
| 0x0000007F | UNEXPECTED_KERNEL_MODE_TRAP | CPU or memory failure | Check hardware (CPU/RAM) |
| 0x0000009F | DRIVER_POWER_STATE_FAILURE | Power management driver issue | Update drivers, disable power saving |
| 0x000000D1 | DRIVER_IRQL_NOT_LESS_OR_EQUAL | Driver accessing invalid memory | Update or rollback drivers |
| 0x000000EA | THREAD_STUCK_IN_DEVICE_DRIVER | GPU driver stuck | Update graphics driver |
| 0x000000F4 | CRITICAL_OBJECT_TERMINATION | system process stops accidentally | check disk, scan malware |  
| 0x00000101 | CLOCK_WATCHDOG_TIMEOUT | CPU core not responding | Check CPU, update BIOS |
| 0x00000109 | CRITICAL_STRUCTURE_CORRUPTION | Kernel corruption (driver/malware) | Scan malware, update drivers |
| 0x00000116 | VIDEO_TDR_FAILURE | GPU failure or driver issue | Update or reinstall GPU driver |
| 0x00000124 | WHEA_UNCORRECTABLE_ERROR | Hardware failure (CPU, motherboard) | Check hardware, temperature |
| 0x00000133 | DPC_WATCHDOG_VIOLATION | SSD or driver issue | Update SSD firmware, drivers |
| 0x00000139 | KERNEL_SECURITY_CHECK_FAILURE | Memory or driver corruption | Check RAM, run SFC |
| 0x0000013A | KERNEL_MODE_HEAP_CORRUPTION | Memory corruption | Check drivers, RAM |
| 0x0000013D | INVALID_CALLBACK_STACK_ADDRESS | Driver issue | Update or remove faulty driver |
| 0x0000014C | REFERENCE_BY_POINTER | Memory management issue | Check RAM |
| 0x00000154 | UNEXPECTED_STORE_EXCEPTION | Storage failure | Check SSD/HDD health |
| 0x00000155 | KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION | Kernel resource leak | Driver or system issue |
| 0x0000021A | STATUS_SYSTEM_PROCESS_TERMINATED | Critical system process failure | Repair system files |
| 0xC000021A | STATUS_SYSTEM_PROCESS_TERMINATED | Winlogon / CSRSS crash | System restore or reinstall |
| 0xC0000221 | STATUS_IMAGE_CHECKSUM_MISMATCH | Corrupted system files | Run SFC /scannow |
| 0xDEADDEAD | MANUALLY_INITIATED_CRASH | Manually triggered crash (debugging) | For testing purposes |

--------

# Event ID List 

|Event ID | Log Type | Source | Description | troubleshooting   |
|------|------|------|------|------|
| 1 | System | WHEA-Logger | System crash (BSOD) with stop code recorded | Check dump file, analyze stop code, update drivers |
| 7 | System | Disk | Bad block detected on disk | Run chkdsk, check disk health (SMART), replace disk if needed |
| 9 | System | Disk | I/O error on disk device | Check cables, controller, disk hardware |
| 11 | System | Disk | Controller error on disk | Verify storage controller, update drivers/firmware |
| 41 | System | Kernel-Power | Unexpected shutdown without clean shutdown | Check power supply, overheating, BSOD logs |
| 51 | System | Disk | Paging I/O error | Check disk performance, run diagnostics |
| 55 | System | NTFS | File system corruption detected | Run chkdsk /f /r, repair file system |
| 157 | System | Disk | Disk removed unexpectedly | Check cable, power, disk connection |
| 1000 | Application | Application Error | Application crashed | Check app logs, reinstall/update application |
| 1001 | System | BugCheck | Dump file generated after crash | Analyze dump file (WinDbg), correlate with BSOD |
| 1002 | Application | Application Hang | Application not responding | Check CPU/memory usage, restart or debug app |
| 1014 | System | DNS Client | DNS resolution failure | Check DNS server settings, network connectivity |
| 1026 | Application | .NET Runtime | .NET application exception | Check stack trace, update .NET/runtime |
| 1102 | Security | EventLog | Security log was cleared | Investigate potential malicious activity |
| 4201 | System | Tcpip | Network interface connected/disconnected | Check network stability, drivers |
| 4227 | System | Tcpip | TCP/IP port exhaustion | Check for too many connections, tune system limits |
| 4624 | Security | Microsoft Windows Security Auditing | Successful logon | Audit user access if needed |
| 4625 | Security | Microsoft Windows Security Auditing | Failed logon attempt | Check credentials, investigate brute force |
| 4634 | Security | Microsoft Windows Security Auditing | User logoff | Track session activity |
| 4672 | Security | Microsoft Windows Security Auditing | Admin privileges assigned | Monitor privileged access |
| 4720 | Security | Microsoft Windows Security Auditing | New user account created | Verify account creation legitimacy |
| 4726 | Security | Microsoft Windows Security Auditing | User account deleted | Audit account removal |
| 4732 | Security | Microsoft Windows Security Auditing | User added to security group | Verify permission changes |
| 6005 | System | EventLog | Event Log service started | Indicates system startup |
| 6006 | System | EventLog | Event Log service stopped | Indicates clean shutdown |
| 6008 | System | EventLog | Unexpected shutdown detected | Investigate crash or power issue |
| 7036 | System | Service Control Manager | Service started or stopped | Monitor service status changes |
| 7045 | System | Service Control Manager | New service installed | Check for unauthorized software/malware |
