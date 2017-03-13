******************
Exportar Syslog
******************

NxFilter permite exportar o Syslog. Os dados exportados tem seus campos separados por '|'.

Por exemplo a seguinte linha de Syslog do NxFilter: ::

 NXFILTER|2017-03-13 10:53:23|Y|www.bbc.co.uk|pwuser|192.168.0.101|admin|news|Blocked by admin|33|grupoA

Pode ser quebrado da seguinte forma:

 - Prefixo : NXFILTER
 - Data : '2017-03-13 10:53:23'
 - Bloqueado (Sim=y/Não=n) : Y
 - Domínio : www.bbc.co.uk
 - Usuário : pwuser
 - IP Cliente : 192.168.0.101
 - Política : admin
 - Categoria : news
 - Motivo do bloqueio : 'Blocked by admin'
 - Tipo de consulta DNS : 33
 - Grupo: grupoA

