# ipfw_nat 

People who use the ipfw nat will specify firewall_nat_* in rc.conf like this:

	firewall_nat_enable="YES"
	firewall_nat_interface="em0"
	firewall_nat_flags="deny_in reset same_ports unreg_only redirect_port tcp 192.168.1.1:25 25 ..."

However, if there are many redirect_port rules, the 
firewall_nat_flags will become longer and it will be troublesome to change a
bit. On maintainance, more than anything, it is difficult to be found
troubles in which occurs. So I tried to change the rc.firewall to manage the
rules as a separate file. On new configuration:

	firewall_nat_enable="YES"
	firewall_nat_interface="em0"
	firewall_nat_flags="deny_in reset same_ports unreg_only"
	firewall_nat_rules="/etc/ipfw_nat.rules"

Where /etc/ipfw_nat.rules is for example:

	redirect_port	tcp 192.168.1.1:25	25
	redirect_port	tcp 192.168.1.2:80	80
	redirect_port	tcp 192.168.1.3:21	21
	  :
