**********************************
NxClient and remote user filtering
**********************************

NxFilter prove um aplicativo cliente para filtro em usuário remoto que é o NxClient. Uma vez instalado o NxClient no sistema de usuário você pode filtrar e monitorar o tráfego de Internet daquele usuário em sua GUI NxFilter de modo centralizado independente de sua localização.

 .. note::
  You need to open 53 UDP and 80, 443 TCP ports on NxFilter side.

Instalação do NxClient
************************

Após instalar o NxClient usando seu instalador, o sistema de configuração estará rodando. Aparecerá um formulário com os campos `Server IP` e `Login Token` e você precisa preenchê-los de acordo com seu ambiente.

 .. note::

  No NxFilter cada usuário tem um login token. Você pode encontrar esse token em 'User & Group > User > Edit'.
  NxClient é um programa Windows que roda como serviço. Ele iniciará automaticamente com o sistema.
  Quando você instalar NxClient ou NxUpdate on Mac OS X, leia as instruções para NxCliente ou NxUpdate no MAC OS X neste tutorial.

Após fazer as devidas modificações e testar sua configuração e assim inicialiizar o sistema, é possível verificar se está funcionando em 'Logging > Signal'. Deverá haver registros do NxClient nesse relatório.

 .. note::
  É possível adicionar mais de um IP de servidor NxFilter separando por ',' ser você estiver rodando um cluster do NxFilter.
  Para mudar a configuração execute o programa 'C:/Arquivos de Programas/nxclient/setup.exe'.

Signals of NxClient
*******************

When it comes to a remote user filtering the most tricky part would be how to force users to be filtered. Nobody wants to get filtered and they are away from your office. If they use their personal PC then you can not filter them anyway. But when they use a company laptop you still can filter them by installing NxClient on their system.
However what if they uninstall or stop NxClient? NxClient is running as a service and it doesn't provide an uninstaller for 'Add/Remove programs' in control panel. So if your users don't have enough privilege they can't uninstall it.
But sometimes you need to give your users 'Local Administrator' privilege. In that case it's not possible to stop your users from uninstalling NxClient. So we defined several signals with which you can find out what's happening on a user system. NxClient send the following signals.
- START : When NxClient starts it sends START signal to NxFilter.
- STOP : When NxClient stops it sends STOP signal to NxFilter.
- PING : On every 5 minutes NxClient sends PING signal to NxFilter.
You can view these signals on 'Logging > Signal' on NxFilter GUI.
Fail-safe measure for NxClient
NxClient needs to update its pollicy from its server that is NxFilter. When NxClient can't connect to its server it bypasses filtering as your users need to be able to use the Internet anyway. You can specify multiple server IP addresses on its setup for redundacy.
Auto-switch between local filtering and remote filtering
When you use NxClient on your mobile worker's laptop you might have a problem with your filtering policy when they are staying in the office. Your mobile worker might be filtered twice. One from NxClient, one from your local NxFilter. And he/she might be required to go through the login-page of NxFilter.
To address this issue NxClient does auto-switch between local filtering and remote filtering. This means that NxClient can find NxFilter in a local network and when it is on your local network it stops its proxy filtering. Plus, it has its own NxLogon module doing single sign-on in your local network.
* If you don't like this auto-switch behavior you can add 'no_switch = 1' into 'C:/Program Files/nxclient/conf/cfg.properties'.
Uninstalling NxClient
To prevent an accidental uninstallation by your user, NxClient doesn't provide an uninstaller for 'Add/Remove programs' in control panel. When you uninstall NxClient you need to do it manually with the following commands.
- Run 'C:/Program Files/nxclient/bin/unstsvc.bat'.
- Delete 'C:/Program Files/nxclient' folder.
Silent install
Some people want to install NxClient on multiple PCs using GPO or PDQ deployment. For this, we have the silent install option for NxClient.
For silent install,
/silent : Runs the installer in silent mode (The progress window is displayed).
/verysilent : Very silent mode. No windows are displayed.
And you can specify 'Server IP' and 'Login Token',
/server=192.168.0.100
/token=2P1WQ6VF
This is the final form of the command.
    nxclient-6.0-win.exe /silent /server=192.168.0.102 /token=2P1WQ6VF
* You can build your own MSI package using MSP wrapper from http://www.exemsi.com.
* When you install Java silently as a prerequisite for NxClient it might not be starting. This is mostly because when you install Java silently it doesn't set 'PATH' environment variable for itself.

