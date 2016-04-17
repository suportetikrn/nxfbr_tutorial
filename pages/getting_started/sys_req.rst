Requisitos Básicos
----------------------
 * Windows, Linux, FreeBSD ou Sistema Operacional que rode Java ( JRE ) 7 ou superior instalado.
 * 512 MB RAM.
 * 4 GB de espaço em disco.
 * Portas Liberadas: 53/UDP, 80/TCP, 443/TCP.



 .. note:: NxFilter pode ser executado com hardware inferior quando há poucos usuários, porém é recomendado se ter mais que 1 GB de memória RAM e 40 GB de espaço em disco, principalmente quando se tem mais de 1.000 usuários.

 .. note:: Por padrão NxFilter é configurado para usar 512 MB de RAM. Essa configuração pode não ser suficiente para um ambiente maior. É aconselhado aumentar o limite de memória para a JVM no seu script de inicialização. Em 'startup.sh' mude o valor '512m' para valores superiores.
