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

Para identificar os usuários são usados o token e a conta do Google. Suponhamos que tenha sido criado um usuário com o nome `estudante` no NxFilter e foram configurados 10 NxBlock com o mesmo token desde usuário. Se nenhum dos usuários se autenticarem no Chrome ( na autenticação do Google ) eles aparecerão nos registros do NxFilter como `estudante` porém se um deles se autenticar no Chrome usando `zedosanzois@gmail.com` - por exemplo - então ele/ela aparecerá como `estudante_zedosanzois` no log do NxFilter.

Configuração centralizada para instalação em massa
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ao fazer uma instalação em massa do NxBlock o problema é que você não terá interesse em configurar os parâmetros necessários um a um. Se você usar somente o agente SSO em sua rede local poderia até ser bom sem os parâmetros de conexão, mas se você deseja usá-lo como filtro remote você precisa definir esses parâmetros.

Para resolver esse problema, nós temos uma alternativa, uma forma de configurar esses valores de modo centralizado. Nós usamos uma pagina web e a função de página de inicialização do Chrome para isto.

Falando de forma objetiva, você irá criar uma página web contendo os valores de configuração e então fazer com que está página seja a página inicial do Chrome. Então toda vez que seus usuários abrirem seus browsers eles serão configurados com estes valores.

Ao criar a página web você adicione a meta tag descrita a seguir ::

  <meta name='nxblock' content='192.168.0.100:HW00IYKW:1'>

Há 3 parâmetros separados por vírgulas. O primeiro é o IP do servidor NxFilter e o segundo é o token de login e o último é sobre bloquear ou não o acesso a página de configuração de extensão do Chrome.

No lado do Google Admin - para configurar a página inicial,

 #. No dashboard, vá em Gerenciamento de Dispositivo > Chrome > Configurações do Usuário
 #. Selecione a unidade organizacional onde serão aplicadas as configurações.
 #. Localize `Páginas para carregar na inicialização`.
 #. Insira a URL para página web que contém a tag de configuração do NxBlock.
 #. Clique em `Salvar alterações`.
