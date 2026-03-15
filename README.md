# Raspberry Pi 5 Homelab NAS

A lightweight self-hosted homelab server built on a Raspberry Pi 5 (8GB) using NVMe SSD storage.
The goal of this project is to create a reliable personal infrastructure capable of running services such as private cloud storage, containerised applications, and secure remote access.

## Goal: 
The goal of this project is to build a reliable, secure, and high‑performance personal homelab using the Raspberry Pi 5 as a compact yet capable server platform.

 • Private cloud storage for personal files and backups                                                                                                                    
 • Containerised application hosting using Docker                                                                                                                    
 • Secure remote access through a VPN                                                                                                                    
 • A modular foundation that can grow with additional services, storage, and automation

## The system prioritises:

 • performance                                                                                                                                                                                              
 • reliability                                                                                                                                                                                              
 • security                                                                                                                                                                                              
 • expandability                                                                                                                                                                                              

## Hardware:                                                                                                                                                                                              

 • Raspberry Pi 5 8GB RAM                                                                                                                                                                                               
 • Storage	2x Crucial CT1000P3PSSD8 1TB NVMe SSD                                                                                                                                                                                              
 • NVMe Adapter	MPS2280D PCIe Adapter                                                                                                                                                                                              
 • MicroSD Card                                                                                                                                                                                              

## Architecture Overview                                                                                                                                                                                              

The homelab uses NVMe storage for the operating system and services, while secure remote access is provided through a private VPN network.

Internet                                                                                                                       
    │                                                                                                                       
    │                                                                                                                       
Tailscale VPN                                                                                                                       
    │                                                                                                                       
    ▼                                                                                                                       
Raspberry Pi 5 Server                                                                                                                       
│                                                                                                                       
├─ SSH administration                                                                                                                       
├─ Docker containers                                                                                                                       
├─ Nextcloud                                                                                                                       
├─ Monitoring tools                                                                                                                       
└─ Future services                                                                                                                       

All services are accessed through the VPN rather than being directly exposed to the public internet.

## Storage Architecture

The system includes two NVMe SSDs.

Initially only one is used for the server, leaving the second drive available for future projects.

SSD1 (nvme0n1) – SYSTEM                                                                                                                       
├─ Raspberry Pi OS                                                                                                                       
├─ Docker                                                                                                                       
└─ Nextcloud                                                                                                                       

This approach keeps the system simple while maintaining expansion capability.

## Operating System: Raspberry Pi OS Lite (64-bit)
                                                                                                                   
 • minimal overhead                                                                                                                     
 • stable and well supported                                                                                                                     
 • ideal for headless servers                                                                                                                     
 • good compatibility with container platforms                                                                                                                     
