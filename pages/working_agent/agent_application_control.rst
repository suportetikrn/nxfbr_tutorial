************************************
Controlando aplicações com NxClient
************************************

O NxFilter permite que se controle as aplicações executadas no desktop com o agente NxClient. Você pode bloquear as aplicações desejadas configurando a política de controle de aplicações através da GUI do NxFilter - de modo centralizado - e ainda visualizar, quem tentou executar os programas bloqueados, através dos logs.


Como funciona?
^^^^^^^^^^^^^^
After you define your application control policy on 'Policy & Rule > Application Control' NxClient retrieves the application control policy periodically.
* You can adjust the policy update period by changing the value for	'Agent Policy Update Period' on 'Config > Setup'.
Supported options
1. Block by port scanning
NxClient detects UltraSurf and Tor processes by port scanning. This means even if your users change the process name or run them from a USB stick you can find and block them.
2. Block by process name
You can block a process running by its name. This works based on keyword matching against process name. You can add the blocked keywords on GUI and If your agent finds the matching process name it will block the process.
Enable application control only for specific users
Basically the application control of NxFilter supposed to be a global policy. When you want to disable it for some user use 'Disable Application Control' option on 'Policy & Rule > Policy > EDIT'.
Logging blocked application
NxFilter is basically a DNS filter so its log data format was designed for showing the allowed/blocked domains. To accommodate the log data about a blocked application NxFilter introduced these domains or rules.
- ultrasurf.port.app : UltraSurf has been blocked by port scanning.
- tor.port.app : Tor has been blocked by port scanning.
- chrome.exe.pname.app : Chrome has been blocked by its process name.
- Skype.title.app : Skype has been blocked by its window title.
* When you enable 'Block UltraSurf' and there is UltraSurf extension for Chrome or other extensions having proxy permission installed NxClient kills Chrome process and sends 'ultrasurf.chrome.app' signal.
Execution Interval
Finding and blocking application may cause some amount of CPU load. If you don't want to cause too much load form your client PC, increase 'Execution Interval' on 'Policy & Rule > Application Control'.
