**********************************
GUI - Config 
**********************************

These are mostly system configuration parameters for NxFilter.

Config > Setup > Block and Authentication
*****************************************

- Block Redirection IP
This is the IP address of NxFilter itself. If there is a blocked DNS request, it will be redirected to this IP address. It is supposed to be populated automatically during the installation process.
* You can add multiple block redirection IP addresses separated by commas for redundancy.
- External Redirection IP
When you use a remote filtering agent you might need to use a different 'Block Redirection IP' for the remote filtering agent since it is outside of your network. If you leave this one empty NxFilter will use 'Block Redirection IP' for redirecting the remote filtering agent.
- IPv6 Redirection IP
You need to set this up when you use NxFilter as your IPv6 network DNS server.
- Enable Authentication
This option is required when you use any authentication methods including IP based authentication. After you enable this option, any unauthenticated user will be redirected to NxFilter's login-page. As a result your users will be forced to login to use the Internet.
- Login Domain
You can access NxFilter's login-page using a domain defined here.
- Logout Domain
You can clear out a user login session using a domain defined here.
- Login Session TTL
NxFilter keeps a login session after a user login. But this login session needs to be expired eventually. It is especially required when there is a shared PC by several users. If a user doesn't make any DNS request for the specified amount of time defined here, his/her login session expires and the user needs to login again.

Config > Setup > Syslog
***********************

NxFilter supports Syslog exportation of its log data. You can build your own reporting system with this feature or you can monitor all the logging in real-time way.

- Syslog Host
The host IP address to which you want to send syslog data.
- Export Blocked Only
With this option NxFilter sends the log data of blocked DNS request only.
- Enable Remote Logging
Enable Syslog exportation.
Config > Setup > NetFlow
NxFilter supports bandwidth control. This is possible by importing NetFlow data.
For more detail read this, Bandwidth control with NxFilter
- Router IP
The IP address of a device sending NetFlow data to NxFilter.
- Listen Port
The UDP port number of NetFlow collector.
- Run Collector
Run NetFlow collector. After change this option you need to restart NxFilter.
Config > Setup > Misc
***********************

- Admin Domain
You can access the admin GUI using the domain you set up. For example, if you use 'admin.nxfilter.org' as your admin domain you can access your admin GUI by typing 'http://admin.nxfilter.org/admin' into your browser address bar.
* This only works when you use NxFilter as your DNS server. Otherwise you need to register your admin domain to your own DNS server.
- Bypass Microsoft Update
You don't want to block Microsoft update with your filtering. Enabling this option means bypassing 'micfosoft.com' and 'windowsupdate.com' and their subdomains.
- Logging Retention Period
If you keep your log data too long it will use your disk space a lot. You can set how long NxFilter keeps its log data here.
- SSL Only to Admin GUI
When you want to allow only HTTPS access to the admin GUI enable this option. Once you enable this option you will be redirected to the SSL port automatically even if you use HTTP.
- Auto Backup
NxFilter makes a backup file for its config into '/nxfilter/backup' directory on '01:00' everyday. The name of the backup file starts with 'auto-' prefix. You can have up to 30 backups.
- Agent Policy Update Period
NxFilter provides several agents programs for application control and remote user filtering. These agents fetch their policies periodically. You can set up the policy update period for them here.

Config > Admin
***************

Você pode alterar o usuário administrador e a senha da GUI de administração aqui.

Config > Alert
***************

NxFilter sends an alert email for recent blocking or clustering node down incident. If you want to send an alert email to 'admin @ nxfilter.org' from 'alert200 @ gmail.com' on every 15 minutes then the setup would look like the followings.

- Admin email : admin @ nxfilter.org
- SMTP host : smtp:gmail.com
- SMTP host : 465
- SMTP SSL : on
- SMTP user : alert200
- SMTP password : ********
- Alert period : Every 15 minutes

Config > Allowed IP
***********************

NxFilter has IP based access restriction function for its DNS, GUI, login redirection. You may need to use this feature when you put your NxFilter on a public IP address. You can make whitelist/blacklist way of ACL here.

Config > Backup
***************

You can make a backup for the config DB of NxFilter manually. The backup files will be created into '/nxfilter/backup' directory.

Config > Block Page
*******************

This is the setup for custom block-page, login-page, welcome-page. When you edit your block-page you can use the following variables populated by NxFilter for making your block-page more informative.
- #{domain} : Blocked domain
- #{reason} : Reason for block
- #{user} : Logged-in username
- #{group} : Groups of the logged-in user
- #{policy} : The applied policy
- #{category} : Categories or the blocked domain

Config > Cluster
*****************

NxFilter has a built-in clustering. You can make your NxFilter to be a master node or a slave node in a cluster. After you change the values in cluster setup you need to restart your NxFilter to apply the new settings.
