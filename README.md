# Project: Pi-hole Ad-Blocker on Ubuntu Server with Hyper-V

This guide documents the step-by-step process of installing a Pi-hole server on an Ubuntu Server 24.04 LTS virtual machine using Windows 11 Hyper-V. The project involved creating a stable VM, installing the Linux operating system, and configuring Pi-hole for network-wide ad-blocking.

---

### ## 1. Prerequisites

* Windows 11 with Hyper-V enabled.
* An internet connection.
* [Ubuntu Server 24.04 LTS ISO file](https://ubuntu.com/download/server).

---

### ## 2. Hyper-V Virtual Machine Setup

The first step was to create a new virtual machine, carefully configured to ensure stable networking.

1.  **Delete Old Switches:** Any previous "External" or "Internal" switches that were causing issues were removed from the **Virtual Switch Manager**.
2.  **Create the VM:** A new Generation 2 VM was created in Hyper-V Manager with the following specifications:
    * **Name:** Ubuntu-Pihole
    * **Generation:** Generation 2
    * **Memory:** 2048 MB (2 GB)
    * **Network Adapter:** Connected to the **Default Switch**. This is crucial as it provides a reliable NAT-based internet connection.
    * **Virtual Hard Disk:** 30 GB
    * **Boot ISO:** The downloaded Ubuntu Server 24.04 LTS ISO file.
3.  **Disable Secure Boot:** Before starting, **Secure Boot** was disabled in the VM's **Settings > Security** tab to allow the Linux installer to boot correctly.

---

### ## 3. Ubuntu Server Installation

The Ubuntu Server installer provided a guided setup process.

1.  **Booting the Installer:** The VM was started, booting into the GNU GRUB menu. The default **"Try or Install Ubuntu Server"** was selected.
     <img width="1126" height="937" alt="3 1 Booting the Installer" src="https://github.com/user-attachments/assets/3de234c4-998a-42e5-b25b-87782af25483" />

2.  **Network Configuration:** The installer automatically detected the network connection from the Default Switch and received an IP address via DHCP. This configuration was accepted.
    <img width="1058" height="917" alt="3 2 Network Configuration  " src="https://github.com/user-attachments/assets/96c9dacf-44b2-4c5c-b149-2bb248ee7ee2" />


3.  **Storage Configuration:** The default guided storage layout, using the entire virtual disk, was selected and confirmed.
    <img width="1044" height="934" alt="3 3 Storage Configuration" src="https://github.com/user-attachments/assets/c664bd53-4964-46e6-bd13-b2aba62e5641" />


4.  **Profile Setup:** A user profile, including a server name, username, and password, was created. This is the primary login for the server.
    <img width="1105" height="904" alt="3 4 Profile Setup" src="https://github.com/user-attachments/assets/d6c05cbc-c8f9-4656-ba66-3c6ceca99c22" />


5.  **SSH Configuration:** The **"Install OpenSSH server"** option was selected to enable secure remote management.
    <img width="1161" height="941" alt="3 5 SSH Configuration" src="https://github.com/user-attachments/assets/7ca203cd-d280-47ce-9350-761268122f47" />


6.  **Server Snaps:** No additional server snaps were chosen. The default selection was accepted by selecting "Done".
    <img width="1094" height="894" alt="3 6 Server Snaps" src="https://github.com/user-attachments/assets/e21586ad-d89f-4e1f-9652-00096afc45b6" />


7.  **Installation and Reboot:** After these steps, the installer completed the setup, and the system was rebooted.

---

### ## 4. Pi-hole Installation

With the Ubuntu server running, the final step was to install Pi-hole.

1.  **Log In and Update:** Logged into the server with the previously created credentials and ran system updates:
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```
2.  **Run Pi-hole Installer:** The `curl` utility was installed, and the Pi-hole installation script was executed:
    ```bash
    sudo apt install curl -y
    curl -sSL [https://install.pi-hole.net](https://install.pi-hole.net) | sudo bash
    ```
  <img width="1132" height="936" alt="4 2 Run Pi-hole Installer" src="https://github.com/user-attachments/assets/16982a63-445a-4758-80a0-bb0bdc671554" />


3.  **Follow the Wizard:** The on-screen graphical installer was followed, accepting the default options for DNS provider, blocklists, and web interface installation.

4.  **Installation Complete:** The installer finished and displayed the IP address and the initial admin password.
    <img width="1117" height="926" alt="4 4 Installation Complete" src="https://github.com/user-attachments/assets/c1e12d3c-bdbb-4e16-b10c-a821e17209d6" />


5.  **Reset Password (if necessary):** For easier access, the admin password was immediately reset from the command line with a memorable one:
    ```bash
    pihole -a -p
    ```

---

### ## 5. Project Outcome & Access

The project was a complete success. The Pi-hole server is running and accessible.

1.  **Accessing the Dashboard:** The web admin dashboard was accessed by navigating to the Pi-hole's IP address in a web browser (e.g., `http://172.24.132.78/admin`).
    <img width="1900" height="1064" alt="5 1 Accessing the Dashboard" src="https://github.com/user-attachments/assets/f543fa5a-34a9-48ae-bf09-b105c0c9fdbf" />


2.  **Final Result:** After logging in with the new password, the fully functional Pi-hole dashboard was displayed, ready to start blocking ads.
    <img width="1885" height="1060" alt="5 2 Final Result" src="https://github.com/user-attachments/assets/687ed3ef-c6e2-4fe8-ac56-88000d67e551" />

