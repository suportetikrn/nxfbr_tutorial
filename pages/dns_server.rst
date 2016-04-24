.. _dnsserver:

************
Servidor DNS
************

NxFilter é basicamento um servidor DNS com capacidade de fazer forward e/ou cache com a habilidade de filtrar as consultas DNS. Pode também ser usado como um servidor DNS Autoritativo. E também tem suporte ao serviço de DNS Dinâmico.

Forward
*******

Quando o NxFilter é instalado ele já vem com a opção de servidor DNS forward ativa. Ele usa os servidores do Google DNS, por padrão, como servidor DNS upstream. É permitida a alteração para outro servidor uptream em 'DNS > Setup'.


Caching
*******
NxFilter has its own cache for the DNS response from its upstream server. This means when you use a public or ISP DNS server as a DNS server for your network NxFilter can boost up your network speed by reducing the traffic to the DNS server outside your local network. This is because once a DNS response from an upstream server has been cached then your users will get the response from NxFilter not from the upstream server. You will not have a latency problem between your local network and the DNS server on the Internet.


Authoritative DNS server
************************
NxFilter can be working as an authoritative DNS server.
1. Zone File
We use the same form of zone file as BIND. You create a zone file for a domain on 'DNS > Zone File'. And then you can add your hosts into the DNS zone by editing it on GUI.
2. To put it on the Internet
Since NxFilter is a DNS filter with authentication, when you use it as an autoritative DNS server there are several things you would need to think about.
- Authentication
You must enable authentication especially when you put NxFilter on the Internet to avoid of being a target of DDOS attack. But the problem is that if you enable authetication, these anonymous users querying your domain will be redirected to the login-page of NxFilter. To allow the anonymous DNS query against your domain, you need to bypass authentication for your domain.
- Filtering
NxFilter is a DNS filter so your domain might be blocked by NxFilter for some reason. This will lead to the failure of resolving the domain you want to service. To avoid of having this kind of problem, it might be better to bypass filtering for your domain.
- Too many log
You could have too many log data for your domain as a result of DDOS attack. In that case, you would better bypass logging for your domain.
* You can set up whitelist for your domain with some bypass options but you also can do that using the bypass options of a zone file.
* On NxCloud you have 'Public Service' option instead of bypass options. In reality this is	a combination of 'Bypass Filtering' and 'Bypass Logging' as there is no 'Bypass Authentication' option for NxCloud. You need to set this option to service your DNS zone on the Internet when you use NxCloud.
3. Clustering
When you build a cluster of NxFilter your slave nodes will be working as an authoritative DNS server with the settings from the master node. You don't need to set up a secondary DNS server for redundancy. It is already clustered.

DNS Dinâmico
************
NxFilter tem suporte a DNS Dinâmico. Você pode construir um serviço no estilo 'DynDNS' com NxFilter se assim desejar.

Para ativar esse serviço vocë precisa ter um domínio em 'DNS > Setup > Dynamic Domain' e então ativar o serviço. Se quiser que o serviço seja público ou esteja disponível na internet, você tera de ativar uma Zone DNS Autoritativa em 'DNS > Zone File' para que seu Domínio Dinâmico funcione.

Uma vez que esteja tudo configurado no lado do servidor, é necessário instalar o cliente de DNS Dinâmico no sistema do seu cliente. Para isso usamos o NxUpdate.

No NxUpdate você precisa configurar o ip do Servidor, que no caso é o IP do seu NxFilter e um token associado ao nome do usuário da estação. No caso o nome do usuário será o nome da máquina.

Por exemplo, se você tem o domínio dinâmico 'exemplo.com' e instalar o NxUpdate na estação de trabalho com o token do usuário 'minhamaquina', uma vez que o NxUpdate entre em ativa você poderá pingar o endereço 'minhamaquina.example.com'.
 
 .. note::
  Dynamic DNS service requires to enable authentication on 'Config > Setup'.
  You can view the list of dynamic domains being serviced on 'DNS > Dynamic Domain'.
  On NxCloud we have 'Logging > Dynamic DNS' for admin to monitor the activities related to your dynamic domain.
