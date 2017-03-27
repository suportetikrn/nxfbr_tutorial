NxUpdate e atualização dinâmica de IP
**************************************

Para casos em que se tem um cliente que usa IPs dinâmicos e ainda sim se deseja associar esse IP a um determinado usuário, você pode instalar o NxUpdate no sistema. Ele irá atualizar os IP's associados ao usuário no NxFilter.

NxUpdate tem, basicamente, a mesma estrutura do NxClient. Você pode instalá-lo do mesmo modo que instalaria o NxClient.

.. note:: 
  
  Ele envia os sinais: START, STOP e IPUPDATE.

  NxUPDATE pode trabalhar como um cliente de DNS dinâmico para o NxFilter.

Escrevendo seu próprio NxUpdate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Para a comunicação entre o NxFilter e o NxUpdate é usado o protoloco DNS. Significa então que você pode simular ou criar o seu próprio NxUpdate usando apenas o 'nslookup' ou outra ferramenta que faça uma simples consulta DNS.

* NxFilter v3.3.0 ou superiores e NxUpdate v7.0 ou superiores seguem esse formato de comunicação baseado no protoloco DNS.

Então, para fazer a atualização de um IP usando o nslookup, você pode proceder da seguinte forma::

  nslookup GKSYEJYG.ipupdate.signal.nxfilter.org. 192.168.0.100

Onde 'GKSYEJYG' é o token de um usuário e 'ipupdate.signal.nxfilter.org.' é o domínio especial para sinalizar o 'IPUPDATE' e '192.168.0.100' é o endereço IP do seu servidor NxFilter.

São utilizados os seguintes sinais.

- start.signal.nxfilter.org : 'START' - inicializa .

- stop.signal.nxfilter.org : 'STOP' - para .

- ipupdate.signal.nxfilter.org : 'IPUPDATE' - atualiza.

* Como demonstrado anteriormente, você tem de escrever o token do usuário para que esses sinais o identifiquem.

When we send these signals we can have two kinds of responses as a DNS response from NxFilter.
Quando esses sinais são enviados você pode receber dois tipos de respostas ( como registro DNS ) a partir do NxFilter. E elas são ::

  - 127.100.100.1 = Erro.
  - 127.100.100.100 = Successo.

Não é necessário enviar os sinais 'START' ou 'STOP' a cada atualização. Basta enviar 'IPUPDATE'.
