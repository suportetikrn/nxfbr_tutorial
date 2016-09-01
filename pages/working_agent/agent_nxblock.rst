***********************
NxBlock para Chromebook
***********************

NxBlock é o agente remoto para filtragem no Chromebook. Ele também pode ser usado como um agente SSO em uma rede local.

.. note::
  NxBlock se tornou um software open source desde a versão 1.8. Você pode fazer o download do código completo na área de download.

.. image:: /images/nxblock.png

Instalação do NxBlock
^^^^^^^^^^^^^^^^^^^^^^^^

NxBlock é basicamente uma extensão do Chrome. Você pode instala-lo a partir da loja Chrome Web Store. É possível, também, baixar do seguinte link. ::

   https://chrome.google.com/webstore/detail/nxblock/gibapcjkdgdiamgdkbcpgaldogcoldgf


Política de filtro do NxBlock
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxBlock compartilha a política em ``Policy & Rule > Proxy Filtering`` com os outros agentes de filtro proxy. Ele sincorniza a política a cada 120 segundos.

Conexão com o NxFilter
^^^^^^^^^^^^^^^^^^^^^^^

Depois de instalar, você verá o NxBlock na área de extensões no painel de configurações do Chrome ou `chrome://extensions`. Abaixo do ícone do  NxBlock tem o link `opções`.Ao clicar no link você verá a página de configuração do NxBlock. Você precisa definir os seguinte parâmetros:
 - Sever IP : O endereço IP do NxFilter.
 - Login Token : A chave token definida para o usuário no NxFilter.

Uma vez que esses parâmetros tenham sido configurados você pode testar a conectividade com o servidor NxFilter clicando no botão `Test`. E então clique em `Save` e abra novamente o Chome para receber a nova configuração.

Protegendo a configuração com senha
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Você pode ocultar a área de configuração do NxBlock de seus usuários através de uma senha de autenticação.

Uma vez que tenha sido definida a senha e esta tenha sido ativada, os usuários serão impedidos de acessar a página de configuração do NxBlock e 'chrome://extension'.

.. note::

   Você pode usar a senha de cliente do NxFilter para acessar a configuração do NxBlock uma vez que ele tenha se conectado ao servidor.

Identificação do usuário
^^^^^^^^^^^^^^^^^^^^^^^^^^

We use login token and Google account to identify users. Suppose you create a user named 'student' and setup 10 NxBlock with the login token associated to 'student'. If these users don't login to Chrome they will be appeared on NxFilter side as 'student' but if one of them login to Chrome using 'john1234@gmail.com' for example, then he/she will be appeared as 'student_john1234' on NxFilter log view.

Central configuration for mass installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When you do mass installation for NxBlock the problem is that you don't want to set up its connection parameters one by one. If you just use it as a single sign-on agent in your local network it might be fine without the connection parameters but if you want to use it for remote filtering you must set these parameters.
To solve this problem, we have a way for setting up these values centrally. We use a webpage and Chrome's start page function for this. Simply speaking, you write a webpage containing these config values and then make that webpage to be Chrome's start page on Google admin console. Then everytime your users start their Chrome they will set up themselves with the values.
When you write the webpage you add a meta tag like the followings,
<meta name='nxblock' content='192.168.0.100:HW00IYKW:1'>

We have 3 parameters separated by colons. The first one is NxFilter's IP address and the second one is a login token and the last one is about locking or unlocking Chrome's extension setup page.

On Google admin side,

 #. From the main dashboard, go to Device Management > Chrome > User Settings.
 #. Select the organizational unit to which you want the settings to apply.
 #. Find 'Pages to Load on Startup'.
 #. Enter the URL for the web page containing NxBlock configuration meta tag.
 #. Click the 'Save Changes' button.
