Quando o NxFilter não Inicializa
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Quando o NxFilter não inicializa, a primeira coisa a se verificar é o conteúdo do arquivo de log, geralmente fica em ``/nxfilter/log/nxfilter.log``. Nesse arquivo é possível encontrar a possível causa do problema. 

Outra parte importante a se verificar é se não está havendo conflito de portas e a instalação do Java. O NxFilter usa as portas: UDP/53, TCP/80, TCP/443, TCP/19001. Para o Cluster usa ainda as portas: TCP/19002, TCP/19003, TCP/19004. Isto por que além do NxFilter ser um servidor DNS e Web ( por conta das páginas de administração, autenticação e bloqueio ), ele tem as portas próprias para comunicação entre os serviços. Então, caso haja algum outro servidor DNS ou Web rodando no mesmo servidor o NxFilter não inicializará ou inicializará de modo incorreto.

Sobre a instalação Java, se você usa o instalador do NxFilter para Windows, na marioria dos casos você não terá problema algum, porém, se você instalar o NxFilter de modo manual ou inicializá-lo manualmente sem usar o gestor de serviços do Windows você pode encontrar alguns problemas relacionados ao Java. Para evitar esse tipo de problema o Java deverá ser instalado previamente e você tem de configurar de maneira correta as variáveis de ambiente para o Java.

Se você está em um ambiente Windows com o Java configurado corretamente, você receberá a seguinte mensagem ao digitar ``java`` na linha de comando.


.. image:: /images/cmd_java_ok.png

No ambiente Windows você deverá ter as seguinte variáveis:

  JAVA_HOME = C:\Program Files\Java\jre7
  PATH = %JAVA_HOME%\bin;C:\bin

Se está usando um Sistema Operacional Linux, NxFilter tentará encontrar primeiro o `java` em ``/usr/bin`` e depois em ``/usr/local/bin`` então caso não haja o comando ``java`` nesses diretórios você precisa alterar o scripts em ``/nxfilter/bin`` ou definir a variável ``JAVA_HOME`` com o caminho correto.

Para configurar a variável `PATH` para o Java você pode seguir os passos em `http://java.com/en/download/help/path.xml`. 

