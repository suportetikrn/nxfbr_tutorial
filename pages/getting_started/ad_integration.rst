**********************************
Integração com o Active Directory
**********************************

O NxFilter tem integração com o AD. A seguir será explicada a integração do AD com o NxFilter, quando usá-lo e como implementálo.

O que é a integração com o AD
*****************************

Um dos motivos para se integrar o NxFilter com o AD é ter a possibilidade de aplicar políticas baseados em Usuários e Grupos. Também pode não desejar que os usuários se autentiquem em uma página extra de autenticação só para poder utilizar a internet, permitindo autenticação apenas quando fizessem Login nas estações de trabalho. Então a integração permite que se use a mesma conta do AD para identificar os usuários e ativar Single Sign-On.

Importação de Usuário
*********************

No NxFilter a integração com o AD funciona importanto os usuários e grupos existentes no AD. Isso significa que você permitirá o NxFilter acessar seus usuários e grupos. Para fazer esse procedimento acesse ``User & Group > Active Directoryi``.

Após a importação dos usuários e grupos, seus usuários conseguirão usar suas credenciais na página de Login do NxFilter.

Single Sign-On com Active Directory
***********************************
