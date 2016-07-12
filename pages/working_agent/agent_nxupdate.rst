NxUpdate e atualização dinâmica de IP
**************************************

Para casos em que se tem um cliente que usa IPs dinâmicos e ainda sim se deseja associar esse IP a um determinado usuário, você pode instalar o NxUpdate no sistema. Ele irá atualizar os IP's associados ao usuário no NxFilter.

NxUpdate tem, basicamente, a mesma estrutura do NxClient. Você pode instalá-lo do mesmo modo que instalaria o NxClient.

.. note:: 
  
  Ele envia os sinais: START, STOP e IPUPDATE.

  NxUPDATE pode trabalhar como um cliente de DNS dinâmico para o NxFilter.

Escrevendo seu próprio NxUpdate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We use the standard DNS protocol for communication between NxFilter and NxUpdate. This means you can write your own NxUpdate as long as you can run 'nslookup' or if you can send a DNS query.

* NxFilter v3.3.0 or later and NxUpdate v7.0 or later required for the DNS protocol based communication.

If you send an IP update query against NxFilter from your Windows CMD using nslookup,

nslookup GKSYEJYG.ipupdate.signal.nxfilter.org. 192.168.0.100

'GKSYEJYG' is a login-token of a user and 'ipupdate.signal.nxfilter.org' is the special domain for 'IPUPDATE' signal. '192.168.0.100' is the IP address of your NxFilter.

We use the following signals.

- start.signal.nxfilter.org : 'START' signal.

- stop.signal.nxfilter.org : 'STOP' signal.

- ipupdate.signal.nxfilter.org : 'IPUPDATE' signal.

* You need to add a login-token of a user to these signals for user identification.

When we send these signals we can have two kinds of responses as a DNS response from NxFilter.

- 127.100.100.1 : Error.

- 127.100.100.100 : Success.

You don't need to send 'START' or 'STOP' signal if you want to go simple. Sending 'IPUPDATE' would be enough.
