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
Insira '*.facebook.com' em 'Whitelist > Domain' e marque a opção 'Admin Block'.

Desejo bloquear o 'facebook.com' apenas para um determinado grupo
*****************************************************************
Antes é necessário separar de algum modo seu grupo de outros usuários usando a parte de autenticação do NxFilter. Daí bloquear a categoria de 'Social Networking' em uma política quando estiver usando a Jahaslist. O último passo seria atribuir essa política ao grupo desejado.

Se houver o interesse em permitir, por exemplo, que o grupo de 'Vendas' possa usar a internet sem bloqueios no horário de almoço.

Crie um usuário ou um grupo e defina o horário livre em 'Políticas e Regras > Horário Livre' então atribua a política de horário que mais convier para esse grupo.

Como alterar a porta do servidor web do NxFilter?
*************************************************************
Você pode mudar as portas HTTP/HTTPS do NxFilter. Porém ao mudar a porta HTTP você perderá a página de bloqueio para o caso de redirecionamento. Isso ocorrerá por conta do NxFilter redirecionar o usuário - quando necessário - para algo no browser do usuário na porta TCP/80.

Para fazer a alteração das portas você precisa mudar os seguintes parâmetros em '/nxfilter/conf/cfg.properties'.

http_port = 80
https_port = 443

Após a mudança de portas reinicie o NxFilter.


Como resetar a senha de administrador?
*************************************************************

Existe o script `/nxfilter/bin/reset_pw.sh` para resetar a senha de administrador. Uma vez executado o script, o nome e a senha do administrador será resetada para o padrão de instalação. Esse script deve ser executado enquando o NxFilter está em execução.

 .. note::
  Há também o script '/nxfilter/bin/reset_acl.sh' que reseta as resitrições de acesso ao GUI.

Can I bind NxFilter to a specific IP address?
*************************************************************
You might want to bind NxFilter to a specific IP address to avoid of having a port collision problem. You can bind NxFilter to a specific IP address using 'listen_ip' parameter in '/nxfilter/conf/cfg.properties' file. If you set it to '0.0.0.0' NxFilter will listen on all the IP addresses of the system but if you set it to a specific IP address NxFilter will listen on the specified IP address only.
* Even if you bind NxFilter to a specific IP address you can not run multiple NxFilter on the same machine. This is because NxFilter needs to bind several ports on localhost for internal communication.

How do I bypass my local domain?
*************************************************************
On 'DNS > Setup' You can set your local DNS server and local domain. With this setup if there are DNS queries for your local domain NxFilter forwards the queries to the local DNS server and bypass authentication, filtering and logging.

Can I use an exact matching keyword for log search?
*************************************************************
You can use square brackets for exact matching on log search.
    ex) [john], [192.168.0.1]

Why do I need to re-login after lunch break?
*************************************************************
Your login session has been expired. If there is no activity(DNS query) from your PC for a certain time your login session expires. You can increase 'Login Session TTL' on 'Config > Setup'.
* If you use single sign-on with Active Directory you can avoid of having this problem.

How do I apply my own SSL certificate?
*************************************************************
We use an embedded Tomcat 7.x as the built-in webserver for NxFilter. If you want to apply your own SSL certificate with Tomcat there are two parameters you need to set in Tomcat config file. One is 'keystoreFile' and the other one is 'keystorePass'. However we don't have a separated config file for Tomcat. We use '/nxfilter/conf/cfg.properties' file to set these parameters.
keystore_file = conf/myown.keystore
keystore_pass = 123456
* About how to build keystore file read Tomcat manual.

How do I enable debug mode?
*************************************************************
When there is something wrong with NxFilter the first thing you can do is to find out what is going on exactly with its log data. NxFilter keeps its system log data inside '/nxfilter/log' directory. If you need more detailed log data, enable debug mode on '/nxfilter/conf/log4j.properties'. Change 'INFO' to 'DEBUG' inside the file and restart NxFilter.

Como oculto o alerta de SSL?
****************************
Quando um browser está sendo redirecionado para HTTPS ele alerta o usuário que isso está ocorrendo. Tem o objetivo de prevenir o ataque `Man in the middle <https://pt.wikipedia.org/wiki/Ataque_man-in-the-middle>`_. Por esse motivo que é recebida a mensagem de alerta ao invés da tradicional página de bloqueio do NxFilter. Seu browser está apenas fazendo o que deve ser feito e não é o objetivo do NxFilter interferir nisso.
Em todo caso há situações em que se deseja ocultar essa página de alerta. Para que isso ocorra pode se mudar a porta HTTPS do NxFilter, desse modo os usuários receberão a mensagem de "Erro de Conexão".
 .. note::
  Para mudar a porta HTTPS modifique a linha `https_port = 443` em '/nxfilter/conf/cfg.properties', alterando 443 para outra porta que não a padrão.

I don't see any username on 'Logging > Request'.
*************************************************************
The first thing you need to check would be 'Enable Authentication' option on 'Config > Setup'. Some people don't understand that they need to enable authentication before implementing any authentication method.

How do I bypass logging completely?
*************************************************************
For internal purposes, the minimum log retention period you can set is 3 days. But you can bypass logging completely by setting 'syslog_only' option on '/nxfilter/conf/cfg.properties' file. If you set this option without having Syslog exportation setup then NxFilter bypasses logging and not sending Syslog data as it doesn't know where to send it.
To enable 'syslog_only' option add the following line on '/nxfilter/conf/cfg.properties' file,
syslog_only = 1
* You still get the counting data but the actual logging data will not be stored into your traffic DB.

Como alterar o timezone?
*************************
Alguns usuários sentiram necessidade de usar um timezone diferente do usado no NxFilter. Acontece geralmente no CentOS. Quando houver a necessidade de mudar o timezone de forma manual isso pode ser feito mudando os parâmetros da JVM.
Em '/nxfilter/bin/startup.sh' na chamada do java, onde tem os parâmtros da JVM, insira o seguinte parâmetro `-Duser.timezone=America/Fortaleza`.
 .. note::
  'America/Fortaleza' foi um exemplo, você pode ver a que se aplica melhor a sua região em `<http://www.ibm.com/support/knowledgecenter/ssw_i5_54/rzamy/reftzval.htm>`.

My Browsers keep restarting after NxClient starting.
*************************************************************
NxClient is a local proxy so it needs to update the system proxy settings to redirect HTTP/HTTPS traffic of your browsers to itself. And after it updates the proxy settings it needs to restart the browsers to apply the changes. But you might have another Windows program preventing the update or doing the update for itself. You have a race condition here. To fix it, you have to disable one of them.
