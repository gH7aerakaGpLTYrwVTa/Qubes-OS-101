# Qubes OS 101

## Table of Contents
* [**1. Before You Proceed**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#before-you-proceed)
* [**2. Settings Up Qubes OS**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#setting-up-qubes-os)
* [**3. Check for Updates**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#check-for-template-upgrades) 
* [**4. VM Settings**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#vm-settings)
* [**5. Customize**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#customize)
* [**6. Password Management**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#password-management)
* [**7. VPN**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#vpn)
* [**8. Whonix**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#whonix)
* [**9. Multimedia VM**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#multimedia-vm)
* [**10. Disposable VMs**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#disposable-vms)
* [**11. Messenger**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#messenger)
* [**12. Tips and Tricks**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#tips-and-tricks)
* [**13. Bisq DEX**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#bisq-dex)
* [**14. Electrum**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#electrum)
* [**15. Trezor**](https://github.com/gH7aerakaGpLTYrwVTa/Qubes-OS-101/blob/master/README.md#trezor)

<br/>

## **Before You Proceed**
Please watch the video or read docs about basic function before using Qubes OS. I assume the reader is somewhat familiar with the command line, knows basic things about Qubes like the difference between a Template VM & Application VM, and understand the basics of some privacy tools like Tor.

<br/>

**Video:**

https://www.youtube.com/watch?v=Aghj8MyDF4I

<br/>

**Docs:**

https://www.qubes-os.org/doc/

Verify hash files and download Qubes `.iso` from:

```https://www.qubes-os.org/doc/installation-guide/```

<br/>

**Privacy Tools:**

https://www.privacytools.io/

https://prism-break.org/en/

Update all template VMs, whonix VMs, etc. before using them!

<br/>

**Open Source BIOS:**

https://github.com/merge/skulls

https://www.ministryofnodes.com.au/2020/02/17/a-journey-into-qubes-os/

https://web.archive.org/web/20200924050757/https://www.ministryofnodes.com.au/2020/02/17/a-journey-into-qubes-os/ (archive)

https://www.youtube.com/watch?v=2Y06x1f22B0

Optional, but this may be worth looking into depending on your setup!

<br/>

## **Setting Up Qubes OS**

During OS install leave all options default and enable updates over Tor if you wish. Select desired language/passwords/disk encryption(LUKS).

System may reboot a few times, do not remove usb.

Connect internet. Open main menu in top left corner and select System Tools, then select Qube Manager. Right click and select update for dom0 + all template VMs. Right click each template VM and make clean template VM clones as backups once updates are complete. Example name fedora-29-clean. If unsure about infected template VM, simply clone a clean template VM backup to start fresh.

Shutdown Qubes OS so any dom0 updates can finish, and reboot.

In top right corner of screen (toolbar) right click and open power manager settings (battery and plug symbol). Go to Display tab and turn power management off.

(Optional) Screensaver will lock the screen every 10 minutes which may be desired. If you wish to disable go to top left corner menu on desktop, select system tools, and select Screensaver. Click the Mode (dropdown) menu and choose disable.

In top left corner open the main menu. Select Terminal Emulator. This is the dom0 terminal. Install redshift in dom0:

```sudo qubes-dom0-update redshift```

```sudo redshift -O 4000```

```sudo redshift -x```

Add notes called REMINDERS.txt in all AppVMs to remind yourself to use Vault VM airgapped storage, dispVMs when needed, pgp encrypt, vpn as much as possible, keep regular backups of difficult configs, always update all password managers, and use tor where possible!

<br/>

**Setup mac address spoof:**

https://www.qubes-os.org/doc/anonymizing-your-mac-address/

https://github.com/QubesOS/qubes-issues/issues/3905

<br/>

## **Check for Template Upgrades**

Make sure that your template VMs are up to date and keep up with the latest annoucements

<br/>

**Upgrades, annoucements, and more:**

https://www.qubes-os.org/news/categories/#announcements

https://www.qubes-os.org/doc/templates/fedora/#upgrading

https://www.qubes-os.org/doc/templates/debian/#upgrading

https://www.qubes-os.org/doc/template/fedora/upgrade/#detailed-instructions-for-standard-fedora-templatevms

<br/>

**PROTIP:** the following command will help remove an old template VM that is installed by package manager run this command in dom0 terminal. For example, running this command in `dom0` terminal will allow you to remove an old `fedora-34` template VM:

`qvm-prefs fedora-34 installed_by_rpm false`

<br/>

## **USB Qube**

Take some time to learn about the USB qube named `sys-usb` and be aware of its function.

https://www.qubes-os.org/doc/usb-qubes/

https://www.qubes-os.org/doc/how-to-use-usb-devices/

<br/>

**PROTIP:** When updating your `sys-usb` qube to use a new template VM, the following command will help you not lose USB peripheral access by properly restarting it. For example, running this command in `dom0` terminal to switch `fedora-35` as the template VM:

`qvm-shutdown --wait sys-usb; qvm-prefs sys-usb template fedora-35;qvm-start sys-usb`

<br/>

## **Example Settings for Qubes** 

I think 2VCPU and 2gb RAM for things like very basic tasks. For the VM with mediacodecs and videostreaming 4VCPU and 4gb RAM.

All vpn vms should be 1 vcpu wtih 300/300 fixed ram (memory balance enabled is fine). Qubes uses a ton of RAM so make sure you have a proper setup.

*sys-net:* can stay at default settings.

*sys-firewall:* 1 vcpu - 450mb min / 450mb max RAM

*sys-whonix:* 1vcpu - 400mb min / 400mb max RAM

*password-manager:* 1vcpu - 300mb min / 300mb max RAM

*multimedia:* 4-6vcpu - 400mb min / 8000mb max RAM

*anon-whonix:* vcpu1 - 400mb min / 1000mb max RAM

*vault:* vcpu1 - 300mb min / 300mb max RAM

*whonix-ws-15-dvm:* vcpu2 - 400mb min / 2000mb max RAM

*fedora-32-dvm:* vcpu2 - 400mb min / 2000mb max RAM

<br/>

## **Customize** 

Get your Qubes OS looking good:

https://www.qubes-os.org/doc/i3/ and config file `~/.config/i3/config`

http://www.compiz.org/

https://www.qubes-os.org/doc/awesome/

https://www.qubes-os.org/doc/disposablevm-customization/#using-static-disposablevms-for-sys-

https://www.qubes-os.org/doc/disposablevm-customization/

<br/>

**Qubes OS Darkmode:**

https://www.qubes-os.org/doc/dark-theme/#dark-xcfe-in-dom0

Go to settings, under appearance, choose Adwaita-dark. You can also got to the fonts tab here and customize font/size.

Go back to settings and click Window Manager, and set any option that you prefer.

<br/>

**Icons:**

https://askubuntu.com/questions/95104/how-to-lock-desktop-icons-on-xfce

https://forum.xfce.org/viewtopic.php?id=7597

Adding +i or -i adds or takes away immutability. When the file is immutable the desktop icon positions cannot be modified on screen resize/system reboot.

`sudo chattr +i ~/.config/xfce4/desktop/icons*`

`sudo chattr -i ~/.config/xfce4/desktop/icons*`

<br/>

**Move Panel:**

Some do not want the system panel on the top of their screen. Right click it and go to panel -> panel preferences. Unlock the panel, then use the button on the far left side to drag and move it to the bottom. Change any other settings that you prefer.

Right click the workspaces on the panel (left of clock). Go to workspace settings and adjust to your preferences. 

<br/>

## **Password Management**

Always airgap the virtual machine you are using for password management. I simply clone the Qubes Vault VM which is already airgapped.

KeePassXC is a great open source password manager for linux. It should already be installed in any fedora-30 based AppVm. Simply open that Qube's settings, go to the Applications tab, and select Keepassxc to be added to the menu.

<br/>

## **VPN**

Setup Qubes-vpn-support software in a proxy VM. 

To have the ability to choose multiple geographic locations easily you may setup many VPN Proxy VMs. Be sure to select a VPN that has many locations (config files) available for download, or use multiple VPN providers. 

Configure all neccesary VMs to use VPN proxyVMs for networking by default. Press Alt + F3 and open Qube Manager by searching its name. You may need to have Fn lock enabled if using a Thinkpad T series. Right click the app VM you want to have VPN, such as the one named untrusted, and choose settings. Set the networking to your new VPN proxy VM. Apply and press ok.

**Qubes VPN Support:**
https://github.com/tasket/Qubes-vpn-support

<br/>

***Quick Deployment Script for Qubes VPN Support:***
1. Create AppVM Qube for VPN with option enabled to provide network services to other Qubes.

2. Go to new VPN Qube settings, services, and add vpn-handler-openvpn by clicking the + button.

3. Download Qubes-vpn-support and your .ovpn files, copy to new VPN Qube.

4. Make sure Qubes-vpn-support and .ovpn files are in $HOME directory on new VPN Qube.

5. Make sure the script (step #6 below) is in home folder and made executable:
 
`nano vpn-setup`

`sudo chmod +x vpn-setup`

6. Quick Deployment Script:

```
#!/bin/sh

printf "\nChecking if /rw/config/vpn exists...\n"
if [ -d /rw/config/vpn ]; then
    printf "\n Found it!\n"
else
    printf "\nNot found, creating dir!\n"
sudo mkdir /rw/config/vpn
fi
# Check if VPN config directory exists

sudo cp "$HOME"/${1} /rw/config/vpn/vpn-client.conf
# Copy user input .ovpn file to VPN config directory

printf "\nEnter random letters for username and password to skip prompt...\n"
cd ~/Qubes-vpn-support && sudo bash ./install
# It is important to enter random text here and not leave prompts blank

printf "\nModifying username and password for max lazy mode...\n"
sudo sed -i '2a VPNusernameGOEShere' /rw/config/vpn/userpassword.txt   # MODIFY THIS LINE WITH VPN USERNAME
sudo sed -i '3a VPNpasswordGOEShere' /rw/config/vpn/userpassword.txt   # MODIFY THIS LINE WITH VPN PASSWORD
sudo sed -i '1,2d' /rw/config/vpn/userpassword.txt                     # FOR NO PASSWORD MODE LEAVE PASSWORD BLANK DURING RANDOM LETTER ENTRY ABOVE

printf "\nNow restart VPN Qube to start VPN!\n"
```

7. Clone this new VPN AppVM many times and reuse this script!

8. Example script usage with a .ovpn file:

`./vpn-setup.sh sweden-brazil-01.protonvpn.net.udp.ovpn`

<br/>

**Mullvad VPN - Qubes OS:**
https://mullvad.net/it/help/qubes-os-4-and-mullvad-vpn/

<br/>

## **Whonix**

**Security, Privacy, Hardening, Etc:**

https://www.whonix.org/wiki

https://github.com/qubenix/qubes-whonix-bitcoin

https://prism-break.org/en/

https://github.com/tycrek/degoogle

<br/>

**Extras:**

https://www.whonix.org/wiki/AppArmor#Qubes_Users_Note

https://www.whonix.org/wiki/Whonix-Gateway_Security#Tor_Connection_Padding

<br/>

## **Multimedia VM**

Multimedia VM for things like Google chrome, vlc media player, spotify, etc.

I prefer Fedora rather than Debian for this.

https://www.qubes-os.org/doc/multimedia/

<br/>

**For quick Chrome install:**

`sudo nano /etc/yum.repos.d/google-chrome.repo`

<br/>

**Make enabled true by changing:**

`enabled=0` to `enabled=1`

Use Ctrl+O to save and Ctrl+X to exit nano text editor.

<br/>

**Install:**

`sudo dnf install google-chrome-stable`

Some users may want rpmfusion repository because it has some useful software. 

<br/>

**Enter these commands if you want rpmfusion:**

```sudo dnf config-manager --set-enabled rpmfusion-free rpmfusion-nonfree```

```sudo dnf upgrade --refresh```

When installing you will see all sha256checksums for the software, check that they match by using websites like:

https://rpmfusion.org/keys

(Optional) Resize disk image as needed and install cryptocurrency wallets in AppVMs as needed. 

(Optional) Resize app VMs or template VMs disk image as needed using `sudo df` to check on image size.

https://www.qubes-os.org/doc/resize-disk-image

<br/>

## **Disposable VMs**

On a fresh installation of Qubes, the default DVM Template is called fedora-XX-dvm (where XX is the Fedora version of the default TemplateVM). If you have included the Whonix option in your install, there will also be a whonix-ws-dvm DVM Template available for your use.

<br/>

**You can set any AppVM to have the ability to act as a DVM Template in dom0 with:**

```qvm-prefs <vmname> template_for_dispvms True```

The default system wide DVM Template can be changed with qubes-prefs default_dispvm. By combining the two, choosing Open in DisposableVM from inside an AppVM will open the document in a DisposableVM based on the default DVM Template you specified.

You can change this behaviour for individual VMs. 

In the Application Menu, open Qube Settings for the VM in question and go to the “Advanced” tab. Here you can edit the “Default DisposableVM” setting to specify which DVM Template will be used to launch DisposableVMs from that VM. 

<br/>

**This can also be changed from the command line with:**

```qvm-prefs <vmname> default_dispvm <dvmtemplatename>```

For example, anon-whonix has been set to use whonix-ws-dvm as its default_dispvm, instead of the system default. You can even set an AppVM that has also been configured as a DVM Template to use itself, so DisposableVMs launched from within the AppVM/DVM Template would inherit the same settings.

NetVM and firewall rules for DVM Templates can be set as they can for a normal VM. By default a DisposableVM will inherit the NetVM and firewall settings of the DVM Template on which it is based. This is a change in behaviour from R3.2, where DisposableVMs would inherit the settings of the AppVM from which they were launched. Therefore, launching a DisposableVM from an AppVM will result in it using the network/firewall settings of the DVM Template on which it is based. For example, if an AppVM uses sys-net as its NetVM, but the default system DisposableVM uses sys-whonix, any DisposableVM launched from this AppVM will have sys-whonix as its NetVM.

Warning: The opposite is also true. This means if you have changed anon-whonix’s default_dispvm to use the system default, and the system default DisposableVM uses sys-net, launching a DisposableVM from inside anon-whonix will result in the DisposableVM using sys-net.

A DisposableVM launched from the Start Menu inherits the NetVM and firewall settings of the DVM Template on which it is based. Note that changing the “NetVM” setting for the system default DVM Template does affect the NetVM of DisposableVMs launched from the Start Menu. Different DVM Templates with individual NetVM settings can be added to the Start Menu.

<br/>

**Important Notes:**

Some DVM Templates will automatically create a menu item to launch a DVM, if you do not see an entry and want to add one please use the command:

```qvm-features deb-dvm appmenus-dispvm 1```

<br/>

**To launch a DVM from the command line, in dom0 please type the following:**

```qvm-run --dispvm=NameOfDVM --service qubes.StartApp+NameOfApp```

<br/>

## **Messenger**

Make a standalone VM for your messengers. See VM settings above for VCPU and RAM info.

I prefer to intall `telegram-dekstop` on fedora using rpm fusion repo (info above):

<br/>

**Install using rpm fusion:**

```sudo dnf install telegram-desktop```

<br/>

**Other Info:**

https://keybase.io/docs/the_app/install_linux

https://snapcraft.io/install/telegram-desktop/fedora

https://snapcraft.io/docs/getting-started

https://www.addictivetips.com/ubuntu-linux-tips/how-to-use-and-install-snap-packages-on-linux/

A snap’s installed applications can be found under /snap/bin, and subsequently, often added to $PATH. This makes commands directly accessible from the command line.

<br/>

**For example, the command installed via the VLC snap is simply vlc:**

```which vlc```

```/snap/bin/vlc```

<br/>

**If executing a command directly doesn’t work, try prefixing it with the /snap/bin path:**

```/snap/bin/vlc```

Adding /snap/bin to your default $PATH makes running snaps that don’t automatically add themselves more convenient.

<br/>

**Snaps are updated automatically. However, to manually check for updates, use the following command:**

`sudo snap refresh vlc`

Finally, use https://www.qubes-os.org/doc/managing-appvm-shortcuts/ to get a #shortcut setup

<br/>

**telegram 256x256 icon path:**

```/var/lib/snapd/snap/telegram-desktop/1038/share/icons/hicolor/256x256/apps/telegram.png```

<br/>

## **Tips and Tricks**

**Nvidia GPU Drivers on Fedora:**

https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-fedora-32

<br/>

**Message of the day:**

https://forums.fedoraforum.org/showthread.php?255780-How-to-get-motd-to-display

<br/>

**Use this command in dom0 to monitor resources used by VMs:**

```xl top```

```sudo xl info | grep -i total_memory```

You may wonder you see sys-net-dm & sys-usb-dm in addition to sys-net & sys-usb VMs from the output of this command. I was able to find the following answer.

"Xen uses by default qemu for HVMs. But this increases the attack surface for dom0, so in Qubes qemu is started in a PV domain, which is called [domainname]-dm."

<br/>

**Troubleshooting signed git commits:**

https://github.com/pstadler/keybase-gpg-github/issues/24#issuecomment-340877348

https://github.com/keybase/keybase-issues/issues/1712#issuecomment-141226705

When trying to get setup with gpg + git I was getting error when trying to make signed commits.

<br/>

**Output:** 

```> error: gpg failed to sign the data```

```> fatal: failed to write commit object```

Found the 2 links above that explain to try testing command below. If this fails with folowing errors, then you will know gpg having a problem.

<br/>

**Run Command:**

```echo "test" | gpg --clearsign```

<br/>

**Output:**

```> gpg: signing failed: Inappropriate ioctl for device```

```> gpg: [stdin]: clear-sign failed: Inappropriate ioctl for device```

To get rid of the completely usless misleading "Inappropriate ioctl for device" error, you have to run following command.

<br/>

**Run Command:**

```export GPG_TTY=$(tty)```

https://gist.github.com/Joeviocoe/6c4dc0c283f6d6c5b1a3f5af8793292b

<br/>

<br/>

## **Bisq DEX**

**General Info:**

https://www.whonix.org/wiki/Bisq

https://wiki.ronindojo.io/Bisq

https://bisq.wiki/Running_on_HiDPI_screen

<br/>

**Run Bisq:**

```GDK_SCALE=1 /opt/Bisq/Bisq --torControlPort=9051 --torControlPassword=notrequired --socks5ProxyBtcAddress=127.0.0.1:9050 --useTorForBtc=true --daoActivated=false```

<br/>

## **Electrum**

Electrum is now in Whonix by default thanks to awesome devs.

I will leave this older electrum setup below for those that wish to learn.

To install Electrum on a new standalone VM, be sure it is based on whonix-ws-15 VM.

https://www.whonix.org/wiki/Electrum

First see the link above if Electrum version is current. It should be up to date. If not proceed with the manual installation below.

While it is usually strongly recommended to install software from the Debian repositories (usual method in link above), the latest available package could be too old and will not connect to public servers. This means Debian's official package manager (APT) cannot be used to install a working Electrum version.

The best option in this case is to install Electrum from the official website, although it is currently being attacked (see the notices section). The following instructions provide steps to verify the AppImage, but keep in mind the risks involved with manual software installation, particularly if the server infrastructure is under assault. 

https://www.whonix.org/wiki/Electrum/Manual_Installation

Do not run Electrum yet!

Next, obtain your .onion address from the electrs instance on your node if you have one or, or use a trusted node run by a friend/service.

Choose one of the two commands below to start your electrum wallet based on your Electrum setup.

<br/>

**Qubes Whonix start command (replace xxxx.onion):**

```electrum-appimage --oneserver --server XXXXX.onion:50001:t --proxy socks5:10.152.152.10:9111```

<br/>

**If you downloaded & verified .AppImage (manual setup) use this command (replace xxxx.onion):**

```./electrum-3.3.8-x86_64.AppImage --oneserver --server XXXXX.onion:50001:t --proxy socks5:10.152.152.10:9111```

<br/>

## **Trezor**
For hooking up a trezor to electrum in Qubes, you only need to add the udev rules from the link below into the standalone whonix VM you wish to use with your Trezor.

<br/>

**Udev Rules:**
https://wiki.trezor.io/Qubes_OS
