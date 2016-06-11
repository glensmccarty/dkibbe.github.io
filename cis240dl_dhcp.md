# The DHCP Process

### Preparation

Boot into CerntOS 7 minimal

## Network Configuration Scripts

Interfaces are configured throught scrips located in `/etc/sysconfig/network-scripts/`.
Use `ip addr show` to list network interfaces.

## Release the Current Address

### Edit the Network Script

Comment out the **BOOTPROTO** line in the appropriate and change the **ONBOOT** line to "no" in the script to disable networking on boot. Reboot the system.

## Bring Up the Network

After rebooting the system test that networking does not exist.

### Testing

1. `ping -c4 google.com` does not succeed.
2. The `ip addr show` command does not show an IP address for the interface.
3. The `ip r` command does not return a route.

DHCP to te Rescue

Use the DHCP client to bring up the network interface.

	# dhclient -r

Test the network again and you will see that you have an IP address and can ping Google because a route exists.

## Request a New Address

	# dhclient -v
DHCP will ask for a new lease half way and then again at 7/8th if not received.

## Configure a Static IP Address

CentOS 7 comes with NetworkManager install. You'll use that to configure a static IP address for the Network Interface Card (NIC).

	# nmtui edit

![NetworkManager TUI](http://dennisk.fastmail.net/gallery/nm-edit-1.png)

1. Use `nmtui` to set a static IP address.
2. Change the hostname
3. Set name servers to Google's public name servers.

## Resources

 - [dhclient man page](http://linux.die.net/man/8/dhclient)


----------


> Written with [StackEdit](https://stackedit.io/).