# Headtracking on Linux

A short meta explanation on how to use Opentrack to achieve headtracking with games running on Proton. 
This write-up is based on:
opentrack/opentrack#2109 (comment)

---

## Overview

The current headtracking situation (early 2026) on Linux is confusing. This write-up aims to help you get Opentrack headtracking working in most games running under Steam’s Proton.

---

## Setup Instructions

### 1. Install opentrack-launcher

Get: https://github.com/markx86/opentrack-launcher
Follow the instructions provided there.

This tool launches a Windows Opentrack portable executable via Proton (tested with Proton 10.0).

---

### 2. First Launch Behavior

After installation, launching Opentrack will fail. This is expected due to a dependency issue with Qt6 DLLs in the most current version of Opentrack.

---

### 3. Verify Installation

Ensure the following directory exists:

```bash
~/.local/share/opentrack-launcher/scripts
```

This indicates a successful installation.

**Note:** The process can take a couple of minutes, even if the launch crashes.

---

### 4. Clean Installation Directory

Delete the contents of:

```bash
~/.local/share/opentrack-launcher/install
```

---

### 5. Download Compatible Opentrack Version

Download the 32-bit portable Opentrack 2024.1.1 from:
https://github.com/opentrack/opentrack/releases/tag/opentrack-2024.1.1

---

### 6. Extract Files

Extract the portable version into:

```bash
~/.local/share/opentrack-launcher/install
```

---

### 7. Launch

The launch should now be successful. `Opentrack.exe` and your game should both start.

---

## Native Linux Opentrack

You also need the native Linux version of Opentrack.

* Option 1: Use an AppImage
* Option 2 (recommended): Compile from source

Instructions:
https://github.com/opentrack/opentrack/wiki/Building-on-Linux

It is recommended to automate this process to keep up with dependencies.

---

## Running the Setup

1. Launch your game from Steam using the provided parameters (see below).
2. This will also launch the portable `Opentrack.exe` via opentrack-launcher.
3. Start your native Linux Opentrack.

---

## Configuration

### Native Linux Opentrack

* **Input:** NeuralNet Tracker (or any working alternative)
* **Output:** UDP over network

  * Address: `127.0.0.1`
  * Port: `4242`

Make sure this port is allowed in your firewall (ufw or similar), restricted to localhost.

---

### Portable Opentrack.exe

* **Input:** UDP over network

  * Address: `127.0.0.1`
  * Port: `4242`

* **Output:** Freetrack 2.0 Enhanced

  * Ensure the correct interface option is selected if headtracking input is buggy.

---

## Usage

* Press **Start** in both Opentrack instances.
* Use your head to look around.

---

## Steam Launch Parameters

```bash
~/.local/bin/opentrack-launcher %command%
```

If using gamemode (this way the Opentrack.exe also benefits from gamemode):

```bash
gamemoderun ~/.local/bin/opentrack-launcher %command%
```


---

## Closing Notes

After closing the game and `Opentrack.exe`:

* Verify the process has fully exited in Steam (PLAY/STOP button).
* If necessary, press **Close** to ensure proper savegame syncing.

---

## Alternatives

* Some games support UDP input directly. In that case, the native Linux Opentrack alone is sufficient.
* If a game does not support UDP input:

  * Consider contacting the developers.
  * If the game is end-of-life, check the modding community.

---

## In case this write-up breaks

Please contact me, it will also break for me and i'd rather fix the issue before i run into it. 

