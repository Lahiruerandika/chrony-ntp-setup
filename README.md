# Setting Up an NTP Server and Client with Chrony

This repository provides step-by-step instructions and configuration files for setting up a Network Time Protocol (NTP) server and client using **Chrony**. Chrony is a versatile implementation of the NTP protocol, designed for systems with intermittent network connections or those that do not run continuously.

## 📌 Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)

---

## Overview

This project demonstrates how to:

- Set up a Linux machine as an NTP server using Chrony.
- Configure a client machine to synchronize time with the Chrony server.
- Validate synchronization using chrony tools and system utilities.

---

## Prerequisites

- Two Linux machines (e.g., CentOS, RHEL, Ubuntu, or Debian).
- Root or sudo access on both machines.
- Basic knowledge of the terminal and network configuration.

## 📘 Full Setup Guide

See the full setup instructions in [`NTP Server Setup.md`](NTP%20Server%20Setup.md):

- [Step 1: Configure the NTP Server](NTP%20Server%20Setup.md#step-1-configure-the-ntp-source-server-primary-server)
- [Step 2: Configure the Syncing Client](NTP%20Server%20Setup.md#step-2-configure-the-syncing-client-secondary-server)
- [Step 3: Testing & Troubleshooting](NTP%20Server%20Setup.md#step-3-testing--troubleshooting)
