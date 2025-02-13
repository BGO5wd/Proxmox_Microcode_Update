Install: 

add the firmware repo 

echo "deb http://deb.debian.org/debian/ unstable non-free-firmware" > /etc/apt/sources.list.d/debian-unstable.list

priorize the intel or amd (or both) packages and lowest priority to all other packages in 

/etc/apt/preferences.d/unstable-repo 

# lower the priority of all packages in the unstable repository
Package: *
Pin: release o=Debian,a=unstable
Pin-Priority: 10

# allow upgrading microcode from the unstable repository
Package: intel-microcode
Pin: release o=Debian,a=unstable
Pin-Priority: 500
# just leave a blank line or comment here
Package: amd64-microcode
Pin: release o=Debian,a=unstable
Pin-Priority: 500


check if anything unwanted wants to upgrade from unstable with 
apt update && apt list --upgradable


install needed microcode

# Intel CPU
apt install intel-microcode
# AMD CPU
apt install amd64-microcode


and reboot

check journalctl for applied microcodepatch

journalctl -k --grep="Updated early from"
