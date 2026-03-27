# Website Cannot Connect Troubleshooting Runbook

**Category:** Network Issues  
**Supported OS:** Windows 10 / 11  
**Last Updated:** 2026-03

---

## Problem Description

User reports one or more of the following:
- A specific website cannot be opened
- All websites cannot be opened
- Browser displays an error code (e.g. 404, 502, ERR_CONNECTION_TIMED_OUT)
- Website stops loading halfway
- One website is slow but others load normally

---

## First Step: Determine Scope of Impact

Ask the user the following two questions:

**Question 1: Is it all websites, or only a specific website?**
- All websites → Issue is with the network connection itself → Start from Step 1
- Specific website → Issue may be with that website or DNS → Skip to Step 4

**Question 2: Are other devices also unable to reach the same website?**
- Yes → The website itself may be down → Skip to Step 3
- No → Issue is with this computer → Start from Step 1

---  

## ⚠️ Special Case: Browser Displays an Error Code

Use the table below to identify the error type before continuing:

| Error Code | Meaning | Possible Cause |
|---|---|---|
| ERR_CONNECTION_TIMED_OUT | Connection timed out | Network issue or website not responding |
| ERR_NAME_NOT_RESOLVED | Domain not found | DNS issue |
| ERR_CONNECTION_REFUSED | Connection refused | Server issue or firewall blocking |
| ERR_SSL_PROTOCOL_ERROR | SSL certificate error | Incorrect system time or expired certificate |
| 404 Not Found | Page not found | Incorrect URL or page has been removed |
| 502 Bad Gateway | Gateway error | Website server issue |
| 503 Service Unavailable | Service unavailable | Website overloaded or under maintenance |

---

## Step 1: Confirm Network Connection Status

- [ ] Confirm Wi-Fi or network cable is connected
- [ ] Confirm other websites load normally (e.g. google.com)
- [ ] If Wi-Fi is connected but all websites are unreachable, refer to the Wi-Fi Troubleshooting Runbook

---

## Step 2: Refresh and Basic Browser Operations

Start with the simplest methods first:

1. Press `F5` or `Ctrl + R` to refresh the page
2. Press `Ctrl + Shift + R` to force refresh (clears cache and reloads)
3. Try opening the same URL in **Private / Incognito mode**:
   - Chrome / Edge: `Ctrl + Shift + N`
   - Firefox: `Ctrl + Shift + P`
4. Try opening the URL in a **different browser**

**Interpret results:**

| Result | Meaning |
|---|---|
| Opens in Incognito mode | Issue is with browser cache or extensions → Skip to Step 6 |
| Opens in a different browser | Issue is with the original browser → Skip to Step 6 |
| Neither method works | Continue to Step 3 |

---

## Step 3: Confirm Whether the Website Itself is Down

Visit either of the following sites to check if the website is down globally
(results are for reference only — check both and compare):
- https://downforeveryoneorjustme.com
- https://www.isitdownrightnow.com

**Interpret results:**

| Result | Action |
|---|---|
| Website confirmed down | Wait for the website to recover — no further troubleshooting needed |
| Website is up, only you cannot connect | Continue to Step 4 |

---

## Step 4: Test Network Connectivity

Open Command Prompt or PowerShell (run as Administrator) and test connectivity:
```cmd
ping google.com
```
```cmd
ping 8.8.8.8
```

**Interpret results:**

| Result | Meaning | Action |
|---|---|---|
| Both google.com and 8.8.8.8 respond | Network is working, issue is with browser or DNS | Step 5 |
| google.com no response, but 8.8.8.8 responds | DNS issue | Step 5 |
| Both do not respond | Network connectivity issue | Refer to Wi-Fi Troubleshooting Runbook |

---

## Step 5: Change DNS Server

DNS issues are one of the most common causes of specific websites being unreachable:

1. Control Panel → Network and Sharing Center → Change adapter settings
2. Right-click the active network adapter → **Properties**
3. Select **Internet Protocol Version 4 (TCP/IPv4)** → **Properties**
4. Select **Use the following DNS server addresses**:
   - Preferred: `8.8.8.8` (Google)
   - Alternate: `1.1.1.1` (Cloudflare)
5. Click OK and retry the connection

### Clear DNS Cache

Run the following command to clear outdated DNS records:
```cmd
ipconfig /flushdns
```

---

## Step 6: Clear Browser Cache and Cookies

Corrupted browser cache can prevent specific websites from loading:

### Chrome / Edge
1. Press `Ctrl + Shift + Delete`
2. Set time range to **All time**
3. Check the following:
   - Browsing history
   - Cookies and other site data
   - Cached images and files
4. Click **Clear data**

