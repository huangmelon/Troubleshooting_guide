# Wi-Fi Connection Troubleshooting Runbook

**Category:** Network Issues  
**Supported OS:** Windows 10 / 11  
**Estimated Time:** 10–20 minutes  
**Last Updated:** 2026-03

---

## Problem Description

User reports one or more of the following:
1. Cannot find any Wi-Fi networks
2. Can see the network but unable to connect
3. Connected but shows "No Internet Access"
4. Wi-Fi icon completely missing from taskbar
5. **Wi-Fi icon intermittently disappears (appears and disappears randomly)**

---

## First Step: Determine Scope of Impact

Ask the user: **Are other devices (phone, tablet) also unable to connect?**
- **Yes → Multiple devices affected:** Issue is with the router or ISP → Skip to Step 2B
- **No → Only this computer affected:** Issue is with the computer itself → Start from Step 1

---

## ⚠️ Special Case A: Wi-Fi Icon Completely Missing

If the Wi-Fi icon is completely absent from the taskbar, complete the following checks before continuing with general troubleshooting steps.

### Check A1: Confirm Icon is Not Hidden

1. Right-click an empty area on the taskbar → **Taskbar settings**
2. Find **System tray icons** (or "Notification area")
3. Confirm the **Network** icon is enabled

### Check A2: Restart Windows Explorer

1. Press `Ctrl + Shift + Esc` to open Task Manager
2. Find **Windows Explorer (explorer.exe)**
3. Right-click → **Restart**
4. Wait a few seconds — the icon should reappear

### Check A3: Confirm Network Adapter is Not Disabled

1. Right-click **Start** → **Device Manager**
2. Expand **Network adapters**
3. If the Wi-Fi adapter shows a gray down arrow → Right-click → **Enable device**

### Check A4: Confirm WLAN AutoConfig Service is Running

1. Press `Win + R`, type `services.msc` → Enter
2. Find **WLAN AutoConfig**
3. Confirm status is **Running** and startup type is **Automatic**
4. If not running → Right-click → **Start**

If all four checks pass but the icon is still missing → Continue to Step 6 (Update driver)

---

## ⚠️ Special Case B: Wi-Fi Icon Intermittently Disappears

If the Wi-Fi icon appears and disappears randomly, use the table below to identify the likely cause:

| Situation | Most Likely Cause |
|---|---|
| Disappears after computer is idle | Power management settings |
| Disappears randomly with no pattern | Unstable driver |
| Disappears when moving laptop or opening/closing lid | Hardware loose connection |
| Started after a Windows update | Driver compatibility issue |

### Check B1: Disable Power Management (Most common cause — start here)

1. Device Manager → Network adapters → Right-click Wi-Fi adapter → **Properties**
2. Click the **Power Management** tab
3. Uncheck "Allow the computer to turn off this device to save power"
4. Click OK and monitor if the issue persists

### Check B2: Update or Roll Back Driver

If the issue started after a recent update:
1. Device Manager → Network adapters → Right-click Wi-Fi adapter → **Properties**
2. Click the **Driver** tab → **Roll Back Driver**

If the issue has persisted but the driver version is outdated:
1. Note the adapter name
2. Download and install the latest driver from the manufacturer's website

### Check B3: Hardware Issue (Laptops only)

If the issue occurs when moving the laptop or opening/closing the lid, and software solutions have not resolved it:
- Document the conditions and frequency of the issue
- Recommend sending the device to a technician to inspect the Wi-Fi module connection
- Temporary workaround: Use a USB Wi-Fi adapter

### Check B4: Check Windows Update Status

1. Settings → Windows Update → Check for updates
2. If updates are available, install them and monitor the issue
3. If the issue resolves after updating, the root cause was a driver compatibility issue

---

## Step 1: Check Basic Status

- [ ] Confirm Airplane Mode is off (system tray, bottom right)
- [ ] Confirm Wi-Fi is turned on
- [ ] Confirm SSID (network name) appears in the available networks list

If no Wi-Fi networks appear at all → Likely a driver issue, skip to Step 6

---

## Step 2A: Restart Device (Single device affected)

1. Restart the computer
2. Attempt to reconnect

If still unable to connect → Continue to Step 3

---

## Step 2B: Restart Router (Multiple devices affected)

1. Unplug the router's power cable
2. Wait 30 seconds
3. Plug the power cable back in and wait 2 minutes for the router to fully restart
4. Attempt to reconnect

If still unable to connect → Contact ISP (Internet Service Provider)

---

## Step 3: Forget and Reconnect to Network

1. Click the Wi-Fi icon in the system tray
2. Find the target network → Click **Forget**
3. Reselect the network and enter the password

---

## Step 4: Check IP Address

Open Command Prompt (run as Administrator):
```cmd
ipconfig /all
```

**Interpret results:**

| IP Address Shown | Meaning | Action |
|---|---|---|
| 192.168.x.x | IP obtained successfully | Continue to next step |
| 169.254.x.x | DHCP failure | Run commands below |
| Blank | Network adapter not enabled | Skip to Step 5 |

If IP shows 169.254.x.x, run:
```cmd
ipconfig /release
ipconfig /renew
```

---

## Step 5: Reset Network Settings

Open Command Prompt as Administrator and run the following commands in order:
```cmd
netsh winsock reset
netsh int ip reset
ipconfig /flushdns
```

**Restart the computer** after running all commands, then test the connection.

---

## Step 6: Update Network Driver

1. Right-click **Start** → **Device Manager**
2. Expand **Network adapters**
3. Right-click the Wi-Fi adapter → **Update driver**
4. Select **Search automatically for drivers**

If automatic update finds nothing, note the adapter name and download the latest driver from the manufacturer's website.

---

## Common Error Messages

| Error Message | Possible Cause | Solution |
|---|---|---|
| Can't connect to this network | Network settings corrupted | Step 3 (Forget and reconnect) |
| DNS server not responding | DNS configuration issue | Manually set DNS to 8.8.8.8 |
| Connected but no internet access | IP conflict or gateway issue | Step 4 |
| No networks found | Driver issue | Step 6 |
| Wi-Fi icon missing | Icon hidden / adapter disabled / driver issue | Special Case A |
| Wi-Fi icon intermittently disappears | Power management / unstable driver / hardware issue | Special Case B |

---

## Manual DNS Configuration (Reference)

1. Control Panel → Network and Sharing Center → Change adapter settings
2. Right-click Wi-Fi → **Properties**
3. Select **Internet Protocol Version 4 (TCP/IPv4)** → **Properties**
4. Select **Use the following DNS server addresses**:
   - Preferred: `8.8.8.8` (Google)
   - Alternate: `1.1.1.1` (Cloudflare)

---

## Resolution Log

| Field | Details |
|---|---|
| Issue Description | Wi-Fi icon intermittently disappearing |
| Steps Performed | Special Case B |
| Resolution | All software solutions were ineffective. Confirmed hardware failure of the Wi-Fi module. Replaced with a Windows 11 compatible network adapter. |
| Time Spent | Approximately one week including observation period |
| Notes | |

---  

*Author: Gua, Huang / References: Google IT Support Certificate, Microsoft Docs* 
