*******************************
Proxy filter com NxClient
*******************************

NxClient tem módulo de proxy local para filtro em protocolo HTTP.

Como funciona?
--------------

Antes de qualquer coisa defina sua política de filtragem em ``Policy & Rule > Proxy Filtering``. Após iniciar o NxClient no sistema do usuário ele irá filtrar o tráfego HTTP definindo ele mesmo como um servidor proxy local. NxClient coleta as políticas/regras de filtro do proxy de tempos em tempos, definido de acordo com o parâmetro ``Agent Policy Update Period`` em ``Config > Setup``.

Opções Suportadas
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

NxClient bypasses the domains you have on 'Whitelist > Domain' with 'Bypass Filtering' option. But this only applied on HTTP protocol on Windows. When you need to bypass the other protocols than HTTP or the sites using the other ports than TCP/80 add the sites here. They will be appended to the system proxy bypass list on Windows.
Enable proxy filtering only for specific users
The proxy filtering of NxFilter works globally. If you need to disable it for some user check 'Disable Proxy Filtering' option on the 'Policy & Rule > Policy > EDIT'.
Logging
You only get domain level log data. But you will see a detailed block reason like the followings.
Domain: www.google.com
Reason: Blocked by proxy, url_kw=game
