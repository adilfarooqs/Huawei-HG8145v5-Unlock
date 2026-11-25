# Unlock Huawei HG8145V5 — Set Provider Lock to COMMON

A step-by-step guide to removing the provider lock on the Huawei HG8145V5 ONT and switching the Custom Info to **COMMON**, restoring WAN and the Software Upgrade menu.

## Device Info

Check these values on the device's web interface before starting.

| Field | Value |
|---|---|
| Device Type | HG8145V5 |
| Hardware Version | 26AD.A |
| Software Version | V5R022C10S197 |

**Symptoms of a locked device:**

- ❌ No WAN
- ❌ No "Software Update" menu
- ✅ "Update Configuration File" available

## Requirements

- `Configuration-Default.xml`
- `R022.bin` (shell file)
- Panda Flasher (optional, if no Software Upgrade menu)

## Instructions

> **Note:** For firmware older than R021 (and below), **skip Step 3** — no downgrade is needed.

### Step 1 — Upload default config

Upload `2Config-DEFAULT.xml`
Login: `telecomadmin` / `admintelecom`

### Step 2 — Upload the shell file

Upload `R022.bin`

- Use the **Software Upgrade** menu.
- If there is no Software Upgrade menu, use **Panda Flasher** instead.

### Step 3 — Downgrade R022 to R020/R021

1. Run `Huawei-Downgrade-Tools.exe` → (device restarts)
2. Log in to the web interface, change **RED** → **Firmware Upgrade** menu
3. Upload the firmware:
   - **HG series:** `HG8145V5-R020-212.bin` → (restart)
   - **EG series:** `EG8145V5-R021-210.bin` → (restart)

> Sometimes, after downgrading, the EG type reverts to `192.168.18.1` (login: `Epadmin` / `adminEp`).
> In that case, upload `2Config-DEFAULT.xml` again (login: `telecomadmin` / `admintelecom`).

### Step 4 — Run the PON tool

Run `Huawei-PON-Tools-HG8145V5.exe`:

1. Click **1**
2. Click **2** — the modem reboots; wait 10–20s after the LAN light turns on
3. Click **3**
4. Click **4**
5. Choose mode: **GPON / EPON / XPON**
6. Click **5** — Done (modem reboots)

### Step 5 — Roll back to original

Double-click `RollBackCommand.bat` to restore the original R022 version.

## Expected Result

- ✅ Web interface changes to **BLUE**
- ✅ Custom Info: **COMMON**
- ✅ WAN working
- ✅ Software Upgrade menu available

## Features

- Updated GPON option to remove vendor lock (PTCL / Pakistan)
- Fixed GPON blinking every 2–5 minutes
- Added vendor-lock removal to the XPON option
