GUI - Dashboard, Logging, Report
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxFilter armazena os registros de acesso por até 400 dias e você pode gerar relatórios diários, semanais e por usuários baseado nesses registros.

Dashboard
*********

 Ao acessar a GUI o Dashboard é logo apresentado. Há diversos gráficos mostrando um resumo das últimas 2 horas de acesso. Na parte inferior do Dashboard é possível ver o 10 bloqueios mais recentes das últimas 12 horas.
.. note::
  A diferença entre 'request-sum' e 'request-cnt' vem do sistema de logging do NxFilter. Para recuzir a quantidade de acesso a disco NxFilter mantém todos registros na memória. E então ele faz um 'flush' dos dados a cada minuto. Se há uma requisição ao mesmo domínio feito pelo mesmo usuário em um minuto, ele só incrementa na contagem. Então 'request-sum' significa a soma de todas as contagens e 'request-cnt' significa a contagem de todos os dados distintos.
  
Logging
*******

É possível pesquisar as requisições em diversas variáveis em 'Logging > Request'. Os registros são atualizados a cada minuto para reduzir a carga no Banco de Dados.

Em 'Logging > Signal' é possível ver os registros de acesso dos agentes do NxFilter.
Em 'Logging > NetFlow' você pode monitorar os dados NetFlow recebidos.

.. note::
  Use colchetes para melhorar sua busca.
    ex) [nxfilter], [192.168.0.100]

Relatório
*********

NxFilter gera relatórios diários, Semanais e por usuários
