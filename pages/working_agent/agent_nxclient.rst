************************************
NxClient e filtro de usuário remoto 
************************************

NxFilter provê um aplicativo cliente para filtro em usuário remoto que é o NxClient. Uma vez instalado o NxClient no sistema de usuário você pode filtrar e monitorar o tráfego de Internet daquele usuário em sua GUI NxFilter de modo centralizado independente de sua localização.

.. note::

  Você precisa permitir o acesso às portas 53/UDP e 80,443/TCP no(s) servidor(es) NxFilter.

Instalação do NxClient
^^^^^^^^^^^^^^^^^^^^^^^

Após instalar o NxClient usando seu instalador, o sistema de configuração estará rodando. Aparecerá um formulário com os campos `Server IP` e `Login Token` e você precisa preenchê-los de acordo com seu ambiente.

.. note::

  No NxFilter cada usuário tem um login token. Você pode encontrar esse token em 'User & Group > User > Edit'.
  NxClient é um programa Windows que roda como serviço. Ele iniciará automaticamente com o sistema.
  Quando você instalar NxClient ou NxUpdate on Mac OS X, leia as instruções para NxCliente ou NxUpdate no MAC OS X neste tutorial.

Após fazer as devidas modificações e testar sua configuração e assim inicialiizar o sistema, é possível verificar se está funcionando em 'Logging > Signal'. Deverá haver registros do NxClient nesse relatório.

.. note::

  É possível adicionar mais de um IP de servidor NxFilter separando por ',' ser você estiver rodando um cluster do NxFilter.
  Para mudar a configuração execute o programa 'C:/Arquivos de Programas/nxclient/setup.exe'.

Sinais do NxClient
^^^^^^^^^^^^^^^^^^^^^^^

Quando há o interesse em controlar um usuário remoto a parte mais difícil é forçar os usuários a ter o acesso controlado. Ninguém tem interesse em ter o acesso controlado e ainda mais estão afastados da empresa. Se esses seus próprios computadores no trabalho não há como garantir o controle. Porém se o dispositivo for da empresa é possível controlá-lo instalando NxClient no sistema dele.

Em todo caso o que impede do usuário desinstalar e parar o NxClient? NxClient roda como serviço e não dispõe de um desinstalador em 'Adicionar/Remover programas' no Painel de Controle. Então se seus usuários não tem privilégios de administração e não pode desinstalá-lo.

Porém em alguns casos é necessário dar o privilégio de 'Administrador Local' a seus usuários. Neste caso não é possível impedir os usuários de removerem o NxClient. 

Por conta disso foram definidos diversos sinais que podem indicar o que está ocorrendo no sistema. NxCliente envia os seguintes sinais: ::

- START : Quando NxClient inicia ele envia esse sinal para o NxFilter.
- STOP : Quando o NxClient para ele envia esse sinal para o NxFilter.
- PING : A cada 5 minutos o NxClient envia esse sinal para o NXFilter.

Você pode visualizar esses sinais em 'Logging > Signal' na área de administração do NxFilter.

Fail-safe measure for NxClient
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxClient needs to update its pollicy from its server that is NxFilter. When NxClient can't connect to its server it bypasses filtering as your users need to be able to use the Internet anyway. You can specify multiple server IP addresses on its setup for redundacy.

Auto-switch between local filtering and remote filtering
********************************************************

When you use NxClient on your mobile worker's laptop you might have a problem with your filtering policy when they are staying in the office. Your mobile worker might be filtered twice. One from NxClient, one from your local NxFilter. And he/she might be required to go through the login-page of NxFilter.

To address this issue NxClient does auto-switch between local filtering and remote filtering. This means that NxClient can find NxFilter in a local network and when it is on your local network it stops its proxy filtering. Plus, it has its own NxLogon module doing single sign-on in your local network.

 .. warning:: 
  If you don't like this auto-switch behavior you can add 'no_switch = 1' into 'C:/Program Files/nxclient/conf/cfg.properties'.

Uninstalling NxClient
*********************

Para evitar uma desinstalação acTo prevent an accidental uninstallation by your user, NxClient doesn't provide an uninstaller for 'Add/Remove programs' in control panel. When you uninstall NxClient you need to do it manually with the following commands.
- Run 'C:/Program Files/nxclient/bin/unstsvc.bat'.
- Delete 'C:/Program Files/nxclient' folder.

Silent install
**************

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

