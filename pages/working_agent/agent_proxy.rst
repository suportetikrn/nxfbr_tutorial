*******************************
Proxy filter com NxClient
*******************************

NxClient tem módulo de proxy local para filtro em protocolo HTTP.

Como funciona?
--------------

Antes de qualquer coisa defina sua política de filtragem em ``Policy & Rule > Proxy Filtering``. Após iniciar o NxClient no sistema do usuário ele irá filtrar o tráfego HTTP definindo ele mesmo como um servidor proxy local. NxClient coleta as políticas/regras de filtro do proxy de tempos em tempos, definido de acordo com o parâmetro ``Agent Policy Update Period`` em ``Config > Setup``.

Opções Suportadas
^^^^^^^^^^^^^^^^^^

1. Block HTTPS

 Você pode bloquear todo o tráfego HTTPS.

2. Block IP Host

 Bloquear requisições HTTP que utilizam somente IP.

3. Block Other Browser
 
 O processo de filtro no Proxy do NxFilter é ativado através das configurações de proxy de sistema. Internet Explorer e browsers como o Chrome e muitas outras aplicações usam as configurações de proxy do sistema operacional. Porém algumas aplicações ainda usam conexões diretas para a internet. 

 Com essa opção ativada o NxClient irá bloquear qualquer programa que faça conexão HTTP diretamente a internet.

.. note::
  
  - O serviço de Proxy Filter suporta Internet Explorer e os Navegadores Chrome e Firefox.
 
  - Você pode permitir acesso direto a internet atraveś do HTTP para determinadas aplicações usando a opção ``Excluded Keywords`` em ``Policy & Rule > Application``. Ele é usado para controle de aplicações, mas ele pode ser usado para 'bypassar' a opção 'Other Browser Blocking'.

4. Blocked Keyword in URL

 Verifica palavras chave com base na URL solicitada.

5. IE Proxy Bypass

NxClient ignora os domínios registrados em ``Whitelist > Domain`` no parâmetro ``Bypass Filtering``. Porém só é aplicado no Windows sobre o protocolo HTTP. Quando você precisa ignorar outros protocolos além do HTTP ou sites usando outras portas que não sejam 80/TCP insira os sites nesse campo. Ele será inserido em Proxy do Sistema, na lista de endereços ignorados no Windows.

Ativando o filtro de proxy somente para usuários específicos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

O filtro de proxy do NxFilter funciona de modo global. Se você precisar desabilitá-lo para um determinado usuário, marque o item `Disable Proxy Filtering` em ``Policy & Rule > Policy > EDIT``.

Logging
^^^^^^^^

Você só terá registro a nível de domínio. Mas você verá a razão do bloqueio detalhada como a seguir.

 - Domínio: www.google.com
 - Razão: Bloqueado por proxy, url_kw=jogos
