<h1 align="center">Home-Lab-Setup</h1>

<br>

## Objective
To build a secure, segmented virtual lab that simulates an enterprise network using pfSense for network segmentation and Wazuh as a centralized SIEM for comprehensive log collection and security monitoring across multiple operating systems.

<br>

## Skills Learned

- Setting up virtual networks and machines in VirtualBox
- Installing and configuring a firewall using pfSense
- Installing and updating Kali Linux, Ubuntu Server, and Windows 10
- Troubleshooting Linux package and driver issues
- Deploying and managing Wazuh SIEM
- Connecting and monitoring Windows and Linux agents with Wazuh
- Testing and verifying security event monitoring

<br>

## Tools Used

- **Oracle VirtualBox:** Virtual machine management
- **pfSense:** Open-source firewall and router
- **Kali Linux:** Security testing and monitored endpoint
- **Ubuntu Server:** Wazuh SIEM host
- **Windows 10:** Monitored endpoint
- **Wazuh:** Security Information and Event Management
- **Oh My Zsh & Powerlevel10k:** Shell improvements for Kali
- **VirtualBox Guest Additions:** Enhanced VM integration

<br>

## Step-by-Step Walkthrough

### Step 1: Prepare Your Virtual Lab

- Installed Oracle VirtualBox.
- Downloaded ISO files for pfSense, Kali Linux, Ubuntu Server, and Windows 10.

<br>

### Step 2: Set Up pfSense Firewall

- Created a pfSense VM with two network adapters (NAT and internal).
- Installed pfSense and configured the internal "labnetwork" for network segmentation.

<br>

### Step 3: Install and Configure Kali Linux

- Created a Kali Linux VM connected to the internal "labnetwork."
- After installation, ran into an error when trying to update Kali because no APT data sources were configured. The system displayed an error message about missing APT sources.
- Discovered that the `/etc/apt/sources.list` file was empty or incorrect, which prevented package updates and installations.
- Resolved this issue by adding the official Kali rolling repository to the sources list, then performed a full update and upgrade of the system.
    - Here is a screenshot of the APT fix:<br>
      <img width="400" height="275" alt="kaliapt" src="https://github.com/user-attachments/assets/21d3abc0-a314-4122-b11f-f8535c1a12f6" />
- Initially had trouble installing build tools and kernel headers for VirtualBox Guest Additions, as some packages could not be found.
- Fixed this by installing the correct headers and then successfully installing VirtualBox Guest Additions after a reboot.
- Customized Kali with additional tools and improved the shell experience using Oh My Zsh and Powerlevel10k.

<br>

### Step 4: Add Windows 10 and Ubuntu Server

- Set up a Windows 10 VM for endpoint monitoring and testing.
- Set up an Ubuntu Server VM, enabled OpenSSH for remote access, and updated the system.
- Installed Wazuh SIEM on Ubuntu Server.
- Accessed the Wazuh dashboard from the Windows 10 VM browser to verify setup.

<br>

### Step 5: Deploy Wazuh Agents and Test Monitoring

- Installed the Wazuh agent on both Windows 10 and Kali Linux virtual machines.
- Verified that both agents successfully connected to the Wazuh server.
- Tested the monitoring setup by:
  - Logging in with a fake user on Windows to generate a failed login event.
  - Attempting a failed SSH login on Kali Linux.
- Confirmed that both security events appeared in the Wazuh dashboard:
    - Windows 10 event as seen in the Wazuh dashboard:<br>
     <img width="786" height="134" alt="win10wazuhtest" src="https://github.com/user-attachments/assets/d98e9b80-9fcb-4433-9a47-c2e2b65f994b" /><br>
    - Kali Linux event as seen in the Wazuh dashboard:<br>
     <img width="801" height="263" alt="kaliwazuhtest" src="https://github.com/user-attachments/assets/e4637001-f861-4d58-ab50-ff82d958b831" /><br>

