Cluster com NxFilter
***********************

O NxFilter tem um sistema embutido para criar clusters com load balance e alta disponibilidade. Uma vez que você tenha um nó master você pode adicionar até 4 nós ''Slave'' no cluster.

Todos os nós slave em seu cluster recebem as configurações do nó master. Então você pode controlar tudo a partir do nó master.

Criando um cluster
^^^^^^^^^^^^^^^^^^

 Para criar um cluster, a primeira coisa a se fazer é configurar o nó master. Em 'Config > Cluster' você definir que uma de suas instalações do NxFilter seja o nó Master. E então você pode adicionar os outros NxFilter como nós ''Slave'', vinculando-os ao nó ''Master''. 

 Após definir o NxFilter como master, ou sempre que for feita qualquer alteração na parte de configuração do cluster, você precisa reiniciar os NxFilter.

.. note::

  O serviço de cluster requer que as portas 19002,19003 e 19004 - que usam protocolo TCP - sejam liberadas ( todas no nó master e demais )

Iniciando o NxFilter em cluster
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ao configurar o serviço de cluster no NxFilter, você precisa iniciar antes o nó principal ''Master'' e só em seguida os nós ''Slave''. Isso é necessário pois os nós ''Slave'' tentarão baixar as configurações iniciais a partir do nó ''Master'' assim que estes forem inicializados.


Load balance e alta disponibilidade 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Uma coisa boa sobre o filtro DNS é que o load balance (lb) e ia alta disponibilidade (ha) são funcionalidades nativas do sistema. Configure seu nó ''Master'' como o DNS Primário e seu ''Slave'' como DNS Secundário na sua rede. Então você já tem tanto o load balance quanto a alta disponibilidade.

.. note::

  Se você deseja ter LB e HA nas páginas de bloqueio e login ou atualizações de politicas para os agentes do NxFilter você precisa definir diversos blocos de redirecionamento separados por vírgulas em 'Config > Setup'.

Quando um dós nós cair
^^^^^^^^^^^^^^^^^^^^^^

 - Quando um nó slave cai os outros nós não serão afetados.

 - Quando cai o nó master você ainda não perderá os filtros a menos que você reinicie seu nó slave antes de restaurar o nó master. Porém há diversas formas de evitar isso.

.. note::
 
 Se você configurar o alerta de email, em 'Config > Alert', você receberá o aviso de que o nó caiu.

1. Redirecionamento do Login não funciona

  Quando o nó master cai não se consegue compartilhar as sessões de login entre os nós restantes. Isso significa que sua página de login não funcionará corretamente. Então seu usuário não será redirecionado para a página de login.

2. Usuários não autenticados passarão livremente

  Se não redirecionar as 'Senhas de usuários' para a página de login eles não poderão se autenticar. Mas no não desejamos fazer com que nossos clientes fiquem sem Internet. Então o filtro é desativado para os usuários sem autenticação para o caso do servidor Master cair. Se você não deseja desativar os filtros para todos os usuários então pro caso do master cair tente criar um usuário padrão para uma faixa de ip na sua rede.

.. note::

  Para o NxCloud é um pouco diferente. Ele cancela as requisições de usuários não autenticados, afinal para o NxCloud a página de login não é um opção padrão e os usuários do NxCloud geralmente usam outros métodos de autenticação.

3. Diversos endereços IP para um agente

 Se você usar um dos agentes do NxFilter com múltiplos IP para contemplar os nõs slave, eles continuarão funcionando.

Controle de acesso para os nós slave
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Se você adicionar todos os endereços IP dos nós Slave em 'Config > Cluster' toda solicitação para se unir a um nó slave a partir de um IP desconhecido será bloqueado.

Monitorando os nós slave
^^^^^^^^^^^^^^^^^^^^^^^^

Você pode visualizar o status da conexão dos nós slave, acesse 'Config > Cluster'. Uma você que o cluster for levantado todos os nós slave aparecerão informando o registro da última sincronia. Ele também informa as quantidades de requisições, bloqueios, usuários e ips.
Esse contador será zerado a meia-noite ou quanto o NxFilter for reiniciado.

Compartilhando as sessoões entre os nõs do cluster
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Portas TCP são utilizadas visando permitir a troca de informações entre os nós pertencentes ao cluster. Um dos dados compartilhados é a sessão do usuárioi, então não é necessário logar ( se autenticar ) a cada vez que consultar um nó diferente. Também são compartilhados o consumo de banda e o tempo de navegação. Mas isso pode degradar a performance caso os servidores fiquem lentos e também aumenta o tráfego de dados entre eles.

Se você não deseja que essas informações sejam compartilhadas, é possível desativar a autenticação e não usar o controle de banda nem o tempo de navegação. 

Porém, ainda pode ser interessante não ter de se autenticar a cada troca de servidor DNS. E na verdade, a sessão compartilhada é somente para evitar o redirecionamento à página de login. Se você não usa autenticação - com base em senhas - você não terá problemas. NxLogon, NxMapper e NxClient podem se comunicar com os nós do NxFilter.

E a autenticação baseada em IP funciona tranquilamente sem compartilhar a sessão.

Para desativar o compartilhamento de sessões enquanto a autenticação estiver ativa, insira o seguinte parâmetro em '/nxfilter/conf/cfg.properties'.

    no_share_session = 1

.. warning::
 O parâmetro 'no_share_session' tem de ser aplicado em todos os nós.
