**********************************
GUI - DNS
**********************************

NxFilter é basicamente um servidor DNS com a habilidade de aplicar filtros.  Estes são os parâmetros relacionados a configuração do Serviço DNS.


DNS > Setup > DNS Setup
************************
.. envvar:: Upstream DNS server

  NxFilter funciona como um servidor de encaminhamento DNS. É obrigatório ter ao menos um servidor de Upstream DNS para o NxFilter.

.. envvar:: Upstream DNS Query Timeout

  Timeout para uma consulta DNS retornar do seu servidor Upstream DNS.

.. envvar:: Upstream DNS Load Balance

  Opção para ativar balanceamento de carga entre seus servidores de upstream DNS.

.. envvar:: Max Client Cache TTL

  O TTL pode ser modificado para uma resposta de registro DNS a partir do NxFilter. Se for definido o valor '60' o NxFilter modificará o cache TTL para '60' caso ele seja superior a esse valor.

  - 0 - Ignorará o valor TTL enviado pelo servidor Upstream

  - 60 - Ignora somente se o valor for inferior a '60', caso seja superior força com que o mesmo seja '60'

  A ideia principal dessa funcionalidade é minimizar os efeitos causados pelo cache dns do cliente. Em todo caso se no seu ambiente houver mais de 1.000 usuários é interessante desligar essa funcionalidade de alteração do TTL para obter melhor performance.

.. envvar:: Response Cache Size

  NxFilter tem seu próprio cache DNS, que é alimentado a partir do servidor Upstream. Geralmente, quanto maior o cache melhor a performance. 

  .. note ::

    Atualmente o NxFilter comporta 200.000 registros e é suficiente para a maioria dos ambientes.

DNS > Setup > Local DNS 
************************

.. envvar:: Local DNS Server

   Quando já um servidor DNS para resolver os endereços do domínio interno/local insira o ip dele nessa área. Você pode inserir múltiplos servidores DNS separando-os por ',' visando redundância.

.. envvar:: Local Domain

   Quando existe um domínio o qual você deseja fazer o foward para seu servidor DNS local adicione o mesmo nesse campo. É possível adicionar multimpos domínios separando-os por ','.

 .. warning:: 

	Não use '*' ou qualquer outro caracter especial para um domínio local

.. envvar:: Local DNS Query Timeout

    Timeout para uma consulta DNS feita no seu servidor de DNS local.

.. envvar:: Upstream DNS Load Balance

   Habilitar o balanceamento de carga para seus servidores de DNS locais.

.. envvar:: Use Local DNS

   Ativa o uso de DNS Local.

  .. note::

	Se você configurar um servidor DNS local para seu domínio local, todas as consultas DNS para seu domínio local serão direcionadas sem regras não tendo autenticação, filtro e registros dessas consultas.


DNS > Setup > Dynamic DNS
*************************

 NxFilter suporta o serviço de DNS dinâmico. Para saber como leia,'Servidor DNS Dinâmico' nesse mesmo tutorial.

DNS > Setup > Misc
******************

.. envvar:: Drop Hostname Without Domain

   Útil para ambientes que usem NxFilter ou NxCloud nas nuvens e que n&atilde;o necessita resolver hostnames.

.. envvar:: Drop PTR For Private IP
   
   Descarta consultas para endereços IP privados. Indicado para ambientes que rodem o NxFilter em nuvem.

DNS > Zone File
***************

 Quando você usa NXFilter como um servidor DNS autoritativo você pode precisar configurar um arquivo de Zona. É utilizado o mesmo padrão usado em arquivos de zona do serviço BIND. Para saber mais sobre servidores de DNS Autoritativos, acesse nesse tutorial.

DNS > Redirection
*****************

 Redirecionamento Domínio para IP ou domínio para domínio é possivel de ser feito com NxFilter. Ele funciona como um registro DNS alterado.


DNS > Zone Transfer
********************

 Em algumas situações pode ser necessário importar uma zona DNS a partir de outro servidor DNS. Ao ser configurada uma zona para transferência, o NxFilter importa a mesma constantemente usando o protocolo IXFR.
