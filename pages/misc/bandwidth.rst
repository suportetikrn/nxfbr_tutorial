********************************************
Controle de Banda com NxFilter ( Bandwidth ) 
********************************************

  NxFilter dá suporte a controle de uso de banda por usuário usando os dados do NetFlow. A ideia é simples. NxFilter vincula os dados do NetFlow vindos de um roteador a sessão do usuário baseado no endereço IP e se há um usuário consumindo o limite de uso especificado, NxFilter bloqueia todas as requisições feitas pelo usuário.

  A vantagem é que isso não é aplicado apenas no tráfego HTTP. Desde que NxFilter esteja usando os dados do NetFlow você pode monitorar e bloquear outros protocolos incluindo HTTP, FTP, IM, Skype, Torrent e qualquer outro protocolo usando TCP/UDP.

  Para ativar o controle do uso de banda você precisa de um roteador ou firewall com suporte a NetFlow versão 5 em sua rede e você precisa fazer com que este envie os dados de NetFlow para o NxFilter. E então ative o coletor de NetFlow no NxFilter em 'Config > Setup > NetFlow'. Então configure um limite de banda em uma política.

  Os pré-requisitos para que o NxFilter importe os dados do NetFlow:

  #. O IP de origem ou o destino deve poder ser associado a um IP de um usuário autenticado no NxFilter.
  #. NxFilter igrnora o tráfego interno. Então o IP de origem ou destino precisa ser um endereço público. Isso por levar em consideração que se está interessado em tráfego de entrada ou saída para a Internet.
  #. Por último NxFilter coleta somente dados TCP/UDP.

.. alert::

 Atualmente o NxFilter tem compatibilidade somente com o NetFlow v5

