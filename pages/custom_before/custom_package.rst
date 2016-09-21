Criando seu próprio pacote de instalação dos agentes
***********************************************************

Você pode fazer seu próprio pacote dos agentes NxClient, NxUpdate, NxMapper, NxLogon, NxBlock, NxRelay.

Já o NxLogon, que é uma aplicação simples sem instalador você só precisa substituir vários arquivos do arquivo zip original e fazer seu próprio arquivo zip. Você pode alterar o nome dele também, mas quando fizer essa alteração é indicado mudar também o conteúdo dos arquivos batch mas isso será visto a frente.

Contudo esse processo é um pouco diferente para o NxClient, NxUpdate e NxMapper uma vez que estes requerem que sejam feitos instaladores para Windows e Mac OS.

Criando sua própria instalação Windows
----------------------------------------

Para fazer os instaladores do Windows foi utilizado o `Inno Setup`_ . Quando NxClient, NxUpdate e NxMapper é instalando, eles criam seus próprios diretórios dentro de 'C:/Program Files (x86)' e registrado como um serviço Windows. 

Por exemplo, quando é executado o instalador NxClient todos os arquivos necessários são copiados para 'C:/Program Files (x86)/nxclient' e então é executado 'bin/instsvc.bat' para registrá-lo como serviço Windows e então é executado o arquivo 'bin/setup.bat' ao término do processo de instalação para rodar seu programa de configuração.

.. note::

 - Se você se tornar nosso parceiro comercial podemos disponibilizar nosso script Inno Setup.

 - Os arquivos zip usados para criar nossos pacotes de instaladores estão em um pacote antigo na nossa página de download.

 - Quanto o sistema é removido, é executado o batch 'bin/unstsvc.bat' para remover o registro do serviço do Windows.

Criando seu instalador para o Mac OS
-------------------------------------

É usado o programa `Packages`_ para construir nosso instalador Mac OS. Quando o instalador é executado ele criará seus diretórios em '/Library' e o arquivo 'conf/plist.default' é copiado para dentro de '/Library/LaunchDaemons' com um novo nome como 'org.nxfilter.nxclient.plist' para ser executado como um daemon. E então ele roda o script 'setup-mac.sh' localizado no diretório de instalação para iniciar o programa de configuraçãoi.

Para remover o programa você precisa rodar o script 'uninstall-mac.sh', que está dentro do diretório de instalação.

.. note::

  - Podemos disponibilizar nosso script do Packages se for nosso parceiro comercial.

  - Os arquivos zip usados para criar nossos pacotes de instaladores estão em um pacote antigo na nossa página de download.

Mudando o nome da aplicação
---------------------------

Quando você personalizar nossos agentes, uma das coisas que pode desejar é mudar os nomes dos nossos agentes. Altere o arquivo 'conf/appname', localizado no diretório de instalação. Quando o nome é alterado, ele aparecerá no programa de instalação dos nossos agentes.


Replacing icon file and default setup value
Substituindo/Alterando ícones
------------------------------

Para usar seu próprio ícone, o arquivo é ''nxd.ico'' localizado no diretório de instalação e é um arquivo que contém ícones com as dimensões 16x16, 32x32 e 48x48. No momento só é usado para o Instalador Windows e programa de configuração.

.. note::
  
  A versão do NxClient e NxUpdate baseado em Java precisa que seja adicionado mais um ícone cujo nome seria 'nxd16.png'. É um arquivo PNG de 16x16 para a GUI de configuração.

Também é possível mudar os valores padrão na conexão com o servidor. Você pode modificar os valores padrão de 'Server IP' e 'Login Token' do programa de configuração alterando o arquivo 'conf/cfg.default'.

  O arquivo 'conf/cfg.default' será copiado por cima do arquivo 'conf/cfg.properties' quando você executa o programa de configuração pela primeira vez ou durante o processo de instalação.

Escrevendo seu programa de configuração 
-----------------------------------------

É possível construir seu próprio pacote, para fazê-lo e incluir seu programa de configuração. Em nossos programas de configuração existem alguns controles e botões. Para controle, nós lemos os paramêtros no arquivo 'conf/cfg.properties'.

E quando você clicar nos botões que são 'SAVE', 'TEST', 'START', 'STOP' as ações são feitas relendo/alterando o arquivo de configuração.

  - O botão 'SAVE' grava os valores definidos na tela em 'conf/cfg.properties'. 
  - Os botões 'START' e 'STOP', se forem usados no Windows chamam os comandos 'net start' e 'net stop' considerando que o agente foi instalado como serviço. Já no Mac OS, é executado o programa '/bin/launchstl' com o arquivo Plist gravado no diretório '/Library/LaunchDaemons'.

Então - reafirmando - ao fazer seu programa de configuração para o NxClient no Windows, quando for clicando em 'START' e 'STOP' você precisa executar os comandos,

.. code-block:: bash

   net start NxClient

   net stop NxClient

Quando for no Mac OS,

.. code-block:: bash

    /bin/launchctl load -w /Library/LaunchDaemons/org.nxfilter.nxclient.plist

    /bin/launchctl unload -w /Library/LaunchDaemons/org.nxfilter.nxclient.plist

O botão 'TEST' executa o batch 'bin/test.bat' ou o script 'bin/test.sh'. Antes de executar seu próprio script de testes você precisa gravar primeiro os valores de configuração.

Após você executar o script de teste você pode receber algumas mensagens com os seguintes códigos de saída.

0 = Sucesso
-1 = Valores incorretos na configuração
-2 = Erro de conexão
-3 = Erro de login

.. note::

   Para o NxMapper, ao invés de 'bin/test.bat' é usado o aplicativo 'test.exe'.
  
   Para o NxMapper não há code de erro do login já que não existe processo de login.

Personalizando o NxBlock
--------------------------

NxBlock é um software Open Source. Você pode fazer o download de seu código fonte na área de download de nossa página.

Personalizando o NxRelay
--------------------------

Não é disponibilizado um instalador ou programa de configuração do NxRelay por não ser um sistema para um usuário comum do Windows. Mas sua estrutura é a mesma do NxFilter. Nos tópicos anteriores é explicado como criar um pacote de instalação, siga o mesmo procedimento.

Limitação
--------------

Preparando seu próprio instalador e modificando os nomes dos agentes geralmente atende a maioria das necessidades. Mas há algo que não pode ser mudado. Internamente, no sistema, há uma codificação contendo a assinatura 'nxfilter'. É importante mantê-la para que tenhamos uma unica assinatura e possamos diferenciar os sinais recebidos dos agentes.

E também não é permitido remove a licença ou qualquer das licenças de terceiro sob pena de caracterizar uma violação na licença base. Você pode ter seu próprio arquivo de licença mas a licença base precisa ser mantida. Sào permitidas muitas caracterizações e alterações, então é inevitável não ter alguma limitação.

.. target-notes::
.. _`Inno Setup`: http://www.jrsoftware.org
.. _`Packages`: http://s.sudre.free.fr
