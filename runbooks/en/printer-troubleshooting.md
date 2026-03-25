# Printer Connection Troubleshooting Runbook  

**category:** Printer Issues  
**Supported OS:** Windows10/11  
**Estimated Time:** 15-30 minutes  
**Last Updated:** 2026-03  

---  

## Problem Description  

User reports one or more of the following:  
- Printer displays "Offline" status
- No response after sending a print job
- Printer device not found
- Print queue is stuck and cannot be cleared
- Wireless printer unable to connect

---  

## First Step: Identity Connection Type  

Confirm how the printer is connected, as troubleshooting steps differ:  

| Connection Type | Common Issues |  
|---|---|  
| USB (direct connection) | Cable, driver, or USB port issues |  
| Local network (wired/wireless) | IP address or network connectivity issues |  
| Shared Printer (via another computer) | Sharing settings or permissions issues |  

---  

## ⚠️ Special Case: Print Queue Stuck

If print jobs are stuck in the queue and cannot be deleted, complete the following steps before continuing:

1. Press `Win + R`, type `services.msc` → Enter
2. Find **Print Spooler** → Right-click → **Stop**
3. Open File Explorer, navigate to the path below and delete all files inside (do not delete the folder itself):
```

C:\Windows\System32\spool\PRINTERS
```
4. Return to services.msc → Print Spooler → Right-click → **Start**
5. Retry printing

---  

## Step 1: Check Basic Hardware Status

- [ ] Is the printer powered on?
- [ ] Does the printer panel show any error messages or warning lights?
- [ ] Is paper loaded correctly? Any paper jams?
- [ ] Is ink or toner level sufficient?
- [ ] Is the USB cable securely connected? (USB connection only)

---

## Step 2: Restart All Devices

1. Power off the printer, wait 30 seconds, then power it back on
2. Restart the computer
3. If using a wireless printer, restart the router as well
4. Wait for all devices to fully boot up before testing again
---

## Step 3: Confirm Printer is Set to Online

1. Settings → Bluetooth & devices → Printers & scanners
2. Select the target printer
3. If status shows "Offline":
   - Click **Open print queue**
   - Top menu → **Printer** → Confirm "Use Printer Offline" is **unchecked**

---

## Step 4: Set as Default Printer

1. Settings → Bluetooth & devices → Printers & scanners
2. Disable "Let Windows manage my default printer"
3. Right-click the target printer → **Set as default printer**

---

## Step 5: Check USB Connection (USB only)

1. Unplug the USB cable and reconnect to a different USB port
2. Try replacing the USB cable
3. Open Device Manager and confirm the printer appears without a yellow warning symbol

If a yellow warning symbol is present → Skip to Step 7 (Reinstall driver)

---

## Step 6: Check Network Connection (Wireless/Network printer only)

### Find the Printer's IP Address

Print a "Network Configuration Page" or "Status Report" from the printer panel to obtain the current IP address.

### Test Network Connectivity

Open Command Prompt and run (replace x.x.x.x with the printer's actual IP):
```cmd
ping x.x.x.x
```

**Interpret results:**

| Result | Meaning | Action |
|---|---|---|
| Reply from x.x.x.x | Network connection is working | Continue to Step 7 |
| Request timed out | Computer cannot reach the printer | Check if both are on the same subnet |
| Unable to connect | Printer is not connected to the network | Reconfigure printer Wi-Fi settings |

### Fix IP Address (Recommended)

If the printer's IP changes frequently, configure a DHCP Reservation in the router settings to assign a fixed IP to the printer, preventing connection issues after IP changes.

---  
## Step 7: Reinstall Printer Driver

1. Settings → Bluetooth & devices → Printers & scanners
2. Select the target printer → **Remove**
3. Download the latest driver from the manufacturer's website:
   - HP: support.hp.com
   - Canon: canon.com
   - Epson: epson.com
   - Brother: support.brother.com
4. Run the installer and follow the on-screen instructions
5. Restart the computer and test printing

---

## Step 8: Run Windows Printer Troubleshooter

1. Settings → System → Troubleshoot → Other troubleshooters
2. Find **Printer** → Click **Run**
3. Follow the on-screen instructions
4. Test printing again

---

## Step 9: Check Print Spooler Service

1. Press `Win + R`, type `services.msc` → Enter
2. Find **Print Spooler**
3. Confirm status is **Running** and startup type is **Automatic**
4. If not running → Right-click → **Start**
5. If running but still having issues → Right-click → **Restart**

---

## Step 10: Check Shared Printer Settings (Shared printer only)

If the printer is shared through another computer:

1. Confirm the host computer is powered on and logged in
2. Confirm Print Spooler service is running on the host computer
3. On the host computer: Control Panel → Devices and Printers → Right-click printer → **Printer properties** → **Sharing** tab → Confirm sharing is enabled
4. Confirm both computers are on the same network
5. Try adding the network printer again: Settings → Bluetooth & devices → Add device

---

## Common Error Messages

| Error Message | Possible Cause | Solution |
|---|---|---|
| Printer offline | Connection lost or settings issue | Step 3 |
| Driver unavailable | Driver missing or corrupted | Step 7 |
| Print Spooler service not running | Service stopped unexpectedly | Step 9 |
| Access denied | Permission issue | Step 10 |
| Print queue stuck | Spooler temp files corrupted | Special Case |
| Printer not found | Network or driver issue | Step 6 → Step 7 |

---

## Resolution Log

| Field | Details |
|---|---|
| Issue Description | |
| Printer Model | |
| Connection Type | |
| Steps Performed | |
| Resolution | |
| Time Spent | |
| Notes | |

---  

*Author: Gua, Huang / References: Google IT Support Certificate, Microsoft Docs* 


