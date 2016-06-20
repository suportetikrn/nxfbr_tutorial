Ajustes de performance
*************************

Apesar do Serviço do NxFilter ser concebido para atender milhares de usuários facilmente, existem vários fatores que podem ser ajustados para atingir melhor performance do NxFilter caso seja necessário.

Memory size
^^^^^^^^^^^^

Por padrão NxFilter usa cerca de 512 MB RAM. É o suficiente para a maioria dos casos. Mas se você alocar mais memória para o NxFilter você terá uma performance maior ainda.

No script de inicialização do serviço do NxFilter `/nxfilter/bin/startup.bat` você tem a linha.
 ::
    java -Djava.net.preferIPv4Stack=true -Xmx512m -cp "%NX_HOME%"\nxd.jar;"%NX_HOME%"\lib\*; nxd.Main

Se desejar aumentar para 1GB mude o parâmetro `-Xmx512m` para `-Xmx1024m`.

.. note::
   Case estejas usando o NxFilter como um serviço no Windows, é necessário reinstalar o serviço com esse ajuste de memória. Quando for reinstalá-lo, desinstale usando `unstsvc.bat` altere o arquivo `instsvc.bat` com o ajuste de memória desejado e aí sim reinstale executando `instsvc.bat`.

Espaço em disco e redução do volume de dados de log
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxFilter tem várias modalidades de relatórios. Você pode ver todos os registros de acesso diários, semanais e por usuário. Em todo caso este tipo de relatório consome muito espaço em dico. É possível que note uma degradação na performance quando atingir um volume muito grande de registros nos relatórios.

Se na sua rede tem centenas de usuários é interessante ter no mínimo 10GB reservados só para os registros de tráfego. Ou para economizar espaço em disco é possível reduzir a quantidade de dados. Para reduzir é possível ajustar o valor em 'Log Retention Days' em 'Config > Setup'.

A outra forma de reduzir o volume de dados de tráfego é fazer uma lista branca/whitelist com a opções 'Bypass Logging' para os domínios que não tem interesse em registrar.

Usar cache no cliente para consultas DNS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxFilter manipula o TTL do DNS cache para que o cliente DNS limpe os registros o mais rápido possível, de modo que as atualizações/ajustes nas políticas sejam aplicadas mais rapidamente. Porém essa não uma funcionalidade tão crítica e ela aumenta o número de consultas vindas dos clientes.

Para melhorar a performance você pode achar interessante que o NxFilter não altere o TTL dos registros no DNS Cache.

Pode alterar o parâmetro 'Max Client Cache TTL' em `Config > Setup` para `0`, desligando assim a funcionalidade. Quando isso é desligado o sistema cliente não não fará consultas DNS enquanto o registro estiver no cache e assim reduzirá a carga para o NxFilter drásticamente. Quando há mais de 1.000 usuários é recomendado desligar esta funcionalidade.
 
Aumentar o número de threads de requisições
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxFilter é um sistema multi-thread. Ele tem threads que atendem as requisições DNS dos clientes. A quantidade de threads padrão é 8 e é suficiente em muitos casos. Mas se acha que o NxFilter está demorando a responder você pode aumentar essa quantidade.

Para aumentar para 16 threads insira a seguinte linha em `/nxfilter/conf/cfg.properties` e reinicie o NxFilter.

.. code-block:: jproperties

    rh_num = 16

Usando um servidor DNS recursivo internamente
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Um dos motivos que podem causar degradação na performance do NxFilter é a latência do servidor upstream ( servidor DNS que o NxFilter consulta ). Não é um caso para quando há centenas de usários já que o NxFilter tem seu próprio cache. Porém se sua rede tem milhares de usuários, isso pode ser um problema. Por isso foi criado o parâmetro `Local DNS Server`.

Mas isso não quer dizer que o NxFilter não consiga fazer consultas recursivas no DNS. Em vez de instalar um servidor DNS recursivo 
However this doesn't mean that NxFilter does recursive DNS query by itself. Rather you install a recursive DNS server into the server having NxFilter already installed and make NxFilter uses it as its upstream DNS server. 

Caso tenha instalado algo como o servidor de DNS recursivo  MaraDNS's Deadwood e configurado-o para usar a porta 10053 e o ip for `127.0.0.1` é preciso adicionar a seguinte linha em `/nxfilter/conf/cfg.properties`.

.. code-block::

    local_resolver_port = 10053

E reiniciar o NxFilter.

Desativando o compartilhamento de dados entre os clusters
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Quando há um cluster NxFilter, existe uma troca constante de dados entre eles visando o compartilhamento de dados. No caso do servidor ter um processamento alto isso pode ser um fator de degradação da performance.

Para diminuir o volume de troca de dados leia a seção `Criando um Cluster NxFilter` nessa mesma documentação.

