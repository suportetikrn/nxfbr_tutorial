********************************************
Single Sign-On com AD usando NxLogon
********************************************

Quando se tem um AD é possível usar o recurso de Single Sign-On e não emitir mais uma solicitação de Login a seus usuários. Para isso é disponibilizado o agente NxLogon. Quando o NxLogon é executado ele cria e atualiza a sessão de login desse mesmo usuário no NxFilter.

Caso não deseje instalar este programa em cada PC na sua rede é possível usar um Script de Logon na GPO. Este script de logon será executado toda vez que um usuário se autenticar no AD e lançar o NxLogon.

.. note::
  Antes de iniciar esse processo é preciso importar usuários e grupos do AD. Para importá-los leia o procedimento 'GUI - Usuário'.
  
.. warning::
  NxLogon usa a porta 19002/TCP para se comunicar o NxFilter. Ela precisa estar liberada no seu firewall - caso haja um.

Você pode seguir esses passos para executar o NxLogon através do GPO.

#. Baixe o pacote nxlogon-x.x.zip do www.nxfilter.org.
#. Mude o endereço IP em ``nxlogon.bat`` para o IP do seu servidor NxFilter. Se estiver usando um cluster Nx você pode colocar múltiplos IPs apenas separando-os por `espaço`.
#. Abra 'Ferramentas Administrativas > Usuários e Computadores do Active Directory' em seu Domain Controller (DC).
#. Abra a aba 'Política de Grupo' em Propriedade do seu Domínio AD.

.. image:: /images/gpo.png

#. Clique no botão 'Editar' e então vá em 'Configuração do Usuário > Configurações do Windows > Scripts ( Logon/Logoff )'

.. image:: /images/gpo_edit.png

#. Clique em 'Logon' e clique em 'Adicionar' então clique em 'Navegar'. Você verá o diretório 'Logon' para selecionar o arquivo. Copie seu 'nxlogon.bat' e 'nxlogon.exe' do diretório gerado pelo pacote NxLogon, contido no diretório 'Logon'. Você pode arrastar e soltar os arquivos no diretório.

#. Selecione o arquivo copiado na pasta o 'nxlogon.bat' como um script de logon para adicionar.

