Script de Login Personalizado para SSO
***************************************

 Atualmente NxFilter suporta SSO com AD. Em todo caso algumas pessoas querem outros tipos de validadores. Por exmeplo, você pode querer que o SSO seja aplicado ao seu OpenLDAP.

 NxFilter tem uma API para permitir a criação de sessões através do protocolo HTTP. Você precisa escrever seu próprio script de login para executar uma determinada página no servidor Web do NxFilter. E então seus usuários não precisarão acessar a página de login do NxFilter.

 Existem alguns exemplos em `/nxfilter/example/login_user.jsp`. Inicialmente o acesso a página é restrito apenas a localhost, por questões de segurança, mas você pode editar o arquivo JSP e permitir chamadas a partir da sua rede local.

 O caminho para executar essa página é :

.. code-block::

  http://192.168.0.100/example/login_user.jsp?ip=192.168.0.100&uname=john


 Como podes ver a página recebe 2 parâmetros. O primeiro é o IP da máquina do usuário e o segundo é o nome do usuário.
 ::
  Não esqueça de importar ou criar os usuários no NxFilter.

One thing you need to consider when you write your own login script is that it might be better to call the webpage periodically. There is a session timeout concept in NxFilter. If there is no activity from a logged-in user for certain amount of time the login session will be expired. So if you don't want to show your users NxFilter's login-page, you would need to refresh the login session periodically.
There are three methods of UserLoginDao class for custom login script.

.. code-block:: java
  
  create_ip_session(String ip, String uname) : Creating a login session with an IP and username.

  delete_ip_session(String ip) : Deleting a login session with an IP.

  find_user(String ip) : You can find a logged-in username by its associated IP address.


 .. note:: 

  Todas as paginas de exemplo estão em `/nxfilter/webapps/example`.

