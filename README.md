# 🔊 Windows 11 Sound Driver Fix Toolkit (PowerShell / CMD)

<p align="center">
  <img src="https://img.shields.io/badge/OS-Windows%2011-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Shell-PowerShell%20%7C%20CMD-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Audio-Driver%20Fix-success?style=for-the-badge">
  <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge">
</p>

<p align="center">
A developer-style toolkit to fix <b>missing, deleted, or broken sound drivers</b><br>
on <b>Windows 11</b> using <b>native PowerShell and CMD commands only</b>.
</p>

---

## 📌 Overview

This repository fixes common Windows 11 audio problems caused by:
- Windows Updates
- Corrupted or deleted drivers
- Audio services not running
- Registry or system file corruption

No third-party tools. No installers. No malware.

---

## ⚠️ Requirements

- Windows 11
- Administrator privileges
- PowerShell (Run as Administrator)

---

## 🚀 ONE-CLICK FULL AUTO FIX (RECOMMENDED)

> Runs **ALL METHODS (1–5)** automatically  
> Restart services → scan hardware → reinstall drivers → repair system → reset registry

### ▶ Copy & paste into **PowerShell (Admin)**

```powershell
# ==========================================
# WINDOWS 11 AUDIO DRIVER FULL AUTO FIX
# ==========================================

Write-Host "Starting Windows Audio Repair..." -ForegroundColor Cyan

# METHOD 1: Restart Audio Services
Write-Host "Restarting Audio Services..."
net stop audiosrv /y
net stop AudioEndpointBuilder /y
net start AudioEndpointBuilder
net start audiosrv

# METHOD 2: Scan & Re-detect Audio Hardware
Write-Host "Scanning for Audio Devices..."
pnputil /scan-devices

# METHOD 3: Reinstall Audio Drivers
Write-Host "Reinstalling Audio Drivers..."
Get-PnpDevice -Class Sound,VideoAndGameControllers -ErrorAction SilentlyContinue |
Disable-PnpDevice -Confirm:$false
Start-Sleep -Seconds 3
Get-PnpDevice -Class Sound,VideoAndGameControllers -ErrorAction SilentlyContinue |
Enable-PnpDevice -Confirm:$false

# METHOD 4: Repair System Files
Write-Host "Running System File Checker..."
sfc /scannow

Write-Host "Running DISM Image Repair..."
DISM /Online /Cleanup-Image /RestoreHealth

# METHOD 5: Reset Windows Audio Registry
Write-Host "Resetting Audio Registry..."
reg delete "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\MMDevices\Audio" /f

Write-Host "Audio Repair Completed. PLEASE RESTART YOUR PC." -ForegroundColor Green

