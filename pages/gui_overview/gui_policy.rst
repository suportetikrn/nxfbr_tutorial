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
Existem alguns `malwares` que usam um domínio próprio como um protocolo de mensagem. Esses domínios são extensos de forma anormal, enquanto a maioria dos domínios tem menos de 30 caracteres. Você pode definiar um limite para esse tamanho.Para previnir falso positivo NxFilter não aplica 'Max Domain Length' contra 100 mil domínios conhecidos.

.. envvar:: Block Covert Channel
Alguns malwares ou botnets usam o protocolo DNS como ferramenta de comunicação. Eles usam consultas DNS e respostas para se comunicar uns com os outros.

.. envvar:: Block Mailer Worm
É incomum se ver consultas MX feitas de uma estação de trabalho. Quando NxFilter encontra essa consulta vinda de uma estação ela provavelmente é feita por algum malware tentando enviar emails.

.. envvar:: Block DNS Rebinding
Quando NxFilter identifica um IP privado (192.168.0.0/16, 172.16.0.0/12, 10.0.0.0/8) nos pacotes de respostas DNS ele será bloqueado, sendo tratado como um ataque de DNS Rebinding.

 .. note::
  Se você tem seu próprio registro DNS com IP privado você precisa colocar o bypass do domínio na whitelist.

.. envvar:: Allow 'A' Record Only
Esta é a forma mais restrita de filtrar malwares e botnets que usam o protocolo DNS como ferramenta de comunicação. Se você tem um típico escritório não precisa usar nenhum tipo de registro DNS especial. Com essa opção o NxFilter permite apenas consultas a registros do tipo A, AAAA, PTR, CNAME e os outros tipos de registros DNS serão bloqueados.

.. envvar:: Quota
NxFilter tem a funcionalidade de quota-por-tempo ( quota-time ). Você pode permitir que seus usuários naveguem por certos sites por um determinado tempo. Você pode definir a quantidade de tempo nesse campo.

.. envvar:: Quota All
Aplicar quota a todos os domínios, inclusive os `não classificados`.

.. envvar:: Safe-search
Força o uso de safe-search no Goolg, Yahoo, Youtube e Bing.
 .. note:: Para uso com Yahoo é obrigatório o uso de proxy agent rodando no sistema

.. envvar:: Block-time
Vocë pode definir o período em que a política de bloqueios é aplicada.

.. envvar:: Disable Application Control
Inativa o controle de aplicação na política.

.. envvar:: Disable Proxy Filtering
Inativa o filtro de proxy na política.

.. envvar:: Logging Only
Monitora somente a atividade do usuário mas não o bloqueia.

.. envvar:: Blocked Categories
Permite bloquear consultas DNS por categorias.

.. envvar:: Quotaed Categories
Se algumas categorias forem marcadas, então os usuários que estiverem nessa política, só poderão acessar os sites classificados nelas pelo tempo determinado em 'Quota'. Quando o usuário consome o tempo da quota suas requisições para os sites dentro das categorias em 'Quotaed Categories' serão bloqueadas.

Definir um horário livre
**********************************
Você pode definir um período livre global em 'Policy & Rule > Free Time'. Se for atribuido um período livre para usuários ele estará subordinado ao horário definido aqui.
 .. note::
  Se a hora inicial for maior que a hora final então ela funcionará da seguinte forma 'hora-fim ~ 24:00' e '00:00 ~ hora-inicio' no mesmo dia.
  Você pode definir um tempo livre específico para um grupo em 'User & Group > Group > EDIT'.

Controle de Aplicação
**********************************
NxFilter permite o controle de aplicações através de seus agentes: NxLogon e NxClient. Para mais detalhes leia 'Controle de Aplicação com NxLogon e NxClient' nesse mesmo tutorial.

Proxy Filtering
**********************************
NxFilter provê um proxy filter HTTP através do NxClient. Para mais detalhes leia 'Proxy filtering com NxClient' nesse mesmo tutorial.
