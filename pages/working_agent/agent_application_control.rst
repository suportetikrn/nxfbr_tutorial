************************************
Controlando aplicações com NxClient
************************************

O NxFilter permite que se controle as aplicações executadas no desktop com o agente NxClient. Você pode bloquear as aplicações desejadas configurando a política de controle de aplicações através da GUI do NxFilter - de modo centralizado - e ainda visualizar, quem tentou executar os programas bloqueados, através dos logs.


Como funciona?
^^^^^^^^^^^^^^

Após definir a sua política de controle de aplicações em ``Policy & Rule > Application Control`` o Nxclient obtém essas definições de tempos em tempos.

.. note::

  Você pode ajustar o tempo de atualização alterando os valores no parâmetro ''Agent Policy Update Period'' em ``Config > Setup``.


Opções suportadas
^^^^^^^^^^^^^^^^^^

1. Bloquear a busca de portas

 NxClient detecta processos do UltraSurf e Tor através de verificação de portas. Isso significa que mesmo que os usuários mudem o nome do aplicativo ou os execute através de um pen drive é possível encontrá-los e bloqueá-los.

2. Bloquear por nome do processo

  Você pode bloquear um processo por um determinado nome. Funciona baseado na identificação de palavras chave. Você pode adicionar as palavras chave na GUI e se o agente identificar algum processo com esse nome ele será bloqueado.
 
Habilitar o controle de aplicações apenas para determinados usuários
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Partimos de um principio em que o controle de aplicações é uma política global. Porém se houver necessidade de aplicá-las a apenas determinados usuários, altere o parâmetro ''Disable Application Control'' em ``Policy & Rule > Policy > EDIT``.

Registrando o bloqueio de aplicações
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxFilter é, em sua essência, um filtro DNS então o formato de registro de logs foi preparado para exibir domínio bloqueados/permitidos. Para poder registrar dados sobre aplicações bloqueadas o NxFilter insere os seguintes domínios ou regras.

- ultrasurf.port.app : UltraSurf foi bloqueado por verificação de portas.
- tor.port.app : Tor foi bloqueado por verificação de portas.
- chrome.exe.pname.app : Chrome foi bloqueado através do nome do processo.
- Skype.title.app : Skype foi bloqueado com base no título da aplicação.

.. note::
 
   Quando você ativa o parâmetro ''Block UltraSurf'' e existem extensões do UltraSurf no Chrome ou há outras extensões para proxy instalados, o NxClient mata o processo e registra o sinal ''ultrasurf.chrome.app''.

Intervalo de execução
^^^^^^^^^^^^^^^^^^^^^^

Encontrar e bloquear aplicações pode causar uma certa carga no processamento. Se você não deseja causar um grande impacto na carga do PC/Desktop do usuário, incremente o valor no parâmetro ''Execution Interval'' em ``Policy & Rule > Application Control``.
