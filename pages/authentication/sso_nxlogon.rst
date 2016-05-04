********************************************
Single Sign-On com AD usando NxLogon
********************************************

Quando se tem um AD é possível usar o recurso de Single Sign-On e não emitir mais uma solicitação de Login a seus usuários. Para isso é disponibilizado o agente NxLogon. Quando o NxLogon é executado ele cria e atualiza a sessão de login desse mesmo usuário no NxFilter.

Caso não deseje instalar este programa em cada PC na sua rede é possível usar um Script de Logon na GPO. Este script de logon será executado toda vez que um usuário se autenticar no AD e lançar o NxLogon.
.. note::
  Antes de iniciar esse processo é preciso importar usuários e grupos do AD. Para importá-los leia o procedimento 'GUI - Usuário'.
  
.. alert::
  NxLogon usa a porta 19002/TCP para se comunicar o NxFilter. Ela precisa estar liberada no seu firewall - caso haja um.

You can follow these steps to launch NxLogon from GPO.
1. Download nxlogon-x.x.zip package from www.nxfilter.org.
2. Modify IP address in 'nxlogon.bat' to point NxFilter. If you use clustering add multiple IP addresses separated by spaces.
3. Open 'Administrative Tools > Active Directory Users and Computers' on your DC.
4. Open 'Group Policy' tab in properties of your Active Directory Domain.
