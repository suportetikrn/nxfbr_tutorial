Cluster com NxFilter
***********************

O NxFilter tem um sistema embutido para criar clusters com load balance e alta disponibilidade. Uma vez que você tenha um nó master você pode adicionar 4 nós slave no cluster.

Todos os nós slave em seu cluster recebem as configurações do nó master. Então você pode controlar tudo a partir do nó master.

Criando um cluster
^^^^^^^^^^^^^^^^^^

 Para criar um cluster, a primeira coisa a se fazer é configurar o nó master. Em 'Config > Cluster' você pode fazer com que uma de suas instalações do NxFilter seja o Master. E então você pode adicionar os outros NxFilter como os nós slave, vinculando-os ao seu nó master. Após definir o NxFilter como masteri ou qualquer alteração no cluster você precisa reiniciar os NxFilter.

.. note::

  O serviço de cluster requer que as portas 19002,19003 e 19004 que usam protocolo TCP sejam liberadas ( todas no nó master e demais )

Iniciando o NxFilter em cluster
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ao ativer o cluster NxFilter você precisa iniciar antes o nó principal e só em seguida os nós slave. Isso ocorre pois os nós slave tentarão baixar a configuração inicial a partir do nós principal assim que forem inicializados.


Load balance e alta disponibilidade 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Uma coisa boa sobre o filtr DNS é que o load balance (lb) e alta disponibilidade (ha) são nativos do sistema. Configure seu nó master como o DNS Primário e seu Slave como DNS Secundário na sua rede. Então você já tem tanto o load balance quanto a alta disponibilidade.

.. note::

  Se você deseja ter LB e HA nas páginas de bloqueio e login ou atualizações de politicas para os agentes do NxFilter você precisa definir diversos blocos de redirecionamento separados por vírgulas em 'Config > Setup'.

Quando um dós nós cair
^^^^^^^^^^^^^^^^^^^^^^

Quando um nó slave cai os outros nós não serão afetados.

Quando cai o nó master você ainda não perderá os filtros a menos que você reinicie seu nó slave antes de restaurar o nó master. Porém a diversas formas de evitar isso.

.. note::
 
 Se você configurar o alerta de email em 'Config > Alert' você receberá o aviso de que o nó caiu.

1. Redirecionamento do Login não funciona

  Quando o nó master cai não se consegue compartilhar as sessões de login entre os nós restantes. Isso significa que sua página de login não funcionará corretamente. Então seu usuário não será redirecionado para a página de login.

2. Usuários não autenticados passarão livremente

If we don't redirect the 'Password Users' to the login-page they can't login. But we don't want to let them lose the Internet.	So we bypass filtering for these unauthenticated users when the master node down. If you don't want to bypass filtering for any users even if your master node down try to have a default user covering whole IP range of your network.
* NxCloud's case is a bit different. It drops the requests from unauthenticated users as the login redirection is not the default option for NxCloud and the users on NxCloud mostly use the other authentication methods.
3. Multiple server IP addresses with an agent
If you use one of our agent programs with multiple server IP addresses to cover the slave nodes, they will still be working.
Access control for slave nodes
If you add all your slave node IP addresses into 'Config > Cluster' any attempt to join a slave node from an unknown source IP address will be blocked.
Monitoring slave node state
You can view connection state from your slave nodes on 'Config > Cluster'. Once you set up your cluster then your slave nodes will be appeared with the last contact time on the page. It is also showing each node's request, block, user, client-ip count information. These counter information will be set to 0 on midnight or when you restart NxFilter.
Session sharing between cluster nodes
We use TCP ports for sharing data between cluster nodes. The one of the data we share is the login session so that you don't need to login twice to master and slave node. And we share quota-time and bandwidth consumption data as well. But this could be a reason for performance degrading when you have busy servers as it increase the amount of communication between nodes.
If you don't want to share these data you can disable authentication and not to use quota-time and bandwidth control. But you may want to have authentication even if you need to login twice. And in reality, this login session sharing is only for the login-page. If you don't use password login you are not going to have any problem. NxLogon and NxMapper, NxClient can talk to multiple NxFilter servers. And IP based authentication works fine without session sharing.

Para desativar o compartilhamento de sessões enquanto a autenticação estiver ativa, insira o seguinte parâmetro em '/nxfilter/conf/cfg.properties'.

    no_share_session = 1

.. warning::
 Essa configuração 'no_share_session' tem de ser feita em todos os nós.
