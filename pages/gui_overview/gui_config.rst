**********************************
GUI - Config 
**********************************

Área com os principais parâmetros de configuração do NxFilter.

Config > Setup > Block and Authentication
*****************************************

.. envvar:: Block Redirection IP

  É o endereço IP do próprio NxFilter. Se houver alguma requisição de um domínio bloqueado, ele será redirecionado para este endereço IP. Geralmente ele é preenchido automáticamente durante o processo de instalação.

.. note::
  Para adicionar mais de um endereço IP separe-os por vírgulas. Isso pode ser usado em caso de redundância ou cluster.

.. envvar:: External Redirection IP

   Quando usar um agente remoto para filtrar requisições DNS ( como o NxClient ) você pode precisar usar um IP diferente do inserido em `Block Redirection IP` para casos onde o agente esteja sendo executado fora da sua rede. Deixando esse campo vazio o sistema usará mesmo registrado em `Block Redirection IP` para redirecionar requisições do agente remoto

.. envvar:: IPv6 Redirection IP

  É preciso definir esse endereço quando NxFilter é usado como servidor DNS na rede IPv6.

.. envvar:: Enable Authentication

 Essa opção deve ser ativada quando é utilizado algum método de autenticação, inclusive Autenticação vinculada a IP. 

 Após habilitar está opção, qualquer usuário ainda não autenticado será direcionado para a página de login. Desse modo só conseguirão navegar na internet após se autenticar.

.. envvar:: Login Domain

 URL para a página de login.

.. note::
  ex) login.nxfilter.org

.. envvar:: Logout Domain

  URL para forçar o término da sessão do usuário.

.. note::

  ex) logout.nxfilter.org

.. envvar:: Login Session TTL

  NxFilter mantém a sessão do usuário por um tempo determinado. Isso pode ser necessário para casos em que o computador seja compartilhado com outras pessoas, desse modo não haverá requisições DNS por um determinado tempo. 

  Atingindo o tempo definido nesse parâmetro a sessão do usuário expira e ele precisará se autenticar novamente.

Config > Setup > Syslog
***********************

O NxFilter permite que se exporte os registros para um Servidor Syslog. Você pode montar seu próprio sistema de relatórios ou pode monitorar todos os registros em real-time.


.. envvar:: Syslog Host

  Endereço do servidor para o qual serão enviados os dados.

.. envvar:: Syslog Port

  Porta UDP usada para se comunicar com o servidor.

.. envvar:: Export Blocked Only

  Enviar somente os registros de bloqueios.


.. envvar:: From Each Node

  Por padrão, o cluster NxFilter envia os dados para o Syslog apenas pelo nó Master. Ativando essa opção, cada nó envia seus próprios dados.

.. envvar:: Enable Remote Logging

  Ativar o envio para o Servidor Syslog definido em `Syslog Host`.

Config > Setup > NetFlow
************************

O sistema tem suporte a controle de banda. Isso é possível através da importação de dados do NetFlow.

Para mais detalhes leia em `Controle de Banda` neste mesmo tutorial.

.. envvar:: Router IP

  O endereço IP do servidor que enviará os dados NetFlow ao NxFilter.

.. envvar:: Listen Port

  Porta do coletor NetFlow ( Protocolo UDP ).

.. envvar:: Run Collector

  Ativar o coletor. Após alterar esse parâmetro é necessário reiniciar o NxFilter.

Config > Setup > Misc
***********************

.. envvar:: Admin Domain

  URL para acesso a GUI de administração do NxFilter. Se, por exemplo, você registrar `admin.nxfilter.org` a área de administração será acessível através do endereço `http://admin.nxfilter.org/admin`.

.. note::
  
  Isso só funcionará quando você estiver usando o NxFilter como seu servidor DNS. Caso contrário você precisará registrar o domínio em seu próprio servidor DNS.

.. envvar:: Bypass Microsoft Update
 
  Caso sua rede tenha estações Windows essa opção permite que os updates não sejam bloqueados. Habilitando esta opção os domínios e subdomínios `microsoft.com`  e `windowsupdate.com` não exigirão autenticação nem será bloqueados.

.. envvar:: Logging Retention Period

  Tempo em que os registros ficarão armazenados.

.. warn::

  Períodos muito longos de armazenamento ocupam muito espaço em disco e lentidão na geração de relatórios.

.. envvar:: SSL Only to Admin GUI

  Forçar que o acesso a área de administração seja feito apenas através de HTTPS/Página segura. Uma vez que esta opção seja habilitada você será redirecionado para o endereço HTTPS automáticamente, mesmo que esteja colocando o endereço HTTP.

.. envvar:: Auto Backup

  Backups são executados todos os dias a '01:00' e ficam gravados na pasta '/nxfilter/backup'. Os arquivos de backup terão o prefixo 'auto-'.

.. envvar:: Agent Policy Update Period

  Os agentes disponibilizados pelo NxFilter baixam suas políticas periodicamente. Essa frequência é determinada por esse parâmetro.

Config > Admin
***************

Você pode alterar o usuário administrador e a senha da GUI de administração aqui.

.. note::

   'Client Password' é para configurações de agentes remotos para filtragem. Ele tem sido usado para acessar a página de configuração do NxBlock

Config > Alert
***************

NxFilter envia um email de alerta informando dos blocks recentes ou caso algum nó do cluster caia. 

Por exemplo, caso deseje enviar um email de alerta para 'admin @ nxfilter.org' de 'alert200 @ gmail.com' a cada 15 minutos a configuração seria :

- Admin email : admin @ nxfilter.org

- SMTP host : smtp:gmail.com

- SMTP host : 465

- SMTP SSL : on

- SMTP user : alert200

- SMTP password : ********

- Alert period : Every 15 minutes

Config > Allowed IP
***********************

NxFilter permite que se faça restrição de acesso baseado em IP para funcionalidades como serviço DNS, GUI ou redirecionamento para login. Isso pode ser útil quando NxFilter é utilizado com endereço de IP público. Você pode fazer uma ACL com permissões e exclusões nessa área.

Config > Backup
***************

Forçar o backup das configurações. Os arquivos ficarão gravados em '/nxfilter/backup'.

Config > Block Page
*******************

Personalização da pagina de bloqueio, login e boas vindas. Quando editar a página de bloqueio podem ser usados os seguintes parâmetros caso deseje deixar a página com mais informações.

- #{domain} : Domínio bloqueado
 
- #{reason} : Motivo do bloqueio
 
- #{user} : Usuário autenticado
 
- #{group} : Grupos aos quais o usuário pertence

- #{policy} : Que política foi aplicada
 
- #{category} : Categorias em que se enquadra ou o domínio bloqueado

Config > Cluster
*****************

NxFilter tem a possibilidade de trabalhar em cluster. Você pode ativar seu NxFilter como um nó principal ou secundário em um Cluster. Após alterações na configuração do cluster você precisa reiniciar seu NxFilter para que as mudanças sejam aplicadas.

