**********************************
Integração com o Active Directory
**********************************

O NxFilter tem integração com o AD. A seguir será explicada a integração do AD com o NxFilter, quando usá-lo e como implementálo.

O que é a integração com o AD
*****************************

Um dos motivos para se integrar o NxFilter com o AD é ter a possibilidade de aplicar políticas baseados em Usuários e Grupos. Também pode não desejar que os usuários se autentiquem em uma página extra de autenticação só para poder utilizar a internet, permitindo autenticação apenas quando fizessem Login nas estações de trabalho. Então a integração permite que se use a mesma conta do AD para identificar os usuários e ativar Single Sign-On.

Importação de Usuário
*********************

No NxFilter a integração com o AD funciona importanto os usuários e grupos existentes no AD. Isso significa que você permitirá o NxFilter acessar seus usuários e grupos. Para fazer esse procedimento acesse ``User & Group > Active Directory``.

Após a importação dos usuários e grupos, seus usuários conseguirão usar suas credenciais na página de Login do NxFilter.

Single Sign-On (SSO) com Active Directory
******************************************

O objetivo do SSO é aproveitar as credenciais utilizadas ao se autenticar na máquina, evitando assim que os usuários tenham de acessar a página de login do NxFilter. Para usar a capacidade do Single Sign-On (SSO) além da integração com o AD é preciso utilizar um agente com o NxFilter. 
Há diversos Agentes disponíveis para tal finalidade. São:
  * NxLogon
  * NxMapper
  * NxClient
  * NxUpdate
  * NxBlock

Você pode usar apenas um deles ou mais de um de modo a se complementarem. 

::
  Para mais informações, leia as partes sobre Single Sign-On ou os devidos Agentes
