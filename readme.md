Build Firewall
==============
This script builds a firewall with a default DROP policy.

Optimised for Ubuntu (16.04) server.

All IPv6 traffic is dropped.

## Installation & Usage
1. Clone this repo (e.g. to `~/sysadmin`)
2. Copy `variables.sample` to `variable` in the same directory: `cp variables.sample variables`
2. Enter the local IP address (`$HOME_IP`) (to lock down pinging) in the `build-firewall` `variables` file
3. Enter the `SSH_PORT` in the `variables` file
2. Make `build-firewall` and `simple-firewall` executable
2. Create symlinks to `build-firewall` and `simple-firewall` from within your `$PATH`
3. Run `sudo build-firewall`

~~~sh
cd ~/sysadmin/firewall
sudo chmod +x build-firewall
sudo ln -s ~/sysadmin/firewall/build-firewall /usr/local/sbin/build-firewall
sudo chmod +x simple-firewall
sudo ln -s ~/sysadmin/firewall/simple-firewall /usr/local/sbin/simple-firewall
~~~

## Persistence
Note that firewall rules are held in memory - they won't persist across reboots.

Use `iptables-persistent` to load rules on boot.

**Important**: if you change rules, run `sudo dpkg-reconfigure iptables-persistent`.

## Notes
- `-o` refers to the output interface
- `-i` refers to the input interface
- `-p` specify protocol

## Resources
- [Iptables Man Page](https://linux.die.net/man/8/iptables)
- [Comprehensive set of rules, well commented](http://www.thegeekstuff.com/scripts/iptables-rules)
- [As above](https://crm.vpscheap.net/knowledgebase.php?action=displayarticle&id=29)
- [OUTPUT rules, implications for security](http://serverfault.com/a/433304)
- [Persistence!](http://dev-notes.eu/2016/08/persistent-iptables-rules-in-ubuntu-16-04-xenial-xerus/)
- [More examples of rules]( http://www.thegeekstuff.com/2011/06/iptables-rules-examples/)
- [Linode guide to server security]( https://www.linode.com/docs/security/securing-your-server#basic-iptables-rulesets-for-ipv4-and-ipv6)
- [Listing, deleting rules]( https://www.digitalocean.com/community/tutorials/how-to-list-and-delete-iptables-firewall-rules) - good description of flushing tables
- [Good example of a script based iptables "service"](https://thelowedown.wordpress.com/2008/07/03/iptables-how-to-use-the-limits-module/)
- [Uses a pair of scripts under `/etc/network` fo achieve persistence](http://kvz.io/blog/2007/07/28/block-brute-force-attacks-with-iptables/)
- [Good description of preventing DOS with iptables](http://blog.bodhizazen.net/linux/prevent-dos-with-iptables/)
- [Netfilter docs on Packet Filtering](http://www.netfilter.org/documentation/HOWTO/packet-filtering-HOWTO-7.html#ss7.3)
- [sport vs dport](http://stackoverflow.com/a/28945345/3590673)
