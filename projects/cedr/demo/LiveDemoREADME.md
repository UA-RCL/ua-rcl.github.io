---
title: Demo Reproduction Guide
style: /_styles/presentations/generic_tutorials/custom.css
---

# CEDR Live Demo Reproduction Guide

This README describes how to reproduce the CEDR live demonstration using an **AUP-ZU3 FPGA board** and a **Linux host machine**.

The demo uses a direct local network connection between the host and the AUP-ZU3. The default configuration assumes:

- **Host IP:** `192.168.10.1`
- **AUP-ZU3 IP:** `192.168.10.2`
- **CEDR TCP port:** `5001`
- **Dashboard:** `http://127.0.0.1:8050`

All files required for the demo are available in the following read-only Google Drive folder:

<a href="https://drive.google.com/drive/folders/1YlDGz3caBvI6kMCsgK_YPf2T1GQhaJJa?usp=sharing"
       target="_blank"
       rel="noopener noreferrer">
      CEDR Live Demo Files
</a>

---

# Part 0 — Prerequisites

## 1. Required Hardware and Software

### Hardware

- AUP-ZU3 FPGA board
- SD card for the AUP-ZU3
- Linux host computer
- Ethernet cable for a direct host-to-board connection

### Host Software

The host should have:

- Python 3
- `pip`
- A modern web browser
- `scp` / SSH utilities

The dashboard script requires the following Python packages:

```bash
python3 -m pip install dash pandas plotly
```

Optionally, you can install them inside a Python virtual environment:

```bash
python3 -m venv cedr-demo-env
source cedr-demo-env/bin/activate
python3 -m pip install --upgrade pip
python3 -m pip install dash pandas plotly
```

---

## 2. Download the Demo Files

Open the Google Drive folder:

<a href="https://drive.google.com/drive/folders/1YlDGz3caBvI6kMCsgK_YPf2T1GQhaJJa?usp=sharing"
       target="_blank"
       rel="noopener noreferrer">
      CEDR Live Demo Files
</a>

The provided files are organized into the following main groups:

- **SD Card files** — image/files used to boot the AUP-ZU3
- **Board_Files** — CEDR binaries, configuration files, and workloads used on the AUP-ZU3
- **Host_Script** — Python dashboard script and its supporting files

Download the required files before continuing.

---

# Part I — AUP-ZU3 Setup

## Prepare the AUP-ZU3 Board

Download the provided SD card image/files from the Google Drive folder.

Use your preferred SD card imaging tool to write the provided image to the SD card.

After the image has been written:

1. Insert the SD card into the AUP-ZU3.
2. Power on the board.
3. Wait for the board to finish booting.
4. Connect the Ethernet adapter to the AUP-ZU3 board.
5. Configure the Ethernet adapter on the AUP-ZU3 with the following IP address:

   ```bash
   sudo ip link set dev <device_name> up
   sudo ip addr add 192.168.10.2/24 dev <device_name>
   ```

   Replace `<device_name>` with the Ethernet interface connected to the host. You can identify the interface using the `ip link` command on the board. The interface that appears after connecting the Ethernet adapter is the one to use.

6. Verify the configuration:

   ```bash
   ip addr show dev <device_name>
   ```

The AUP-ZU3 should now be configured to use:

```text
192.168.10.2
```

---

# Part II — Host Network Setup

## Configure the Host Ethernet Interface

First, identify the Ethernet interface connected to the AUP-ZU3:

```bash
ip link
```

Typical interface names may look like:

```text
eth0
enp3s0
enx001122334455
```

Replace `<device_name>` in the commands below with the correct interface.

Bring the interface up:

```bash
sudo ip link set dev <device_name> up
```

Assign the host IP address:

```bash
sudo ip addr add 192.168.10.1/24 dev <device_name>
```

The demo expects the following network configuration:

| Device | IP Address |
| --- | --- |
| Host | `192.168.10.1` |
| AUP-ZU3 | `192.168.10.2` |

You can verify the host configuration with:

```bash
ip addr show dev <device_name>
```

Finally, verify that the board is reachable:

```bash
ping 192.168.10.2
```

You should receive replies from the AUP-ZU3 before continuing.

