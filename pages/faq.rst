.. _faq:

***
FAQ
***

Perguntas frequentes sobre o NxFilter

Posso burlar o NxFilter usando endereço IP para acessar sites?
***************************************************************
Existem casos de pessoas dizendo que filtros DNS não são práticos por poder se acessar um website usando seu endereço IP. Esta é uma afirmação nem sempre é correta. Atualmente muitos servidores de sites estão rodando com Virtual Host, deste modo diversos sites respondem no mesmo endereço IP. Por isso nem sempre é possível acessar sites diretamente sem usar o respectivo domínio.

Outra coisa para se ter em mente é que existem muitas URLs em uma página só ( endereço de css, endereço de imagem, etc... ). Isso se aplica mais ainda se estivermos falando de algum portal. E essas URLS são baseadas em endereço DNS. É como se você pudesse tentar acessar um site bloqueado usando IP porém o que você obtem é uma página com erros.

 .. note::
   NxFilter pode bloquear IP usando o agente de proxy.

Mesmo tendo alterado o NxFilter continua bloqueando/permitindo o acesso ao site
*******************************************************************************

É provável que seja o cache DNS do seu sistema interferindo. 
Se você está usando o Windows saiba que nele existem dois tipos de cache DNS:
  1. O do Browser
  2. O do próprio Windows
Digamos que antes do cache expirar foi alterada a política no NxFilter bloqueando/permitindo o acesso ao site. O cache só vai expirar em um determinado momento, porém é possivel forçar a limpeza do cache imediatamente.

Para limpar o cache do Browser feche o mesmo completamente, todas as janelas e depois reabra o sistema.

Para limpar o cache DNS do Windows, execute o seguinte comando no prompt, vulgo CMD `ipconfig /flushdns`.

Geralmente o cache DNS do Windows expirar no máximo em 1 dia. É claro que isso também depende do TTL do registro definido pelo DNS, mas ainda não tivemos registros de TTLs superiores a 1 dia - ou 86400 segundos.

Quanto ao cache DNS no Browser o registro DNS pode levar vários minutos para expirar. Porém ele irá expirar e receberá a nova política definida no NxFilter.

  .. note::
    Na prática isso não será um problema, já que não é comum executar esse procedimento de bloqueio/desbloqueio várias vezes ao dia.

Como obrigar o usuário a usar o NxFilter?
*********************************************
Havendo um firewall em sua rede esse é um procedimento simples. Só é preciso bloquear a saída UDP/53 e TCP/53 de outros que não sejam o NxFilter. E então você pode usar o DHCP para registrar no cliente o NxFilter como servidor DNS na sua rede. Desse modo o NxFilter se tornará seu único servidor DNS que seus usuários poderão utilizar e a parte DHCP deixará isso configurado de modo automático.

Como o NxFilter determina que política aplicar a um usuário?
*************************************************************
Você pode atribuir uma política diretamente a um usuário. Se o usuário pertence a um grupo, então a política do grupo sobrepõe a política do usuário.
Porém quando você importa usuários do Active Directory eles podem pertencer a diversos grupos. Nesse caso você não saberia que política seria aplicada a determinado usuário.
Para resolver esses problema use a feature 'Priority Points'. Se há mais de um grupo e se eles tem políticas diferentes, a política que tiver a maior pontuação em prioridade será aplicada. Você pode definir essa pontuação em um política.

 .. note:: Para saber que política está sendo aplicada a um determinado usuário, utilize o botão 'TEST' em 'User & Group > User'.

Qual forma mais rápida de bloquear 'facebook.com'?
**************************************************

Insira ``*.facebook.com`` em 'Whitelist > Domain' e marque a opção 'Admin Block'.

Desejo bloquear o 'facebook.com' apenas para um determinado grupo
*****************************************************************

Antes é necessário separar de algum modo seu grupo de outros usuários usando a parte de autenticação do NxFilter. Daí bloquear a categoria de 'Social Networking' em uma política quando estiver usando a Jahaslist. O último passo seria atribuir essa política ao grupo desejado.

Se houver o interesse em permitir, por exemplo, que o grupo de 'Vendas' possa usar a internet sem bloqueios no horário de almoço.

