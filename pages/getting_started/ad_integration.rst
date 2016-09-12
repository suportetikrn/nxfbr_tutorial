
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

 .. note:: Para mais informações, leia as partes sobre Single Sign-On ou os devidos Agentes

Servidor MS DNS e NxFilter
**************************

Quando você publicar o NxFilter em um ambiente com Active Directory você pode se preocupar com a possibilidade de quebrar a integridade do serviço do AD pelo fato de que o NxFilter atuará como servidor DNS e o papel de servidor DNS em uma estrutura com AD é muito importante. Porém não desabilitaremos ou substituiremos o Servidor DNS do AD. Nossa abordagem é trabalhar com o servidor DNS já existente do AD de forma cooperativa. 

Mas a ideia não é desabilitar ou substituir o servidor DNS AD existente. Nosso objetivo é trabalhar com o servidor DNS AD de forma colaborativa. Então você precisa manter seu servidor MS DNS mesmo que use o NxFilter como servidor DNS para toda a sua rede.

1. Onde instalar

Em alguns ambientes tentam instalar o NxFilter dentro do próprio controlador de Domínio (AD). Mas como dito antes, já existe um servidor DNS no AD, é o seu servidor MS DNS. O correto é instalar o NxFilter em outro servidor de modo que evite conflito de portas, no caso do DNS ( `53/udp` e `53/tcp` ).

2. Atualização dinâmica de IP

O Servidor MS DNS no MS Active Directory executa diversas operações. Ele permite que os terminais/hosts saibam onde estão os recursos que utilizam registros SRV. E mantem uma Zona DNS para todos os terminais/hosts. Ele também faz atualização dinâmica do IP quando o endereço IP da máquina é alterado. 

Para manter todas essas coisas funcionando o NxFilter faz um `bypass` de consultas internas que seriam de cargo do servidor AD, direcionando automaticamente - de modo transparente - para o servidor MS DNS. Ele entende que se você tem um servidor MS DNS no Domain Controller ( DC ) é dele que seus usuários são importados.

3. Que servidor upstream utilizar no NxFilter

Você pode se perguntar sobre que servidor DNS utilizar como upstream para o NxFilter pois você já tem um servidor DNS que é o seu servidor MS DNS . Você pode usar qualquer servidor DNS como upstream, inclusive o próprio servidor MS DNS. O NxFilter continuaŕa direcionando as suas consultas internas para seu servidor AD, isso não impedirá o funcionamento do NxFilter. Então você pode usar o servidor DNS que achar melhor.

 .. warning::

  Ao usar seu servidor MS DNS como upstream leve em conta que o mesmo terá permissão para consulta na internet.

4. Configuração Manual para o servidor MS DNS.

Após fazer a importação dos seus usuários e grupos no AD, NxFilter tentará automáticamente usar seu servidor MS DNS, baseado nas configurações da sua importação porém algumas vezes se deseja usar outro servidor MS DNS. 

Ou pode se deseja ter uma redundância do MS DNS. Neste caso, você pode fazer todas as alterações na página de configuração do Active Directory na GUI do NxFilter. Para ter redundância na consulta de servidores DNS você pode inserir os servidores separando por vírgulas.

 .. note:: 

   Você pode ter de ativar 'Atualização Dinâmica Insegura' em `Propriedades` na Zona do servidor MS DNS para que o NxFilter faça a atualização dos IP das estações diretamente na Zona.

Exemplo de um ambiente em produção
**********************************

Suponha que na empresa ACME o ambiente é composto por diversos desktops com Windows, alguns Macbooks e recentemente foram adquiridos muitos Chromebooks. Os usuários da rede ainda trazem seus smartphones Android e iPhone. E claro para garantir a qualidade dos serviços na rede você tem servidores Linux para manter os sites, sistemas e compartilhamento de arquivos.

Há ainda o interesse de controlar os acessos dentro ou fora do escritórios, mantendo os logins de usuários através de contas no AD.

A primeira coisa a se fazer é configurar o NxOEM ( já que estamos em um ambiente empresarial esse é o modelo certo ) para importar as contas de usuários e grupos do AD. E então usar o NxLogon nos desktops Windows.

Porém o NxLogon não funciona nos MacBooks. Para os Mac você pode usar o NxMapper, só precisa instalar o NxMapper no controlador de domínio.

Já para os notebooks você pode instalar o NxClient. NxClient atua, basicamente, como um agente de filtro remoto para o NxFilter mas eles tentarão fazer o SSO quanto estiverem na rede local.

.. note::

   O NxClient tem versões para Mac e Windows.

Para os Chromebook há a extensão NxBlock. O NxBlock é uma extensão para o Chrome e você pode usá-lo como um agente de filtro remoto ou agente SSO para o AD.

Já para seus servidores é melhor não filtrá-los então defina IP estático para eles e use outro servidor DNS para eles, afinal, geralmente você não precisa bloquear nada - de consulta DNS - para os servidores.

Para os smartphones Android e iPhone, não tem preocupação, afinal o NxFilter tem sua página de login ( estilo Captive Portal ) e eles acessarão a mesma normalmente para autenticar.

