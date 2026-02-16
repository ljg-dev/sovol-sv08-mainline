# Sovol SV08 Mainline Notes

This repository is a personal log of how I mainlined Klipper on my Sovol SV08. It is not a step-by-step guide. I am not responsible for any damage, data loss, or bricked devices. Use everything here at your own risk.

## Index
0. [Read Rappetor's guide for preparations and alternative flashing methods](https://github.com/Rappetor/Sovol-SV08-Mainline?tab=readme-ov-file)
1. [Step 1 - Backup Stock eMMC](docs/1-backup-emmc/README.md)
2. [Step 2 - Install Latest Armbian on CB1 and Prepare OS](docs/2-install-latest-armbian/README.md)

## Scope
- Back up the stock eMMC
- Install Armbian on the CB1 and prepare the OS
- Hand off to a mainline Klipper guide for the remaining steps

## Assumptions
- You are comfortable with Linux CLI tools and recovery workflows
- You have an eMMC adapter/reader and a host computer
- You can attach HDMI and a keyboard for first boot

## Safety Notes
- Double-check device names before using `dd`, `fdisk`, or any disk utility
- Treat UUIDs, paths, and mount points in examples as placeholders

## References
- [Rappetor Sovol SV08 Mainline](https://github.com/Rappetor/Sovol-SV08-Mainline?tab=readme-ov-file)

## Credits
- Rappetor for the mainline guide and requirements list (see his README)
- Vlad for the procedure on latest Armbian
- michrech, cluless, and ss1gohan13 for answering questions throughout the process

## Notes
- This repository exists as a reference for a more up-to-date OS install flow and my own notes. Please rely on Rappetor's README for requirements and the broader guide.

## Why a Newer OS
- Security updates and long-term maintenance matter on networked devices
- Debian Bullseye is end-of-life, so it no longer receives updates
- Newer Klipper versions expect updated dependencies (for example, newer Python packages)
