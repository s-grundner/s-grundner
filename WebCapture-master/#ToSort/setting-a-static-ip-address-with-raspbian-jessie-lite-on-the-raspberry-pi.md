# Setting a Static IP address with Raspbian Jessie Lite on the Raspberry Pi

_Captured: 2017-05-21 at 10:51 from [www.jeffgeerling.com](https://www.jeffgeerling.com/blog/2016/setting-static-ip-address-raspbian-jessie-lite-on-raspberry-pi)_

In the midst of my work upgrading the [Raspberry Pi Dramble](http://www.pidramble.com/) to Raspbian Jessie Lite, I noticed one of the basic components of the architecture--static IP addresses for all the Raspberry Pis--was not working correctly anymore. My Ansible playbooks configured the `/etc/network/interfaces` file correctly, so it would define a static IP address for the `eth0` interface (the built-in Ethernet port on the Pi):

`auto lo  
  
iface lo inet loopback  
  
iface eth0 inet static  
  address 10.0.1.60/24  
  netmask 255.255.255.0  
  gateway 10.0.1.1  
  dns-nameservers 8.8.8.8 8.8.4.4  
  
allow-hotplug wlan0  
iface wlan0 inet manual  
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf  
iface default inet dhcp`

In the past, with Raspbian Wheezy, everything worked fine, and the Pi would (after a reboot) use the static IP address `10.0.1.60`.

In Raspbian Jessie Lite, there is a little additional configuration you need to provide for [dhcpcd](https://wiki.archlinux.org/index.php/dhcpcd), since Raspbian uses `dhcpcd5` by default. If you want, you could disable/uninstall `dhcpcd5` entirely, but it's simpler to provide the correct static IP configuration in dhcpcd's configuration file. In my case, I edited `/etc/dhcpcd.conf`, and put the following inside, after the rest of the configuration:

After rebooting the Raspberry Pi, the static IP address configuration worked just like it did with Wheezy. Another note; you can also delete the persistent dhcp lease info by removing the following files:

  * `/var/lib/dhcp/dhclient.leases`
  * `/var/lib/dhcpcd5/dhcpcd-eth0.lease`

For the Dramble, I made all the above changes to the Ansible playbook that configures Pi networking in [this commit](https://github.com/geerlingguy/raspberry-pi-dramble/commit/11dfedc49ab70869151b27bb1124dc5b973d5f51).

## More resources
