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

NxFilter tem seu próprio cache de DNS originado do servidor upstream configurado. Significa que quando você usa um endereço público ou um servidor DNS na internet como um servidor DNS na sua configuração do NxFilter e usar o NxFilter como servidor DNS da sua rede local você poderá aumentar a velocidade da sua rede, já que o tráfego de rede deixará de fazer acessos externos e só fará consultas de DNS locaias.

Isto ocorre por que uma vez que a consulta seja feita ela é armazenada no cache do NxFilter então seus usuários receberão a resposta do NxFilter e não mais de uma servidor da internet.

Não terá também problemas de latência entre sua rede local e o servidor DNS na internet.

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
  O serviço de DNS Dinâmico requer que a autenticação esteja ativada em `Config > Setup`.

  Pode ser acessada a lista de domínios dinâmicos que estão sendo resolvidos em `DNS > Dynamic Domain`.

  No serviço NxCloud há em ``Logging > Dynamic DNS`` a possibilidade do administrador monitorar as atividades relacionadas ao seu domínio dinâmico. 
