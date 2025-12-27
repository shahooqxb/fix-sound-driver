# Fix Sound Driver on Windows 11 (PowerShell / CMD)

COPY → PASTE → RUN AS ADMIN

---

METHOD 1: RESTART AUDIO SERVICES

PowerShell (Admin)

net stop audiosrv
net stop AudioEndpointBuilder
net start AudioEndpointBuilder
net start audiosrv

RESTART PC

---

METHOD 2: SCAN AND RE-DETECT AUDIO HARDWARE

CMD (Admin)

pnputil /scan-devices

RESTART PC

---

METHOD 3: REINSTALL AUDIO DRIVER AUTOMATICALLY

PowerShell (Admin)

Get-PnpDevice -Class Sound,VideoAndGameControllers

Get-PnpDevice -Class Sound,VideoAndGameControllers | Disable-PnpDevice -Confirm:$false
Get-PnpDevice -Class Sound,VideoAndGameControllers | Enable-PnpDevice -Confirm:$false

RESTART PC

---

METHOD 4: REMOVE CORRUPT AUDIO DRIVER (ADVANCED)

CMD (Admin)

pnputil /enum-drivers | findstr /i audio

pnputil /delete-driver oemXX.inf /uninstall /force

(REPLACE oemXX.inf WITH REAL NAME)

RESTART PC IMMEDIATELY

---

METHOD 5: REPAIR WINDOWS AUDIO SYSTEM FILES

PowerShell (Admin)

sfc /scannow

DISM /Online /Cleanup-Image /RestoreHealth

RESTART PC

---

METHOD 6: RESET WINDOWS AUDIO REGISTRY

PowerShell (Admin)

reg delete "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\MMDevices\Audio" /f

RESTART PC IMMEDIATELY

---

IF SOUND STILL DOES NOT WORK:
- AUDIO DISABLED IN BIOS
- HARDWARE DAMAGE
- INSTALL OFFICIAL DRIVER FROM LAPTOP MANUFACTURER

LICENSE: MIT
