# ipfw_nat

ipfw nat を利用する人は、rc.conf で

	firewall_nat_enable="YES"
	firewall_nat_interface="em0"
	firewall_nat_flags="deny_in reset same_ports unreg_only redirect_port tcp 192.168.1.1:25 25 ..."

とかして運用されいると思いますが、redirect_port ルールが多いと
firewall_nat_flags が長くなり、かつ、ちょっと変更するのにも面倒です。なによ
りもメンテナンス上、ルールが見難くなりトラブルが発生しかねません。ということ
で、ルールを別ファイルとして管理するように rc.firewall を変更してみました。
こんなかんじです。

	firewall_nat_enable="YES"
	firewall_nat_interface="em0"
	firewall_nat_flags="deny_in reset same_ports unreg_only"
	firewall_nat_rules="/etc/ipfw_nat.rules"

たとえば /etc/ipfw_nat.rules は

	redirect_port	tcp 192.168.1.1:25	25
	redirect_port	tcp 192.168.1.2:80	80
	redirect_port	tcp 192.168.1.3:21	21
	  :
