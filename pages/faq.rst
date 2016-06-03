.. _faq:

***
FAQ
***

Perguntas frequentes sobre o NxFilter

Posso burlar o NxFilter usando endereço IP para acessar sites
**************************************************************
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

Como obrigar os usuários a usarem o NxFilter?
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

Tenho de usar a correspondência extada do que estou pesquisando no log ?
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

.. note::

  Para mudar a porta HTTPS modifique a linha `https_port = 443` em '/nxfilter/conf/cfg.properties', alterando 443 para outra porta que não a padrão.

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

Em '/nxfilter/bin/startup.sh' na chamada do java, onde tem os parâmtros da JVM, insira o seguinte parâmetro `-Duser.timezone=America/Fortaleza`.

 .. warning::

  No CentOS esse procedimento geralmente é necessário. 

 .. note::

  'America/Fortaleza' foi um exemplo, você pode ver a que se aplica melhor a sua região em ``http://www.ibm.com/support/knowledgecenter/ssw_i5_54/rzamy/reftzval.htm``.

Meus Browsers ficam fechando e abrindo após o NxClient iniciar
****************************************************************

O Agente NxClient atua como um proxy local, entáo ele precisa atualizar as configurações de proxy de modo a redirecionar o tráfego HTTP/HTTPS dos browsers de suas máquina para ele mesmo. E após essas configurações de proxy serem aplicadas é necessário reiniciar os browsers de modo a aplicar essas alterações. 

Mas você pode ter outro programa no seu Windows bloqueando tais configurações/atualizações ou fazendo as modificações ele mesmo. 

Você terá um conflito nesse ponto. Para corrigir isso você precisa deixar habilitado apenas um dos programas.
