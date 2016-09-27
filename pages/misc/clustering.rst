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

  Se não redirecionar as 'Senhas de usuários' para a página de login eles não poderão se autenticar. Mas os clientes não podem ficar sem acesso à Internet. Por isso o filtro é desativado para os usuários que ainda não tinham sido autenticados para o caso em que o servidor Master cair. Se você não deseja desativar os filtros para todos os usuários a alternativa para ocasiões em que o servidor ''Master'' cair crie um usuário padrão com uma determinada faixa de ip da sua rede.

.. note::

  Para o NxCloud é um pouco diferente. Ele cancela as requisições de usuários não autenticados, afinal para o NxCloud a página de login não é um opção padrão e os usuários do NxCloud geralmente usam outros métodos de autenticação.

3. Diversos endereços IP para um agente

 Se você usar um dos agentes do NxFilter com múltiplos IP para contemplar os nós slave, eles continuarão funcionando.

Controle de acesso para os nós slave
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Só é permitido se conectar ao servidor ''Master'' os nós Slave listados em 'Config > Cluster', o que não estiverem nessa lista serão bloqueados.


Monitorando os nós slave
^^^^^^^^^^^^^^^^^^^^^^^^

Você pode visualizar o status da conexão dos nós slave, acesse 'Config > Cluster'. Uma vez que que o cluster for levantado todos os nós slave aparecerão informando o registro da última sincronia. Ele também informa as quantidades de requisições, bloqueios, usuários e ips.

Esse contador será zerado a meia-noite ou quando o NxFilter for reiniciado.

Compartilhando as sessoões entre os nós do cluster
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Para permitir a troca de informações entre os nós do cluster são utilizadas portas TCP.

Através dessas portas são compartilhados:
1. A sessão do usuário, evitando assim que o usuário se autentique toda vez que consultar um nó diferente.
2. Consumo de banda
3. Tempo de navegação

.. note::

   A desvantagem dessa solução é que pode haver queda no tempo de resposta dos serviço para os casos em que os servidores ficarem lentos e também gerar uma carga maior de tráfego entre os nós.

Se você não deseja que essas informações sejam compartilhadas, é possível desativar todo o compartilhamento de informações entre os nós. 

Porém, ainda sim pode ser interessante não ter de se autenticar a cada troca de servidor DNS. E na verdade, a sessão compartilhada é somente para evitar o redirecionamento à página de login. Se você não usa autenticação - com base em senhas - você não terá problemas. 

Os agente NxLogon, NxMapper e NxClient podem se comunicar com os nós do NxFilter, evitando a necessidade de autenticação a cada acesso a um servidor diferente.

E a autenticação baseada em IP funciona tranquilamente sem compartilhar a sessão.

Para desativar o compartilhamento de sessões enquanto a autenticação estiver ativa, insira o seguinte parâmetro em '/nxfilter/conf/cfg.properties'.

    no_share_session = 1

.. warning::
 O parâmetro 'no_share_session' tem de ser aplicado em todos os nós.
