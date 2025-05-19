# Automated SOC Components Setup Script

## Overview


<img width="615" alt="main_pic" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image1.png">

This script automates the setup of a comprehensive security monitoring environment, including a Security Information and Event Management (SIEM) system,Network-based Intrusion Detection System (NIDS) and Host-based Intrusion Detection System (HIDS) on a single machine. It streamlines the installation process, making it accessible to users with different levels of technical expertise.

**Note:** This script is intended to install all the components on a single machine, meaning the same box will have the SIEM, NIDS, and HIDS core components.

## Components

The script facilitates the installation of the following SOC components:

1. **SIEM (Security Information and Event Management):** This component combines Elasticsearch, Kibana, and Filebeat to provide a powerful platform for monitoring and analyzing security events in your environment. The SIEM setup includes Elasticsearch, Kibana and Filebeat version 7.17.13 as it is the compatible version to integrate with Wazuh manager version 4.5


   <img width="555" alt="siem_setup_1" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image2.png">

   

   <img width="918" alt="elasticsearch" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image4.jpg">


2. **NIDS (Network-based Intrusion Detection System):** Suricata, a high-performance NIDS, is configured to help protect your network from intrusions and suspicious activities.
**Note:** Suricata will monitor the local interface of the machine where it is installed. To monitor the entire network traffic, it should receive traffic from a TAP device or a SPAN port.

<img width="555" alt="Suricata_setup" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image6.png">

<img width="957" alt="suricata_dashboard" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image5.png">

3. **HIDS (Host-based Intrusion Detection System):** The script installs the Wazuh Manager, an open-source HIDS. It aids in monitoring, detecting, and responding to security threats on individual hosts. The setup includes the installation of Wazuh Manager version 4.5

   
<img width="555" alt="wazuh_setup" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image7.png">



<img width="929" alt="wazuh" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image3.jpg">

## System Requirements

Before running the script, please ensure that your system meets the following requirements:

- Ubuntu OS
- Minimum 4GB of RAM
- Minimum 20GB of free disk space

If your system doesn't meet these requirements, the script will issue a warning and allow you to proceed at your own risk.

## Usage

1. Clone this repository to your local machine:

   ```bash
   git clone https://github.com/Yassinoss03/SOC_automation_yk

2. Navigate to the repository's directory:
   ```bash
   cd setup_script
3. Make the setup_script.sh executable:
   ```bash
   chmod +x setup_script.sh
4. Execute the setup_script.sh:
   ```bash
   ./setup_script.sh
5. Follow the on-screen prompts to choose which components you want to install and continue with the setup.
   Post-Installation Steps
6. After successfully running the script and completing the NIDS (Suricata) setup, consider the following post-installation steps:

## Verify NIDS Logs: 
Check if logs are getting written to the /var/log/suricata/eve.json file. This is essential for monitoring network traffic.
Besides, you need to check from kibana if data is being displayed in Suricata Dashboard.

## Wazuh-Agent Installation: 
To complete the setup and ensure effective security monitoring, install Wazuh agents on Linux or Windows machines in your network. This allows you to ingest logs into the SIEM, enhancing your security monitoring capabilities.

## Warnings and Considerations
Data Backup: Before proceeding, it's advisable to backup your data, especially if you plan to run the script on a production system.

## Security Best Practices
After setting up the security components, consider following best practices for system hardening, firewall configurations, and securing sensitive data.

## Telegram Integration with Suricata 

Requirements:
• Telegram Bot Token
• Chat ID (group or user)

Creating the bot
1. To send Wazuh alerts to a Telegram chat, we need to create a bot first. To do this
we have to send a couple of messages to @BotFather. After starting the bot with
the /start command, we have to send the /newbot command to start creating the
bot, and we will choose the name of the bot, Suricata_bot

2. Next lets created the new bots to get alert messages suricata bot name
(Suricata_bot)noted:I have created this private only not in public >


<img width="615" alt="main_pic" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image10.png">


3. And deploy create the group name wazuh12 or any other name and also add the
bot inside tha group and make sure that when we add bot in group(before that
start the bot)


 <img width="443" alt="siem_setup_1" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image11.png">
 

4. Next navigations to (Get Telegram Chat ID) link : https://sean-
bradley.medium.com/get-telegram-chat-id-80b575520659) go to this
websites and copy paste the api which created by botfather: and make sure
that started the bots before copying api key in chat-id)


<img width="615" alt="main_pic" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image12.png">

5. Next lets configuration telegram alert and lets create the custom-telegram
and get messages and alert messages in telegram bot group which we have
created:
• Go to suricata  machine create the folder and  open with  nano
 /usr/local/bin/telegram-alert.sh inside folder we need to add chat id and bot token;


<img width="615" alt="main_pic" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image 13.png">



6. Make /usr/local/bin/telegram-alert.sh executable:
   ```bash
   chmod +x /usr/local/bin/telegram-alert.sh

7. Start the reading from fast.log :
   ```bash
   tail -F /var/log/suricata/fast.log | /usr/local/bin/telegram-alert.sh


8. Next lets configuration  autamatisation telegram alert and get messages and alert messages 
in telegram bot group which we have created:
• Go to suricata  machine create the folder and  open with  nano
 /etc/systemd/system/suricata-telegram.service inside folder we need to add the last command ;

<img width="615" alt="main_pic" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image 15.png">



9.Resultat :

<img width="615" alt="main_pic" src="https://github.com/Yassinoss03/SOC_automation_yk/blob/main/image 14.png">












   
