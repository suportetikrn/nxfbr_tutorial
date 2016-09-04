NxRelay - para identificar usuários de outras redes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxRelay é um servidor Relay de DNS para o NxCloud. Com NxRelay você pode associar um IP Privado ou um Range de IPs a um determinado usuário no NxCloud. O que significa que você pode aplicar diferentes políticas de controle baseados nos IPs privados dos seus clientes.

.. note::

   NxRelay tem como pre-requisito o NxCloud 3.4.2 ou superior.

Como funciona?
^^^^^^^^^^^^^^^


O NxRelay por si só é um servidor DNS Forward. Ele faz a filtragem consultando o NxCloud e trabalha como um servidor DNS redirecionando as consulta DNS para seu servidor de DNS local. Para o NxRelay, o NxCloud não é um servidor DNS Upstream, pelo contrário é um servidor de políticas. O servidor upstream é o seu servidor DNS local ou o servidor MS do AD que responde as suas consultas DNS.

Isso significa que mesmo que você percar a conexão com o NxCloud sua rede continuará a funcionar. E você não terá problemas com sua rede AD ou resolução de nomes do domínio locai, já que suas consultas DNS continuarão sendo resolvidas por seu servidor local.

.. note::
   
   Sendo ele um servidor DNS você pode ter alta disponibilidade e load balance facilmente. Instale múltiplos servidores NxRelay e configure suas estações usando eles como servidores DNS Primário e Secundário.

   Ele envia o sinal 'START' e 'PING'. Você pode verificar se ele está funcionando em 'Logging > Signal' na GUI do NxCloud.


Instalando como um serviço no Windows
-------------------------------------


1. Faça o download do pacote zip
2. Descompacte dentro do diretório 'c:/nxrelay'

   No Prompt CMD, faça

.. code-block:: powershell 

    cd c:\nxrelay/bin
    instsvc.bat
    net start NxRelay
    
.. note::
  
   Antes de iniciar o serviço é preciso alterar os parâmetros de configuração em ''c:\nxrelay\conf\cfg.properties''.


Instalando SystemD no Linux
----------------------------

1. Faça o download do pacote zip
2. Descompacte dentro do diretório '/opt/nxrelay'

  No shell ( bash/sh ) digite:

.. code-block:: bash

    cd /opt/nxrelay
    sudo chmod +x bin/*.sh
    sudo cp script/nxrelay.service /lib/systemd/system/nxrelay.service
    sudo systemctl enable nxrelay.service
    sudo systemctl start nxrelay.service

Para parar o serviço

.. code-block:: bash

    sudo systemctl stop nxrelay.service

.. note::

   Antes de iniciar o serviço é preciso alterar os parâmetros de configuração em ''/opt/nxrelay/conf/cfg.properties''.


Parametrizando
--------------

Antes de iniciar você precisa ter o endereço IP do servidor NxCloud e um token de uma das contas de usuário. Os parâmetros ficam em ''/opt/nxrelay/conf/cfg.properties''.

Por exemplo:

.. code-block:: jproperties

   server = 192.168.0.100
   token = BSYEB28O
   local_dns = 8.8.8.8,8.8.4.4
   local_domain =

Tendo esses parâmetros no arquivo de configuração, considerando que o IP do servidor NxCloud é '192.168.0.100' e o token do usuário 'BSYEB280' e o servidor de DNS local ou o existente é o '8.8.8.8' e '8.8.4.4'. Se há domínios ou endereços que deseja que não sejam filtrados você pode adiciona-los em ''local_domain'' separando-os por virgula.

Depois de modificar o arquivo de configuração, sempre reinicie o NxRelay. E então configure o mesmo para ser seu único servidor DNS na rede.

.. note::
 
  - É possível adicionar múltiplos servidores NxCloud, basta separar os IPs por vírgulas.

  - Pode ainda verificar se a configuração está correta e a conectividade com o servidor através do comando ''/opt/nxrelay/bin/test.sh''

Que políticas aplicar?
-----------------------

Quando o NxRelay estiver funcionando em sua rede local como o servidor DNS ele inicia o filtro com a política associada ao token registrado nele. Porém isso é apenas um procedimento padrão para o NxRelay. Você pode aplicar diferentes políticas baseadas nos endereços IP. Na GUI, do NxCloud, o operador cria um usuário e associa o mesmo a um IP privado ou range de IPs em sua rede para aquele usuário. Agora os usuários associados aquele IP ou range de endereços estará subordinado a política definida ao mesmo usuário criado na GUI do NxCloud.

Scripts inclusos
----------------

Em ''/opt/nxrelay/bin' existem diversos scripts.


Para o Linux/BSD :

  - startup.sh - Ativa o serviço.
  - shutdown.sh - Para o serviço.
  - test.sh - Testa a conectividade com o NxCloud, de acordo com os parâmetros definidos no arquivo de configuração.
  - ping.sh - Testa se o serviço do NxRelay está ativo.

Para o Windows,

  - instsvc.bat - Para instalar o serviço 'NxRelay'.
  - unstsvc.bat - Para remover o serviço 'NxRelay'.


Já para o Ubuntu é disponibilizado também o script para o Systemd em ''/opt/nxrelay/script'',
nxrelay.service
