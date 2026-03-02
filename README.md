# 🦊 FoxHunter

> **Passive Deauth Flood Detection for the WiFi Pineapple Pager**
> Author: FBG0x00 | Version: 1.0

---

## Overview

FoxHunter is a Terminal based passive deauthentication flood detection toolkit for the **WiFi Pineapple Pager** by Hak5.

The script does not perform any active attacks. FoxHunter **only listens**.

---

## Scripts

| Script | Version | Use Case |
|---|---|---|
| `FoxHunter.sh` | 1.0 | Terminal-based monitor via SSH |

---

## FoxHunter.sh

A full-featured deauth flood detector designed to be run over SSH. Captures packets passively, displays a live monitoring dashboard, and throws a full-screen alert when a flood is detected.

### Features

- Auto-detects monitor mode interface
- Live status dashboard with packet counts and alert history
- Full-screen terminal alert overlay on flood detection
- Top attacker MAC identification
- Timestamped event log saved to loot directory
- Audible beep alert on detection
- Clean shutdown with Ctrl+C
- Dependency check on startup

### Requirements

- WiFi Pineapple Pager (SSH access)
- Monitor mode interface (`wlan0mon` or equivalent)
- `tcpdump`, `iw`, `ip`, `awk`, `wc`, `date` (all pre-installed on Pager)

### Installation

- Download the FoxHunter.sh payload.
- SSH into your pager and navigate to the /mmc/root/payloads/alerts/deauth_flood_detected DIR then use mkdir FoxHunter to make a FoxHunter folder.
- Exit out of SSH
- Open your Terminal to Navigate to your Downloads DIR where the payload is usually located.
- Use "pwd" to view the location to the Downloads DIR. Example /home/user/Downloads.
- You should then be able to use the SCP command to move the payload to your pager easily like the example down below.
- or Copy and paste the script to your Pager via SSH which should be the easiest way to do it.

```
#!/bin/bash

scp /home/user/Downloads/FoxHunter.sh root@172.16.52.1:/mmc/root/payloads/alerts/deauth_flood_detected/FoxHunter/FoxHunter.sh
```

Make it executable:

- Inside SSH navigate to the DIR where the payload is located which is /mmc/root/payloads/alerts/deauth_flood_detected/Foxhunter.
- You should be able to then use the "chmod" command to make it into an executable like the example down below.
- To execute use ./FoxHunter.sh

```
#!/bin/bash

chmod +x FoxHunter.sh
```

### Configuration

Edit the variables at the top of the script before running:

```
#!/bin/bash

IFACE=""          # Leave blank to auto-detect, or set e.g. "wlan0mon"
THRESHOLD=50      # Deauth packets per window before alerting
WINDOW_SIZE=30    # Detection window in seconds
LOG_DIR="/mmc/root/loot/FoxHunter"   # Log directory (use /mmc/root/loot/ for SD card persistence)
ALERT_SOUND=true  # Audible beep on alert
MAX_LOG_LINES=500 # Max lines in packet log before trimming
```

> **Note on LOG_DIR:** If your Pager stores loot on the SD card, use `/mmc/root/loot/FoxHunter`. If you want temp-only storage (faster, lost on reboot), use `/tmp/FoxHunter`.

### Usage

```
#!/bin/bash

ssh root@172.16.52.1
bash /mmc/root/payloads/alerts/deauth_flood_detected/FoxHunter/FoxHunter.sh
```

FoxHunter will auto-detect your monitor interface, start capturing, and display the live dashboard. When a deauth flood exceeds the threshold, a full-screen alert interrupts the terminal. Press **Enter** to dismiss and return to monitoring.

Press **Ctrl+C** to stop. The event log is saved automatically.

### Log Files

```
$LOG_DIR/events.log          # Timestamped alert and info log
$LOG_DIR/deauth_packets.txt  # Raw tcpdump packet capture (trimmed automatically)
```

## Legal

FoxHunter is a **passive detection tool only**. It does not transmit any packets, perform any attacks, or interfere with any wireless networks.

Only deploy on networks you own or have explicit written permission to monitor.

---

## Credits

Built for the **WiFi Pineapple Pager** by Hak5.
Author: **FBG0x00**


