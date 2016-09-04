NxRelay - para identificar usuários de outras redes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxRealay é um servidor Relay de DNS para o NxCloud. Com NxRelay você pode associar um IP Privado ou um Range de IPs a um determinado usuário no NxCloud. O que significa que você pode aplicar diferentes políticas de controle baseados nos IPs privados dos seus clientes.

.. note::

   NxRelay tem como pre-requisito o NxCloud 3.4.2 ou superior.

Como funciona?
^^^^^^^^^^^^^^^


NxRelay itself is a forwarding DNS server. It does filtering by querying NxCloud and it works as a DNS server by forwarding DNS queries to your local DNS server. For NxRelay, NxCloud is not its upstream DNS server. Rather it's a policy server. Its upstream server is your existing DNS server or MS DNS server if you are on Active Directory. This means even if you lose the connection to NxCloud your network will be working fine. And you will not have an issue with Active Directory integration or local domain resolving as all the queries will be resolved by your local DNS server.
* Since it is a DNS server you can have fail-safe and load balance easily. Install multiple NxRelay servers and make them as the primary and secondary DNS servers of your network.
* It sends 'START' and 'PING' signals. You can verify if it works on 'Logging > Signal' on NxCloud GUI.
Install it on Windows as a Windows service
1. Download its zip package.
2. Extract it into 'c:/nxrelay'.
On CMD,
cd c:/nxrelay/bin
instsvc.bat
net start NxRelay
* Before you start it you need to modify its config parameters in '/opt/nxrelay/conf/cfg.properties'.
Install it on Linux as a Systemd service
1. Download its zip package.
2. Extract it into '/opt/nxrelay'.
On command line,
cd /opt/nxrelay
sudo chmod +x bin/*.sh
sudo cp script/nxrelay.service /lib/systemd/system/nxrelay.service
sudo systemctl enable nxrelay.service
sudo systemctl start nxrelay.service
To stop it,
sudo systemctl stop nxrelay.service
* Before you start it you need to modify its config parameters in '/opt/nxrelay/conf/cfg.properties'.
How to set it up
You need one of your NxCloud server IP and a login token from one of your user accounts. It has all of its config parameters in '/opt/nxrelay/conf/cfg.properties'.
For example,
server = 192.168.0.100
token = BSYEB28O
local_dns = 8.8.8.8,8.8.4.4
local_domain =
When you have these config values in the config file, your NxCloud server IP is '192.168.0.100' and the login token is 'BSYEB28O' and your local DNS server or the existing DNS server is '8.8.8.8' and '8.8.4.4'. If you have some domains to bypass from filtering you can add them as the comma separated value of 'local_domain'.
After you modify the config file, restart NxRelay. And then make them as the only DNS server for your network.
* You can add multiple NxCloud server IP addresses separated by commas.
* You can verify your config values and the connectivity by running '/opt/nxrelay/bin/test.sh'.
Which policy to apply
When you run NxRelay as the DNS server for your network it starts filtering with the policy associated to the login token you set up in the config file. But that is just a default policy for NxRelay. You can apply a different policy based on IP address. On NxCloud's operator GUI, create a user and associate one private IP address or IP range in your network to the user. Now the users on the associated IP address or IP address range will be under the policy of the user you created on NxCloud GUI.
Scipts included
In '/opt/nxrelay/bin' there are several scripts included.
startup.sh - Starting NxRelay.
shutdown.sh - Stopping NxRelay.
test.sh - Test the connectivity to NxCloud.
ping.sh - Test if it is running.
For Windows,
instsvc.bat - Installing 'NxRelay' service.
unstsvc.bat - Uninstall 'NxRelay' service.
For Ubuntu we have a Systemd script in '/opt/nxrelay/script',
nxrelay.service
