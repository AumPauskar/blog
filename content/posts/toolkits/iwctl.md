+++
title = 'iwctl'
date = 2026-08-29T06:55:32Z
tags = ["networking", "linux"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A minimal document on iwctl working"
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/blob/main/content"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# IWCTL
`iwctl` is the interactive command-line interface for `iwd` (iNet wireless daemon), common on Arch Linux and minimal Linux setups.

## 1. Quick Interactive Shell

Launch the interactive prompt to auto-complete commands and device names:

```bash
iwctl

```

*(Type `exit` or press `Ctrl+D` to leave at any time.)*

---

## 2. Connect to Wi-Fi (Step-by-Step)

If running directly from your standard terminal prompt without entering the shell:

1. Find your Wi-Fi device name (usually `wlan0`):
```bash
iwctl device list

```


2. Turn on the Wi-Fi adapter (if powered off):
```bash
iwctl adapter phy0 set-property Powered on

```


3. Scan for available networks:
```bash
iwctl station wlan0 scan

```


4. List scanned networks**:
```bash
iwctl station wlan0 get-networks

```


5. Connect to a network:
```bash
iwctl station wlan0 connect "Your-SSID-Name"

```


*You will be prompted for the passphrase if required.*

---

## 3. Essential Management Commands

| Action | Command |
| --- | --- |
| **Check Connection Status** | `iwctl station wlan0 show` |
| **Disconnect** | `iwctl station wlan0 disconnect` |
| **List Saved Networks** | `iwctl known-networks list` |
| **Forget a Saved Network** | `iwctl known-networks "SSID-Name" forget` |

---

> **Note:** `iwctl` only handles the Wi-Fi association. If your network doesn't assign an IP address automatically, ensure a DHCP client like `systemd-networkd` or `dhcpcd` is active.