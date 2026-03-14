Raspberry Pi 5 Homelab NAS

A lightweight self-hosted homelab server built on a Raspberry Pi 5 (8GB) using NVMe SSD storage.
The goal of this project is to create a reliable personal infrastructure capable of running services such as private cloud storage, containerised applications, and secure remote access.

The system prioritises:

performance (NVMe storage)

reliability (moving OS off the SD card)

security (private VPN access)

expandability (dual-SSD architecture)

Hardware
Component	Model
Server	Raspberry Pi 5 (8GB RAM)
Storage	2 × Crucial CT1000P3PSSD8 1TB NVMe SSD
NVMe Adapter	MPS2280D PCIe Adapter
Boot Media (initial setup)	MicroSD Card
Architecture Overview

The homelab uses NVMe storage for the operating system and services, while secure remote access is provided through a private VPN network.

Internet »» Tailscale VPN »» Raspberry Pi 5 Server:                                                                                          
 • SSH administration
 • Docker containers
 • Nextcloud
 • Monitoring tools

All services are accessed through the VPN rather than being directly exposed to the public internet.

Storage Architecture

The system includes two NVMe SSDs.

Initially only one is used for the server, leaving the second drive available for future projects.

SSD1 (nvme0n1) – SYSTEM
├─ Raspberry Pi OS
├─ Docker
├─ Nextcloud
├─ Databases
└─ Server services

SSD2 (nvme1n1) – RESERVED
└─ Future projects / additional storage

This approach keeps the system simple while maintaining expansion capability.

Operating System

Raspberry Pi OS Lite (64-bit)

Reasons for this choice:

minimal overhead

stable and well supported

ideal for headless servers

good compatibility with container platforms

Initial Setup

After flashing Raspberry Pi OS Lite to the SD card and booting the system:

Update the system packages:

sudo apt update
sudo apt upgrade -y

Check connected storage devices:

lsblk

Example output:

NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
mmcblk0     179:0    0  58.4G  0 disk
├─mmcblk0p1 179:1    0   512M  0 part /boot/firmware
└─mmcblk0p2 179:2    0  57.9G  0 part /

nvme0n1     259:0    0 931.5G  0 disk
nvme1n1     259:1    0 931.5G  0 disk

Meaning:

mmcblk0 → SD card (current OS)

nvme0n1 → SSD1

nvme1n1 → SSD2

Migrating OS from SD Card to NVMe

Running server workloads from an SD card is not ideal due to limited performance and durability.

The system is migrated to NVMe using rpi-clone.

Install the cloning tool:

sudo apt install rpi-clone -y

Clone the system to the NVMe drive:

sudo rpi-clone nvme0n1

The cloning process:

partitions the SSD

copies the operating system

configures boot settings

After the process completes, reboot the system.

Verifying NVMe Boot

Confirm the system is running from the SSD:

lsblk

The root filesystem / should now appear on:

nvme0n1p2

instead of:

mmcblk0p2
Secure Remote Access (VPN)

Remote access to the homelab is provided using Tailscale, which creates a private encrypted network between devices.

This allows the server to be accessed securely from anywhere without opening ports on the router.

Tailscale is built on WireGuard and provides secure peer-to-peer connectivity.

Installing the VPN

Install Tailscale:

curl -fsSL https://tailscale.com/install.sh | sh

Start the VPN connection:

sudo tailscale up

After authentication, the server will join the private VPN network.

You can then connect from authorised devices.

Example SSH access:

ssh miguel@cloudserver

or using the Tailscale IP:

ssh miguel@100.x.x.x
Planned Services

This homelab will host:

Nextcloud (private cloud storage)

Docker containers

system monitoring tools

development environments
