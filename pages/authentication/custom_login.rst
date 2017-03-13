Script de Login Personalizado para SSO
***************************************

 Atualmente NxFilter suporta SSO com AD. Em todo caso algumas pessoas querem outros tipos de validadores. Por exmeplo, você pode querer que o SSO seja aplicado ao seu OpenLDAP.

 NxFilter tem uma API para permitir a criação de sessões através do protocolo HTTP. Você precisa escrever seu próprio script de login para executar uma determinada página no servidor Web do NxFilter. E então seus usuários não precisarão acessar a página de login do NxFilter.

 Existem alguns exemplos em `/nxfilter/example/login_user.jsp`. Inicialmente o acesso a página é restrito apenas a localhost, por questões de segurança, mas você pode editar o arquivo JSP e permitir chamadas a partir da sua rede local.

 O caminho para executar essa página é :

.. note::

  http://192.168.0.100/example/login_user.jsp?ip=192.168.0.100&uname=john

Como podes ver a página recebe 2 parâmetros. O primeiro é o IP da máquina do usuário e o segundo é o nome do usuário.

.. warning::

  Não esqueça de importar ou criar os usuários no NxFilter.

Um ponto a se considerar quando for feito o script é que tem de ser verificar uma forma da página ser chamada periodicamente. Lembre que há no NxFilter o conceito de tempo de sessão. Se não houver atividade de um usuário autenticado por um determinado tempo a sessão expirará. Então se você não deseja que a página de Login fique aparecendo para os seus usuários, é preciso fazer o refresh na página desse script de tempos em tempos.

Há 3 métodos na classe `UserLoginDao` que são utilizados pelo script de login:

.. code-block:: java
  
  createIPSession(String ip, String uname) // Cria a sessão de login com IP e usuário

  deleteIPSession(String ip) // Fecha a sessão informando o IP

  findUser(String ip) // Localiza o usuário com base no IP informado.

.. note:: 

  Todas as paginas de exemplo estão em `/nxfilter/webapps/example`.

