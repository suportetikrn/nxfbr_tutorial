Single sign-on com AD usando NxMapper
**************************************

  Enquanto que usar o NxLogon seja a melhor solução para SSO com AD, algumas pessoas encontram dificuldade na sua configuração por envolver ajustes de GPO e script de logon.

  Então é oferecida uma alternativa mais fácil de implementar o SSO.Quando você instala o NxMapper no seu Domain Controller ele vai buscar o nome do usuário e o endereço IP ao se autenticar no AD e cria a sessão no NxFilter.

.. note::

   Se deseja usar o recurso de SSO no AD é preciso, antes de qualquer coisa, importar usuários e grupos do seu AD. 
   Para fazer isso leia a parte 'GUI - User'.

Instalando e rodando o NxMapper 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 O instalador do NxMapper para Windows é disponibilizado na nossa seção de Download. Ele instalará o NxMapper como um serviço do Windows. Após instalá-lo, aparecerá a tela de configuração.

  #. NxMapper precisa ser instalado no Domain Controller.
  #. Você pode adicionar diversos IP separados por vírgulas, caso tenha um cluster de NxFilter.
  #. NxMapper usa a porta TCP/19002 para se comunicar com o NxFilter.

 Após modificar os arquivos de configuração, teste sua configuração antes e então inicie o serviço.

Diferença de uso com o NxLogon
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 Apesar de ser facilmente confundido com o NxLogon, NxMapper tem suas limitações.
 
 A sessão criada com o NxMapper pode expirar. Enquanto que o NxLogon atualiza as informações da sessão a todo minuto, NxMapper cria ou atualiza somente quando o usuário faz algo no controlado de domínio. Uma vez que a sessão expira os usuários serão redirecionados para a tela de login do NxFilter. Para evitar que isso ocorra você pode aumentar o tempo da sessão em `Config > Setup > Block and Authentication > Login session TTL`.

.. note::
  It can be expired as NxMapper doesn't refresh it. But as long as there is an activity from a user NxFilter refreshes the login session. It usually expires when a user returned to his/her desk from a long break.

Terminal server exclusion
^^^^^^^^^^^^^^^^^^^^^^^^^^

 Quando o NxMapper é usado, podem haver problemas com o Terminal Server do Windows. Se existirem múltiplos usuários em um só sistema o endereço IP do sistema será associado ao último usuário detectado pelo NxMapper. O que significa que seus usuários podem aparecer no NxFilter com um nome diferente. Para evitar esse tipo de problema a melhor solução seria vincular um IP para o seu terminal server.

