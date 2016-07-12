************************************
NxClient e filtro de usuário remoto 
************************************

NxFilter provê um aplicativo cliente para filtro em usuário remoto que é o NxClient. Uma vez instalado o NxClient no sistema de usuário você pode filtrar e monitorar o tráfego de Internet daquele usuário em sua GUI NxFilter de modo centralizado independente de sua localização.

.. note::

  Você precisa permitir o acesso às portas 53/UDP e 80,443/TCP no(s) servidor(es) NxFilter.

Instalação do NxClient
^^^^^^^^^^^^^^^^^^^^^^^

Após instalar o NxClient usando seu instalador, o sistema de configuração estará rodando. Aparecerá um formulário com os campos `Server IP` e `Login Token` e você precisa preenchê-los de acordo com seu ambiente.

.. note::

  No NxFilter cada usuário tem um login token. Você pode encontrar esse token em 'User & Group > User > Edit'.
  NxClient é um programa Windows que roda como serviço. Ele iniciará automaticamente com o sistema.
  Quando você instalar NxClient ou NxUpdate on Mac OS X, leia as instruções para NxCliente ou NxUpdate no MAC OS X neste tutorial.

Após fazer as devidas modificações e testar sua configuração e assim inicialiizar o sistema, é possível verificar se está funcionando em 'Logging > Signal'. Deverá haver registros do NxClient nesse relatório.

.. note::

  É possível adicionar mais de um IP de servidor NxFilter separando por ',' ser você estiver rodando um cluster do NxFilter.
  Para mudar a configuração execute o programa 'C:/Arquivos de Programas/nxclient/setup.exe'.

Sinais do NxClient
^^^^^^^^^^^^^^^^^^^^^^^

Quando há o interesse em controlar um usuário remoto a parte mais difícil é forçar os usuários a ter o acesso controlado. Ninguém tem interesse em ter o acesso controlado e ainda mais estão afastados da empresa. Se esses seus próprios computadores no trabalho não há como garantir o controle. Porém se o dispositivo for da empresa é possível controlá-lo instalando NxClient no sistema dele.

Em todo caso o que impede do usuário desinstalar e parar o NxClient? NxClient roda como serviço e não dispõe de um desinstalador em 'Adicionar/Remover programas' no Painel de Controle. Então se seus usuários não tem privilégios de administração e não pode desinstalá-lo.

Porém em alguns casos é necessário dar o privilégio de 'Administrador Local' a seus usuários. Neste caso não é possível impedir os usuários de removerem o NxClient. 

Por conta disso foram definidos diversos sinais que podem indicar o que está ocorrendo no sistema. NxCliente envia os seguintes sinais: ::

- START : Quando NxClient inicia ele envia esse sinal para o NxFilter.
- STOP : Quando o NxClient para ele envia esse sinal para o NxFilter.
- PING : A cada 5 minutos o NxClient envia esse sinal para o NXFilter.

Você pode visualizar esses sinais em 'Logging > Signal' na área de administração do NxFilter.

Medidas de segurança para o NxClient
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

O NxClient precisa se conectar ao NxFilter para atualizar as políticas e regras. Quando o NxClient não consegue se conectar ao servidor NxFilter ele faz um bypass nas regras de acesso, afinal seus usuários precisarão acessar a internet de qualquer forma. É possível especificar múltiplos endereços de IP dos servidores NxFilter na configuração do NxCliente  visando redundância.

Alteração automática entre filtro local ou remoto
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Quando você usa o NxClient no notebook da empresa você pode ter problemas com as políticas de controle de acesso quando estiver na empresa. Seu notebook pode ser controlado duas vezes, uma pelo NxClient e outra pelo NxFilter. E o funcionário pode acabar sendo forçado a seu autenticar no NxFilter.

Para resolver estas questões o NxClient faz a mudança automáticamente entre fazer o filtro local ou remoto. Isso signigica que o NxClient pode localizar o servidor NxFilter na rede local e quando consegue ele desativa o proxy. E mais, ele ainda tem seu próprio módulo NxLogon o que permite que seja feito o Single Sign-On na rede local.

 .. warning:: 
  
  Caso não ache interessante a mudança automática você pode adicionar o seguinte parâmetro no arquivo de configuração '' cfg.properties ''

   ``no_swith = 1``

Removendo o NxClient
*********************

Para evitar uma desinstalação acidental feita pelo próprio usuário, o NxClient não provê um módulo de remoção em 'Adicionar/Remover programas' no Painel de Controle. Quando você decidir desinstalar o NxClient você precisará fazê-lo manualmente com os seguintes comandos.

 # Rode 'C:/Program Files/nxclient/bin/unstsvc.bat'.

 # Apague o diretório 'C:/Program Files/nxclient'.

Instalação silenciosa
**********************

Some people want to install NxClient on multiple PCs using GPO or PDQ deployment. For this, we have the silent install option for NxClient.

Em alguns casos pode ser interessante instalar o NxClient em diversos terminais de trabalho usando GPO or publicação PDQ. Para isso nos podemos usar a opção de instalação em modo silencioso do NxClient.

Para fazê-lo,

  /silent : Executa o instalar no modo silencioso ( A janela de progresso é exibida ).

  /verysilent : Nada é exibido.

E ainda é possível passar como parâmetro o 'IP do servidor' e/ou o 'Login Token'.

  /server=192.168.0.100

  /token=2P1WQ6VF

Por exemplo:

   nxclient-6.0-win.exe /silent /server=192.168.0.102 /token=2P1WQ6VF

.. note::

  Você pode criar seu próprio pacote MSI usando o MSP wrapper disponível em http://www.exemsi.com.

  Quando você instala o Java no modo silencioso/discreto ( já que ele também é um pre-requisito para o NxClient ), o NxClient pode não funcionar, isso por que instalando o Java nesse modo as vezes faz com que ele não sete o caminho para sua instalação em ``PATH``


