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


DNS Autoritativo
*********************
NxFilter pode atuar como um servidor DNS Autoritativo.
1. Arquivo de Zone ( Zone File )
 É usado o mesmo padrão nos arquivos de zona do BIND. O arquivo é criado em 'DNS > Zone File'. E então você pode adicionar suas estações ( host ) na zona DNS diretamente pela GUI.

2. Para disponibilizar na internet.
Sabendo que o NxFilter é um filtro DNS com autenticação, quando você o utilizar como servidor DNS autoritativo é necessário tomar conhecimento dos seguintes pontos:
  - Autenticação
    Você precisa habilitar a autenticação principalmente quando expõe o NXFilter na Internet com o objetivo de evitar ataques DDOS. Porém há o problema que se a autenticação for ativada, usuários anônimos serão redirecionados para a tela de login. Para permitir que usuários anônimos façam normalmente consulta DNS no seu domínio, você precisar permitir o 'bypass' da autenticação para seu domínio.
  - Filtro
    NxFilter é um filtro DNS, então seu dominio pode ser bloqueado pelo NxFilter por algumas razões. Para evitar problemas do tipo é indicado fazer o 'bypass' da filtragem do seu domínio.
  - Logs em excesso
    Você pode acabar tendo muitos registros de log por conta de ataques DDOS em seu domínio. No caso, pode ser melhor também ativar o 'bypass' de logs no seu domínio.

 .. note::
  Você pode configurar uma 'whitelist' para seu domínio ser liberado em alguns casos, mas também é possível usar a opção de 'bypass' de um arquivo de zona ( zone file ).
  No NxCloud você tem a opção 'Public Service' ao invés da opção 'bypass'. Na realidade essa opção é a combinação do 'ByPass Filtro' e 'Bypass Logging' não há opção 'Bypass Autenticação'  no NxCloud. Você precisa marcar essa opção para sua Zona DNS na internet quando usa o NxCloud.

3. Clustering / Usando o Cluster
 Quando está usando o NxFilter em Cluster seus nós trabalharão como um servidor DNS Autoritativo com as mesmas configurações do nó principal. Você não precisa configurar DNS Secundário para haver redundância. Isso já faz parte do serviço de clusterização.

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
