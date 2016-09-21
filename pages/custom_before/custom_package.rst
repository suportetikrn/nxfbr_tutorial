Criando seu próprio pacote de instalação dos agentes
***********************************************************

Você pode fazer seu próprio pacote dos agentes NxClient, NxUpdate, NxMapper, NxLogon, NxBlock, NxRelay.

Já o NxLogon, que é uma aplicação simples sem instalador você só precisa substituir vários arquivos do arquivo zip original e fazer seu próprio arquivo zip. Você pode alterar o nome dele também, mas quando fizer essa alteração é indicado mudar também o conteúdo dos arquivos batch mas isso será visto a frente.

Contudo esse processo é um pouco diferente para o NxClient, NxUpdate e NxMapper uma vez que estes requerem que sejam feitos instaladores para Windows e Mac OS.

Criando sua própria instalação Windows
----------------------------------------

Para fazer os instaladores do Windows foi utilizado o [[Inno Setup|http://www.jrsoftware.org]]. Quando NxClient, NxUpdate e NxMapper é instalando, eles criam seus próprios diretórios dentro de 'C:\Program Files (x86)' e registrado como um serviço Windows. Por exemplo, quando é executado o instalador NxClient todos os arquivos necessários são copiados para 'C:/Program Files (x86)/nxclient' e então é executado 'bin/instsvc.bat' para registrá-lo como serviço Windows e então é executado o arquivo 'bin/setup.bat' ao término do processo de instalação para rodar seu programa de configuração.

.. note::

 - Se você se tornar nosso parceiro comercial podemos disponibilizar nosso script Inno Setup.

 - Os arquivos zip usados para criar nossos pacotes de instaladores estão em um pacote antigo na nossa página de download.

 - Quanto o sistema é removido, é executado o batch 'bin/unstsvc.bat' para remover o registro do serviço do Windows.

Criando seu instalador para o Mac OS
-------------------------------------

É usado o programa [[Packages|http://s.sudre.free.fr]] para construir nosso instalador Mac OS. Quando o instalador é executado ele criará seus diretórios em '/Library' e o arquivo 'conf/plist.default' é copiado para dentro de '/Library/LaunchDaemons' com um novo nome como 'org.nxfilter.nxclient.plist' para ser executado como um daemon. E então ele roda o script 'setup-mac.sh' localizado no diretório de instalação para iniciar o programa de configuraçãoi.

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


If you can build your own package, to build and include your own setup program is also a possible option. On our setup programs there are some input controls and buttons. For input controls, we read the values from 'conf/cfg.properties' file.

And when you click the buttons that are 'SAVE', 'TEST', 'START', 'STOP' we do some action with the updated config values. With 'SAVE' button we save the config values into 'conf/cfg.properties' file. For 'START' and 'STOP' buttons, if it is on Windows we use 'net start' and 'net stop' commands as we install our agent as a service. On Mac OS, we use '/bin/launchstl' command with the Plist file we copied into '/Library/LaunchDaemons' directory.
So when you make a setup program for NxClient on Windows, you need to run these commands with 'START' and 'STOP' buttons,

.. code-block:: bash

   net start NxClient

   net stop NxClient

If it is on Mac OS,

.. code-block:: bash

    /bin/launchctl load -w /Library/LaunchDaemons/org.nxfilter.nxclient.plist

    /bin/launchctl unload -w /Library/LaunchDaemons/org.nxfilter.nxclient.plist

For 'TEST' button, you can run 'bin/test.bat' or 'bin/test.sh' script. Before you run the test script you have to save the config values first.
After you run the test script you can get some messages with the following exit codes.
0 = Success
-1 = Invalid config values
-2 = Connection error
-3 = Login error
* For NxMapper, we have 'test.exe' instead of 'bin/test.bat'.
* For NxMapper, we don't have the login error code as there is no login process.

Customization of NxBlock
--------------------------

NxBlock is an open source software. You can download its source code from our download page.
Customization of NxRelay
We don't provide an installer or a setup program for NxRelay as we don't think it is for an ordinary Windows user. But its structure is almost same as NxFilter. You have enough knowledge to make an installer package for it, if you already read the previous part of this tutorial.

Limitation
--------------

Building your own installers and changing the names of the client softwares will do what you want to do mostly. But there is something you can't touch or change. We have some internal code having 'nxfilter' signature. This is important as we need to have a unique signature to diffrentiate signals from our agents.
And you don't remove our license or any third party license from the package otherwise that is a license violation. You can have your own license file but you need to keep our license somewhere. All in all it is our software and you just customize it, so it is inevitable to have some limitation.

