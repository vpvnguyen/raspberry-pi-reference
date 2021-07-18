## Setup

- Download 64-bit image and unzip: https://dietpi.com/downloads/images/DietPi_RPi-ARMv8-Buster.7z
- Reformat and install via Raspberry Pi Imager
- Edit `./dietpi.txt` for custom configurations before start up
- SSH server Dropbear is installed and enabled by default on DietPi,
- Plug micro sd into pi and start up
  hostname: DietPi
  login: root
  pass: dietpi
- Change password: `passwd` or `dietpi-config` > Security Options
- `dietpi-software` or `dietpi-launcher` > DietPi-Software to install optimised software

# dietpi-device_manager

## DietPi configuration

- Configure various system settings, from display / audio / network to auto start options.
- Run `dietpi-config`.

## Configure OpenVPN

- Set router port forwarding:  
  TCP 443  
  TCP 943  
  UDP 1194
- Access micro sd card and edit file `./boot/DietPi_OpenVPN_Client.ovpn`
- Change the target domain/IP address  
  Examples for changing mywebsite.com. e.g.:

  remote MySuperDooperWebsite.com 1194  
  remote 81.252.0.1 1194

- For security reasons, please remove those client connection files after they have been deployed on the client system!

- Run `dietpi-vpn` to setup
- DietPi-VPN comes with an optional killswitch that will shut off your internet in the case of you losing your connection to the VPN sever.
- This will still allow access from your LAN and allow you to fix any problems using SSH, if needed.

## Start LXDE Desktop

- After installation, desktop can be run by typing `startx`
- To start different programs when the system boots, run from the command line: `dietpi-autostart`

## Configure VNC Server

### Basics

- By default DietPi will start a virtual VNC session on boot at screen `:1` for user `root`.
- The screen index can be changed via `SOFTWARE_VNCSERVER_DISPLAY_INDEX` in `/boot/dietpi.txt`.
- Logs can be viewed via `journalctl -t Xvnc:1 -t vncserver` and in `/root/.vnc/`.
- When you logout (instead of only closing the VNC Viewer window), the session will exit.
- Restart via `systemctl restart vncserver`.

### Shared desktop

- If you set `SOFTWARE_VNCSERVER_SHARE_DESKTOP=1` in `/boot/dietpi.txt`
  or select desktop auto login via `dietpi-autostart` (index 2),
  RealVNC server will be started on boot in shared desktop mode, attaching to the first found local desktop session.
- Check the service status via `systemctl status vncserver-x11-serviced`.
- Check all logs via `journalctl -u vncserver-x11-serviced`.

## Configure NFS shared file systems

- Allow permissions to <IP_ADDRESS_OF_DIETPI>:2049

## DietPi backup (backup/restore)

- Fully backups DietPi setup. It also includes the restore capability from an already made DietPi backup.

- DietPi-Backup allows you to Backup and Restore your DietPi system. Same effect as Windows system restore. A snapshot of the system that you can restore at any time.
- You can also customize which files/folders are included and excluded through the GUI.

- If you have broken your system, or want to reset your system to an earlier date, this can all be done with DietPi-Backup. Just make sure you create a backup first.
- Run `dietpi-backup`.
