# Slow Computer Performance Troubleshooting Runbook

**Category:** System Performance Issues  
**Supported OS:** Windows 10 / 11  
**Estimated Time:** 20–40 minutes  
**Last Updated:** 2026-03

---

## Problem Description

User reports one or more of the following:
- Computer takes a long time to boot
- Programs take a long time to open
- Frequent freezing or "Not Responding" errors during use
- Fan running loudly but computer still slow
- Computer gets progressively slower over time

---  

## First Step: Gather Basic Information

Ask the user the following questions before proceeding to narrow down the cause:

| Question | Possible Direction |
|---|---|
| Has it always been slow, or did it start recently? | Recently slow → possible update, new software, or virus |
| Slow from boot, or only after extended use? | Slow from boot → too many startup programs; slow after extended use → memory leak or overheating |
| Is everything slow, or only specific programs? | Specific programs slow → issue with that program itself |
| Was any new software installed recently? | Yes → possible software conflict |
| How old is the computer? | Over 5 years → possible hardware aging |

---

## Step 1: Check Current Resource Usage

Open Task Manager for a quick diagnosis:

1. Press `Ctrl + Shift + Esc`
2. Click the **Performance** tab
3. Check the following values:

| Component | Normal Range | Needs Attention |
|---|---|---|
| CPU | Below 20% at idle | Consistently above 80% |
| Memory | Below 80% | Above 90% |
| Disk | Below 50% | Consistently at 100% |
| GPU | Depends on usage | Consistently above 50% at idle |  

4. Click the **Processes** tab, sort by CPU or Memory, and identify the most resource-intensive programs

---  

## Step 2: End Resource-Heavy Processes

1. Task Manager → **Processes** tab
2. Identify programs consuming high CPU or memory
3. Right-click → **End task**

**Do not end the following processes even if they consume resources:**
- System / System Idle Process
- Windows Security
- Antimalware Service Executable (Windows Defender)

---

## Step 3: Disable Unnecessary Startup Programs

Too many startup programs is one of the most common causes of slow boot times:

1. Task Manager → **Startup** tab
2. Review the "Startup impact" column for each program
3. Right-click programs that do not need to launch at startup → **Disable**

Common programs safe to disable:
- Spotify, Discord, Teams (open manually when needed)
- OneDrive (if not frequently used)
- Updater programs for various applications

**Do not disable:**
- Windows Security
- Audio or graphics driver-related programs
- Any system program whose purpose is unclear

---

## Step 4: Check Disk Space

Insufficient disk space can significantly impact performance:

1. Open File Explorer → This PC
2. Check the remaining space on the C: drive

| Free Space | Status |
|---|---|
| Above 20% | Normal |
| 10–20% | Cleanup recommended |
| Below 10% | Immediate cleanup required |

### Run Disk Cleanup

1. Search for "Disk Cleanup" → Select C: drive
2. Check all items
3. Click **Clean up system files**, check all items again → OK

---

## Step 5: Scan for Malware

Viruses and malware are a common cause of slow performance:

1. Start → **Windows Security**
2. **Virus & threat protection** → **Quick scan**
3. If threats are found, follow the on-screen instructions to remove them
4. If malware is suspected but the quick scan finds nothing, run a **Full scan** (takes longer)

---

## Step 6: Run Disk Defragmentation or Optimization

1. Search for "Defragment and Optimize Drives"
2. Select C: drive → Click **Optimize**

**Important:**
- HDD (hard disk drive) → Runs defragmentation
- SSD (solid state drive) → Runs optimization (Trim) — do not defragment an SSD

Not sure if HDD or SSD? Run:
```cmd
winsat disk
```
If "Timed Sequential Write" speed exceeds 400MB/s, it is likely an SSD.

---

## Step 7: Update Windows and Drivers

Outdated system software and drivers can cause performance issues:

1. Settings → Windows Update → **Check for updates**
2. Install all available updates
3. Device Manager → Check graphics card, network adapter, and chipset drivers are up to date

---

## Step 8: Adjust Power Settings

Confirm the power plan is set to High Performance:

1. Control Panel → Power Options
2. Select **High performance** (recommended only when laptop is plugged in)

If High Performance option is not visible, run:
```cmd
powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61
```
Reopen Power Options after running the command.

---

## Step 9: Check Thermal Performance

CPU overheating causes automatic throttling, which reduces performance:

Use a free tool such as **HWMonitor** or **Core Temp** to check temperatures:

| Component | Normal Range | Needs Attention |
|---|---|---|
| CPU (idle) | 30–50°C | Above 70°C |
| CPU (under load) | 60–80°C | Consistently above 90°C |
| SSD | 30–50°C | Above 70°C |

If temperatures are too high:
- Confirm laptop vents are not blocked
- Clean fan vents with compressed air
- Consider reapplying thermal paste (recommend experienced technician)

---

## Step 10: Evaluate Hardware Upgrade

If all steps above have been completed and performance is still poor, the hardware may be insufficient:

| Upgrade | Effect | Difficulty | Estimated Cost |
|---|---|---|---|
| Add RAM | Improves multitasking performance | Low | ~NT$500–2,000 |
| Replace HDD with SSD | Significantly improves boot and read/write speed | Medium | ~NT$1,500–4,000 |
| Reinstall Windows | Clears accumulated system issues | Medium | Free |

**Recommended upgrade priority:**
1. If C: drive is HDD → Replace with SSD (most impactful upgrade)
2. If RAM is below 8GB → Upgrade to 16GB
3. If still slow after both → Consider reinstalling Windows

---
## Common Symptoms Reference

| Symptom | Most Likely Cause | Check First |
|---|---|---|
| Slow boot | Too many startup programs | Step 3 |
| Gets slower after extended use | Memory leak or overheating | Step 1, Step 9 |
| Disk consistently at 100% | Malware or system issue | Step 5, Step 6 |
| CPU consistently high | Malware or software conflict | Step 2, Step 5 |
| Fan running constantly | CPU overheating | Step 9 |
| Suddenly slow recently | Update or new software issue | Step 7, Step 3 |

---

## Resolution Log

| Field | Details |
|---|---|
| Issue Description | |
| Computer Model | |
| RAM Capacity | |
| Drive Type (HDD/SSD) | |
| Steps Performed | |
| Resolution | |
| Time Spent | |
| Notes | |

---  

*Author: Gua, Huang / References: Google IT Support Certificate, Microsoft Docs*  