Crie um usuário ou um grupo e defina o horário livre em 'Políticas e Regras > Horário Livre' então atribua a política de horário que mais convier para esse grupo.

Como alterar a porta do servidor web do NxFilter?
*************************************************************

Você pode mudar as portas HTTP/HTTPS do NxFilter. Porém ao mudar a porta HTTP você perderá a página de bloqueio para o caso de redirecionamento. Isso ocorrerá por conta do NxFilter redirecionar o usuário - quando necessário - para algo no browser do usuário na porta TCP/80.

Para fazer a alteração das portas você precisa mudar os seguintes parâmetros em ``/nxfilter/conf/cfg.properties``.

.. code-block:: jproperties 

    http_port = 80
    https_port = 443

Após a mudança de portas reinicie o NxFilter.


Como resetar a senha de administrador?
*************************************************************

Existe o script `/nxfilter/bin/reset_pw.sh` para resetar a senha de administrador. Uma vez executado o script, o nome e a senha do administrador será resetada para o padrão de instalação. Esse script deve ser executado enquando o NxFilter está em execução.

.. note::

  Há também o script ``/nxfilter/bin/reset_acl.sh`` que reseta as resitrições de acesso ao GUI.

Posso vincular o NxFilter a um determinado endereço IP?
*************************************************************

Em casos como conflitos de portas é possível vincular o NxFilter a um IP específico. Isso pode ser feito usando o parâmetro ``listen_ip`` em `/nxfilter/conf/cfg.properties`. Se estiver setado ``0.0.0.0`` o NxFilter irá responder em todos os endereços IPs do sistema mas se for especificado o IP o NxFilter só responderá nesse.

.. note::

  Mesmo que se vincule o NxFilter a um determinado endereço IP você não poderá ter multiplas instâncias do NxFilter na mesma máquina. Isso ocorre por que ele precisa se vincular a diversas portas no servidor para comunicação interna.

Como fazer o bypass do meu domínio local?
*************************************************************

Em ``DNS > Setup`` você pode registrar seu servidor DNS interno e domínio local. Nessa configuração se houverem consultas DNS ao domínio local o NxFilter direciona as consultas para o servidor DNS local e não exige autenticação, filtro e/ou registro.

Tenho de usar a correspondência exata do que estou pesquisando no log ?
*************************************************************************
Você pode separar por colchetes para fazer um filtro mais preciso na pesquisa do log.

.. code-block:: jproperties 

    ex: [john], [192.168.0.1]

Por que preciso autenticar novamente após a parada para almoçar?
****************************************************************
Sua sessão expirou. 

Não havendo atividade ( consultas DNS ) vindas do seu terminal de trabalho por um determinado tempo sua sessão expira. Você pode aumentar o tempo em 'Login Session TTL' em 'Config > Setup'.

 .. note::
  Se você usar o modo SSO com o AD você pode evitar esse tipo de problema.

Como aplicar meu próprio certificado SSL?
*************************************************************
O NxFilter usa o Tomcat 7.x de modo embarcado para ser o servidor de páginas. Se você deseja aplicar seu próprio certificado SSL no Tomcat há dois parâmetros que você precisa definir no arquivo de configuração dele.

Os dois parâmetros são `keystorefile` e `keystorePass`. Em todo caso não há um arquivo separado só para configurar o Tomcat. Será utilizado o `/nxfilter/conf/cfg.properties` para definir esses parâmetros.

.. code-block:: jproperties

   keystore_file = conf/minha.keystore
   keystore_pass = 123456

.. note::

  Para saber como gerar o arquivo keystore leia o manual do Tomcat 7.x

Como habilitar o modo de debug?
*************************************************************
Quando há algo de errado com o NxFilter a primeira coisa recomendade é verificar os logs. NxFilter mantém registros de log dentro da pasta `/nxfilter/log`.

Caso precise de informações mais detalhadas sobre o erro, habilite o modo de debug em `/nxfilter/conf/log4j.properties`, alterando o trecho `INFO` para `DEBUG` dentro do arquivo e reinicie o NxFilter

