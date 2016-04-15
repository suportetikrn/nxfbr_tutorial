Configurando o Cliente DNS
----------------------------

Após a instalação do NxFilter para monitorar e/ou filtrar a atividade na sua rede você precisa fazer com que o NxFilter seja o servidor DNS das sua rede.

Windows

 .. image:: /images/dns_setup.png

Linux

 .. image:: /images/dns_setup_lnx.png
 
A forma mais simples de configurar o Servidor DNS para seus usuários seria modificando a configuração de rede do sistema operacional conforme mostrado acima.

Porém se sua rede tem muitos computadores é provável que você utilize o serviço DHCP. Então você só precisa configurar no seu servidor DHCP informando que o servidor DNS de suas estações será o NXFilter.

Se você tiver um firewall você pode forçar os usuários a usar o NxFilter como servidor de DNS bloqueando qualquer tráfego de saída para `53/UDP` e `53/TCP`. Assim garantirá que o únicos servidor DNS utilizado será o NxFilter.
