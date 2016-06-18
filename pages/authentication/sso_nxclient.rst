SSO com AD, OpenLDAP usando NxClient
*************************************************************

 NxClient é basicamente um serviço de controle para usuários remotos como os que tem seus próprios dispositivos móveis ( Notebooks ). Mas você pode usar o mesmo no modo SSO em AD ou OpenLDAP.

 Uma coisa boa é que há versão do NxClient para MAC OS, então pode ter a funcionalidade de SSO no MAC OS.

 Caso já tenhas usado o NxClient saberás que o SSO é possível por usar o conceito de 'Login Token'. Mas com esta abordagem um dos problemas é que é impossível manter - levando em conta o trabalho - centenas de instalações do NxClient com suas próprias 'Login Token'. 

  Então é disponibilizada uma forma de rodar o NxClient em uma rede local sem definir um token para cada PC. O que é preciso fazer é instalar o NxClient usando apenas um Token para todos os computadores. Então quando ele inicializa o sistema acessará o servidor NxFilter nessa rede local e ao se comunicar com o mesmo ele tentará criar uma sessão para o usuário autenticado atualmente ou o usuário da console.

 ::
  Para que o NxClient seja capaz de encontrar o NxFilter da rede local, é preciso usar o NxFilter como servidor DNS no computador em questão.
  
  Para entender mais sobre NxCliente leia : `NxClient - Filtrando usuário Remoto`