.. warning::

   Após identificar o erro ou terminar de analisar os logs não esqueça de alterar isso novamente para o padrão `INFO` pois pode acabar gerando muito log e encher sua unidade de disco de modo acelerado.

Como oculto o alerta de SSL?
****************************
Quando um browser está sendo redirecionado para HTTPS ele alerta o usuário que isso está ocorrendo, pois tem o objetivo de prevenir o ataque `Man in the middle <https://pt.wikipedia.org/wiki/Ataque_man-in-the-middle>`_. Por esse motivo que é recebida a mensagem de alerta ao invés da tradicional página de bloqueio do NxFilter. Seu browser está apenas fazendo o que deve ser feito e não é o objetivo do NxFilter interferir nisso.

Em todo caso há situações em que se deseja ocultar essa página de alerta. Para que isso ocorra pode se mudar a porta HTTPS do NxFilter, desse modo os usuários receberão a mensagem de "Erro de Conexão".

Agora é possível ocultar o Alerta do SSL porém existe um problema nessa abordagem. Alguns usuários informaram que a navegação ficou mais lenta já que é preciso aguardar o timeout de alguns websites. Então agora é permitido usar o parâmetros 'hide_ssl_warning'.

.. code-block:: jproperties

   hide_ssl_warning = 1

Ao ativar essa função no arquivo config.properties, o controle de timeout será aplicado imediatamente.

.. note::

  Caso deseje acessar a GUI usando HTTPS quando ativar a opção ''hide_ssl_warning'' é necessário mudar a porta padrão 443 em ''https_port'' para uma outra porta fora do padrão. Caso contrário a requisição HTTPS retornará timeout imediatamente.
  
  Já para o Chrome é possível exibir a página de bloqueio no HTTPS usando o NxForward. Para saber mais, acesse o tópico do :ref:`NxForward <nxforward>` neste mesmo tutorial.
   

Não vejo o nome do meu usuário em 'Logging > Request'
*************************************************************

A primeira coisa que você precisa ativar é 'Habilitar autenticação' em 'Config > Setup'. 

As vezes passa despercebido que é necessário ativar a autenticação antes de fazer uso de qualquer coisa que dependa do método de autenticação.

Como evitar qualquer registro de log?
*************************************************************

O tempo minimo de retenção de registros é de 3 dias.

Mas caso não deseje registrar nada é possível burlar isso definindo o parâmetro `syslog_only` em `/nxfilter/conf/cfg.properties`. Se esse parâmetro for registrado no arquivo sem ter nenhum valor o NxFilter não registrará nada.

Para ativar o `syslog_only` insira a o seguinte registro em `/nxfilter/conf/cfg.properties`:

.. code-block:: jproperties 

    syslog_only = 1

.. note::

   Você continuará tendo as contagens mas o registro dos dados não serão armazenados em sua tabela de tráfego.

Como alterar a timezone?
*************************
Alguns usuários sentiram necessidade de usar um timezone diferente do usado no NxFilter. 

Quando houver a necessidade de mudar o timezone de forma manual isso pode ser feito mudando os parâmetros da JVM.

Em '/nxfilter/bin/startup.sh' na chamada do java, onde tem os parâmtros da JVM, insira o seguinte parâmetro ``-Duser.timezone=America/Fortaleza``.

 .. warning::

  No CentOS esse procedimento geralmente é necessário. 

 .. note::

  'America/Fortaleza' foi um exemplo, você pode ver a que se aplica melhor a sua região em ``http://www.ibm.com/support/knowledgecenter/ssw_i5_54/rzamy/reftzval.htm``_ .

Meus Browsers ficam fechando e abrindo após o NxClient iniciar
****************************************************************

O Agente NxClient atua como um proxy local, entáo ele precisa atualizar as configurações de proxy de modo a redirecionar o tráfego HTTP/HTTPS dos browsers de suas máquina para ele mesmo. E após essas configurações de proxy serem aplicadas é necessário reiniciar os browsers de modo a aplicar essas alterações. 

Mas você pode ter outro programa no seu Windows bloqueando tais configurações/atualizações ou fazendo as modificações ele mesmo. 