### Firefox
1. Press `Ctrl + Shift + Delete`
2. Set time range to **Everything**
3. Check Cookies and Cache
4. Click **Clear Now**

Reopen the browser after clearing and test again.

---

## Step 7: Rule Out Browser Extension Interference

Certain extensions (such as ad blockers, VPNs, or antivirus tools) may interfere with website connections. Use the methods below to test — avoid disabling security-related extensions directly.

### Method 1: Test Using Incognito Mode (Recommended first)

Incognito mode disables all extensions by default and is the safest testing method:
- Chrome / Edge: `Ctrl + Shift + N`
- Firefox: `Ctrl + Shift + P`

If the website opens in Incognito mode → Confirmed extension interference, continue to Method 2.  
If the website still cannot open → Issue is not extension-related, skip to Step 8.

### Method 2: Create a New Browser Test Profile

Test using a fresh profile with no extensions installed — no changes to the original profile needed:

**Chrome:**
1. Click the profile avatar (top right) → Add profile
2. Open the website using the new profile

**Edge:**
1. Click the profile avatar (top right) → Add profile
2. Open the website using the new profile

**Firefox:**
1. Close Firefox
2. Press `Win + R`, type `firefox.exe -P` → Enter
3. Click "Create Profile" → Launch with the new profile

If the website opens with the new profile → Return to the original profile and disable extensions one by one to identify the cause.

### Method 3: Disable Extensions One by One (Last resort)

Only use this method if the above approaches cannot identify the cause.  
**Recommended disable order: non-security extensions first, security extensions last.**

Suggested order:
1. Ad blockers (e.g. uBlock Origin, AdBlock)
2. Translation tools
3. Shopping comparison tools
4. VPN extensions
5. Antivirus extensions (disable last)

**Note:** Test after disabling each extension. Once the cause is identified, re-enable all other extensions — especially security-related ones.

---

## Step 8: Check Firewall and Antivirus Settings

Firewall or antivirus software may be incorrectly blocking a website.

**Do not disable the firewall or antivirus protection entirely.**

### Method 1: Add the Website to the Antivirus Whitelist
1. Open the antivirus software settings
2. Find the "Website Whitelist", "Exclusion List", or "Trusted Sites" option
   (the exact label varies by antivirus software)
3. Add the affected website URL to the whitelist
4. Retry the connection

### Method 2: Check if Windows Defender Firewall is Blocking the Connection
1. Control Panel → Windows Defender Firewall
2. Click "Allow an app or feature through Windows Defender Firewall" on the left
3. Confirm the browser is in the allowed list
4. If not → Click "Change settings" → "Allow another app" → Add the browser

**Note:** If whitelisting does not resolve the issue and antivirus interference is still suspected, the firewall or protection may be temporarily disabled for testing purposes only. Re-enable it immediately after testing.

---

## Step 9: Reset Browser Settings

If all previous steps have not resolved the issue, try resetting the browser to its default settings:

### Chrome
1. Settings → Reset settings → Restore settings to their original defaults
2. Click **Reset settings**

### Edge
1. Settings → Reset settings → Restore settings to their default values
2. Click **Reset**

### Firefox
1. Type `about:support` in the address bar
2. Click **Refresh Firefox**

---

## Step 10: Check the Hosts File

If the Hosts file has been modified by malware, specific websites may be blocked:

1. Open Notepad as Administrator
2. Open the file: `C:\Windows\System32\drivers\etc\hosts`
3. Check whether any suspicious URLs have been added to the file
4. If suspicious entries are found, delete them and save the file

A normal Hosts file should only contain lines starting with `#` (comments), plus:
```
127.0.0.1    localhost
::1          localhost
```

If additional URLs appear, this may indicate malware activity — run a full antivirus scan immediately.

---

## Common Error Messages

| Error Message | Possible Cause | Solution |
|---|---|---|
| ERR_CONNECTION_TIMED_OUT | Network issue or website not responding | Step 1 → Step 4 |
| ERR_NAME_NOT_RESOLVED | DNS issue | Step 5 |
| ERR_CONNECTION_REFUSED | Firewall blocking or website issue | Step 8 → Step 3 |
| ERR_SSL_PROTOCOL_ERROR | Incorrect system time or certificate issue | Verify system date and time is correct |
| 404 Not Found | Incorrect URL or page removed | Double-check the URL |
| 502 / 503 | Website server issue | Step 3 (check if website is down) |

---

## Resolution Log

| Field | Details |
|---|---|
| Issue Description | |
| Affected Website | |
| Browser Used | |
| Steps Performed | |
| Resolution | |
| Time Spent | |
| Notes | |

---  

*Author: Gua, Huang / References: Google IT Support Certificate, Microsoft Docs*