> **Note:** The provided scripts and binaries assume these IP addresses by default. If different addresses are used, the corresponding host and board configuration must also be updated.

---

# Part III — Copy the Board Files

## Copy `Board_Files` to the AUP-ZU3

From the host machine, navigate to the location where the Google Drive files were downloaded.

Copy the contents of `Board_Files` to the board:

```bash
scp -r Board_Files/* petalinux@192.168.10.2:/home/petalinux/
```

Enter the AUP-ZU3 user password when prompted.

After the transfer completes, SSH into the board:

```bash
ssh petalinux@192.168.10.2
```

Verify that the files are present:

```bash
ls
```

If necessary, make the CEDR binary executable:

```bash
chmod +x cedr
```

---

# Part IV — Start the Host Dashboard

## 1. Prepare the Host Script

Download the complete `Host_Script` folder from the Google Drive folder.

Keep the files together. In particular, the dashboard expects its image files inside an `assets` directory located next to the Python script.

A typical layout should look similar to:

```text
Host_Script/
├── <dashboard_script>.py
├── jetson-demo/
│   ├── api_trace.csv
│   └── power_trace.csv
├── assets/
│   ├── AUP-ZU3.png
│   ├── Jetson.png
│   ├── UA-logo.png
│   ├── RCL-logo.png
│   └── AMD-logo.png
└── ...
```

Navigate to the host script directory:

```bash
cd Host_Script
```

Run the dashboard:

```bash
python3 tcp-gantt-workload.py
```

The script starts:

- a TCP server used to communicate with CEDR using port `5001`, and
- a Dash web application on port `8050`.

---

## 2. Open the Dashboard

Once the Python script is running, open a browser on the host machine and navigate to:

```text
http://127.0.0.1:8050
```

You can also use:

```text
http://localhost:8050
```

For the best demo layout, press `F11` on the browser to place the browser in full-screen mode.

At this point, the dashboard may show that the AUP-ZU3 is not yet connected. This is expected until CEDR is started on the board.

---

# Part V — Start CEDR on the AUP-ZU3

## Run CEDR

On the AUP-ZU3, navigate to the directory containing the copied board files. If the contents of `Board_Files` were copied directly into `/home/petalinux`, use:

```bash
cd ~
```

Start CEDR with:

```bash
sudo ./cedr -c ./daemon_config-light.json -l NONE
```

After CEDR starts, the dashboard on the host should indicate that the board is connected.

---

# Part VI — Run the Live Demo

## 1. Start a Workload

Once both the dashboard and CEDR are running:

1. Return to the browser dashboard.
2. Verify that the AUP-ZU3 shows as connected.
3. Press the workload start button in the dashboard.
4. Observe task execution in the live Gantt chart and the associated performance information.

---

## 2. Experiment with Scheduling Policies

The dashboard allows the scheduling policy to be changed while using the demo.

For example, experiment with:

- **Round Robin**
- **EFT — Earliest Finish Time**
- **ETF — Earliest Time to Finish**
- **MET — Minimum Execution Time**

Changing the scheduler allows you to observe how task placement changes across the available CPUs and FPGA accelerators.

---

## 3. Experiment with Resource Availability

The dashboard also allows the active resource configuration to be modified.

For example:

1. Start with all CPU, FFT, and ZIP resources enabled.
2. Reduce the number of available FFT or ZIP accelerators.
3. Disable one or more accelerator types.
4. Observe how CEDR dynamically adapts task placement to the available resources.

The resource pool visualization indicates which resources are currently enabled or disabled.

---

# Default Demo Configuration

| Parameter | Default |
| --- | --- |
| Host IP | `192.168.10.1` |
| AUP-ZU3 IP | `192.168.10.2` |
| TCP Port | `5001` |
| Dash Port | `8050` |
| Dashboard URL | `http://127.0.0.1:8050` |
| AUP-ZU3 User | `petalinux` |
| CEDR Config | `daemon_config-light.json` |

---

# Demo Files

All files used by this demonstration are available here:

<a href="https://drive.google.com/drive/folders/1YlDGz3caBvI6kMCsgK_YPf2T1GQhaJJa?usp=sharing"
       target="_blank"
       rel="noopener noreferrer">
      CEDR Live Demo Files
</a>
