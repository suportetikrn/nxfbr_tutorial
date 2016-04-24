**********************************
GUI - Policy / Política 
**********************************

Com NxFilter você pode ter diversas políticas de filtro aplicáveis a usuários e/ou grupos.

Criando uma política
**********************************

Quando o NxFilter é instalado, há somente uma política no sistema que é 'Default'. Está política será aplicada a todos se não for feita nenhuma alteração. Para aplicar uma política diferente para um determinado usuário ou grupo é preciso criar uma nova política e habilitar a autenticação.

Editando uma política
**********************************
Após criar uma política você pode modificar suas propriedades

.. envvar:: Priority Points
Se há diversas políticas associadas a um único usuário, a política com o maior valor será aplicada.

.. envvar:: Enable Filter
Se está opção estiver desmarcada essa política não efetuará bloqueios.

.. envvar:: Block All
Tudo bloqueado

.. envvar:: Block Unclassified
Bloqueia domínios não classificados.

.. envvar:: Ad-remove
Bloqueia domínios que estejam na categoria `Ads` da Jahashlist colocando uma página em branco.

.. note:: É muito útil pro caso de remover ads embutidos em páginas e não distorcer mostrando a página de bloqueio do nxfilter.

.. envvar:: Max Domain Length
There are some malwares using domain name itself as a message protocol. These domains are abnormally long while the length of most domains are under 30 characters. You can set a limit for the length of a domain to block these abnormal domains. To prevent having false positives NxFilter doesn't apply 'Max Domain Length' against 100,000 well known domains.
.. envvar:: Block Covert Channel
Some malwares or botnets are using DNS protocol as their communication tool. They are using DNS query and response to communicate to each other.
.. envvar:: Block Mailer Worm
Normally you are not supposed to see MX query from your client PC. When NxFilter finds MX type query from your client PC it will be regarded from some malware trying to send emails.
.. envvar:: Block DNS Rebinding
When NxFilter finds a private IP address(192.168.0.0/16, 172.16.0.0/12, 10.0.0.0/8) on DNS response packet it will be blocked as DNS rebinding attack.
 .. note::
  Se você tem seu próprio registro DNS com IP privado você precisa colocar o bypass do domínio na whitelist.

.. envvar:: Allow 'A' Record Only
This is the most strict way of filtering malwares and botnets employing DNS protocol as their communication tool. If you are an ordinary office worker you don't need to use any special type of DNS record.	With this option NxFilter allows A, AAAA, PTR, CNAME only and the other types of DNS records will be blocked.
.. envvar:: Quota
NxFilter has quota-time feature. You can allow your users to browse some websites for a certain amount of time. You can set the amount of time here.
.. envvar:: Quota All
Apply quota to all domains including unclassified domains.
.. envvar:: Safe-search
Enforcing safe-search against Google, Bing, Yahoo and Youtube.
* Safe-search enforcing for Yahoo requires a local proxy agent running on user system.
.. envvar:: Block-time
You can set policy specific block-time.
.. envvar:: Disable Application Control
Disable application control on policy level.
.. envvar:: Disable Proxy Filtering
Disable proxy filtering for on policy level.
.. envvar:: Logging Only
Monitoring user activity without blocking them.
.. envvar:: Blocked Categories
You can block DNS request by categories.
.. envvar:: Quotaed Categories
If you check some categories in 'Quotaed Categories' then your users can access the websites in the categories for the amount of time you specified with 'Quota' above.	When a user consumed up his quota his/her DNS requests for those sites will be blocked.

Define a free-time
**********************************
You can define a global free-time in 'Policy & Rule > Free Time'. If you assign a free-time policy to users it will be applied during the time defined here.
* If the start-time is bigger than the end-time then it will break into 'end-time ~ 24:00' and '00:00 ~ start-time'	on the same day.
* You can set a group specific free-time on 'User & Group > Group > EDIT'.

Application Control
**********************************
NxFilter provides application control through its agents, NxLogon and NxClient. For more details read 'Application control with NxLogon and NxClient' part of this tutorial.

Proxy Filtering
**********************************
NxFilter provides HTTP proxy filtering through NxClient. For more details read 'Proxy filtering with NxClient' part of this tutorial.
