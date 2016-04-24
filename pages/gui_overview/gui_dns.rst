**********************************
GUI - DNS
**********************************

NxFilter é basicamente um servidor DNS com a habilidade de aplicar filtros.  Estes são os parâmetros relacionados a configuração do Serviço DNS.


DNS > Setup > DNS Setup
************************
- Upstream DNS server
  NxFilter works as a forwarding DNS server. You need to have at least one upstream DNS server for NxFilter.

- Upstream DNS Query Timeout
  Timeout for a DNS query to your upstream DNS server.

- Upstream DNS Load Balance
  Load balancing option for your upstream DNS servers.

- Max Client Cache TTL
  You can modify the TTL value in a DNS response from NxFilter. If you set the value to '60' NxFilter modifies the DNS cache TTL to '60' if the TTL is bigger than 60.
  0 - Don't touch it.
  60 - Don't touch it if it's smaller than 60 and make it '60' if it's bigger than 60.
  We introduced this function to minimize the effect from the client cache. However if you have more than 1,000 users you would better turn this function off for better performance.

- Response Cache Size
  NxFilter has its own cache for DNS query result from its upstream server. Generally speaking, the bigger cache would be better for the performance. Currently the default size is 200,000 and it is enough for most sites.


DNS > Setup > Local DNS 
************************
 - Local DNS Server
   Quando já um servidor DNS para resolver os endereços do domínio interno/local insira o ip dele nessa área. Você pode inserir múltiplos servidores DNS separando-os por ',' visando redundância.

- Local Domain
   Quando existe um domínio o qual você deseja fazer o foward para seu servidor DNS local adicione o mesmo nesse campo. É possível adicionar multimpos domínios separando-os por ','.
 .. warning:: 
	Não use '*' ou qualquer outro caracter especial para um domínio local

- Local DNS Query Timeout
    Timeout para uma consulta DNS feita no seu servidor de DNS local.

- Upstream DNS Load Balance
   Habilitar o balanceamento de carga para seus servidores de DNS locais.

- Use Local DNS
   Ativa o uso de DNS Local.

  .. note::
	Se você configurar um servidor DNS local para seu domínio local, todas as consultas DNS para seu domínio local serão direcionadas sem regras não tendo autenticação, filtro e registros dessas consultas.


DNS > Setup > Dynamic DNS
*************************
 NxFilter suporta o serviço de DNS dinâmico. Para saber como leia,'Servidor DNS Dinâmico' nesse mesmo tutorial.

DNS > Zone File
***************

 Quando você usa NXFilter como um servidor DNS autoritativo você pode precisar configurar um arquivo de Zona. É utilizado o mesmo padrão usado em arquivos de zona do serviço BIND. Para saber mais sobre servidores de DNS Autoritativos, acesse nesse tutorial.

DNS > Redirection
*****************
 Redirecionamento Domínio para IP ou domínio para domínio é possivel de ser feito com NxFilter. Ele funciona como um registro DNS alterado.