Você terá um conflito nesse ponto. Para corrigir isso você precisa deixar habilitado apenas um dos programas.

Como forçar o usuário a fazer o logout?
****************************************
Não existe essa função na GUI. Porém, em muitos casos, as pessoas desejam forçar esse término de sessão quando os usuários deixam de usar seus terminais e desejam forçar que o próximo usuário se autentique. Para isso você pode usar a opção de logout do domínio em 'Config > Setup'. Você escreverá um script batch para o browser acessar o endereço assim que o usuário fizer o logoff.

.. code-block:: bash
   @echo off
   start http://logout.example.com

Ou você pode usar o sinal de logout do endereço que é 'logout.signal.nxfilter.org'. Verifique esse endereço usando o aplicativo 'nslookup' e a sessão de login associada ao IP dessa estação será excluído.

.. code-block:: bash

  @echo off
  nslookup logout.signal.nxfilter.org.

NxFilter deixa de funcionar após o erro 'Queue full'
******************************************************

Ao receber a mensagem de erro 'Queue full' você perde a conexão com a internet ou com o servidor DNS Upstream. Isso ocorre por que o NxFilter não consegue processar as requisições DNS em sua fila. 

Entende-se que o NxFilter deveria retormar as funcionalidade quando sua conexão é restaurada. Em todo caso em alguns sistemas o processamento nao volta a ocorrer após o retorno da conexão. E o problema é que apesar do sistema informar que está conectado não é isso que esteja ocorrendo e como a conexão é UDP não tem como confirmar. Esse problema não ocorre em todas as instalações do NxFilter e apesar de nossas tentativas, ainda não conseguimos repetir o problema em nossos laboratórios, dificultando assim a identificação da causa.

A solução para isso, temporariamente, é reiniciar o NxFilter. E seria muito interessante se fosse possível reiniciar o NxFilter assim que receber a devida mensagem de erro 'Queue full'. Na versão 3.4.4 foi introduzido o parâmetro 'queue_full_exit' em ''/nxfilter/conf/cfg.properties''.

No arquivo haverá a seguinte linha:

.. code-block:: jproperties

   queue_full_exit = 1

Assim o NxFilter fechará automaticamente ao receber a mensagem de erro 'Queue full' e você poderá reinicia-lo. Por exemplo, se estiver em um sistema Linux você pode usar a opção 'respawn' no Upstart ou no Systemd para reiniciar o NxFilter.


Como restringir acesso a resultados com conteudo pornografico no Google e/ou Youtube?
***************************************************************************************

No NxFilter você pode obrigar o uso de pesquisas com o ''safe-search' ativado. No NxFilter tem a opção 'Safe-searc' na política.

.. note::

 - Para usar o Safe-search no Yahoo é necessário ter o agente de proxy local instalado na área do usuário.

 - Os modos 'Moderate' e 'Strict' só interferem nas pesquisas do Youtube.


O que é o erro 'Too many requests' ?
**************************************

Foram registrados diversos casos de uso inadequado do NxFilter atrás de um roteador, por isso foi adicionada a verificação por contagem de requisições. Segundo nossas análises, um usuário faz pouco mais de 1.000 requisições ao dia, dando uma margem de mais 2.000 requisições chegamos ao limite de 3.000 requisições por dia.

Sendo assim mais do que suficiente para a maioria dos casos de uso, já que em diversas empresas a quantidade de requisições fica abaixo de 1.500 por usuário ao dia.

Essa proteção da licença por quantidade de requisições é altamente necessário por conta de nossos contratos de parceria com soluções nas nuvens, já que eles poderiam ter contratos onde milhares de clientes usariam o mesmo usuário e esgotariam o recurso dos mesmos. Ou seja essa proteção não é só para os nossos negócios, ela protege também nossos clientes comerciais.

.. note::

   Temos os parâmetros de 'request-sum' e 'request-cnt'. O 'request-cnt' é utilizado para essa validação.
 
   São contadas apenas as consultas DNS to tipo 'A'.

   Antes de adquirir sua licença é possível acessar o relatório em 'Report > Usage' para ter ideia das quantidades de licenças necessárias. Esse relatório exibe os últimos 30 dias de uso.

