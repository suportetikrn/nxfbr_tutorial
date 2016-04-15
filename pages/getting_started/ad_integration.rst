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

Servidor MS DNS e NxFilter
**************************

Quando você publicar o NxFilter em um ambiente com Active Directory você pode se preocupar com a possibilidade de quebrar a integridade do serviço do AD pelo fato de que o NxFilter atuará como servidor DNS e o papel de servidor DNS em uma estrutura com AD é muito importante. Porém não desabilitaremos ou substituiremos o Servidor DNS do AD. Nossa abordagem é trabalhar com o servidor DNS já existente do AD de forma cooperativa. 

But we don't disable or replace the existing Active Directory DNS server. Our approach is to work with the existing Active Directory DNS server in cooperation. So you have to maintain your existing MS DNS server even though you use NxFilter as the DNS server for your network.
1. Where to install it
Some people try to install NxFilter on their domain controller. But you already have another DNS server there. It is your MS DNS server. It would be better to install it on the other system to avoid of having a port collision problem.
2. Dynamic host update
MS DNS server in Active Directory does a lot of things. It lets the hosts in Active Directory know the location of resources using SRV records. And it maintains a DNS zone for every hosts. It does dynamic host IP update when you change an IP address of a system. To keep all these things working NxFilter bypasses the internal DNS queries for Active Directory domain to MS DNS server automatically. It assumes that you have your MS DNS server on the DC you imported your users from.
3. Which upstream server for NxFilter
You might have a question about which DNS server you should use as an upstream server for NxFilter because you already have a DNS server that is your MS DNS server. You can use any DNS server as an upstream DNS server for your NxFilter including your MS DNS server. NxFilter still forwards your Active Directory internal DNS queries to your MS DNS server. So you can use whichever DNS server you think the best.
4. Manual setup for MS DNS server
After you import Active Directory users and groups, NxFilter tries to work with your MS DNS server automatically based on your Active Directory importation setup but sometimes you want to have a different settings for your MS DNS server. Or you might want to have a redundancy for your MS DNS server. In that case, you can do all these things on the edit page of your Active Directory setup. For having redundancy, you can add multiple DNS servers separated by commas.
* You might need to allow 'Nonsecure Dynamic Update' on your MS DNS zone properties for NxFilter to update the IP addresses of the hosts in the MS DNS zone.
