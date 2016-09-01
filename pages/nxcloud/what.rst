******************
O que é NxCloud?
******************

NxCloud é um ambiente completo para múltiplas empresas baseado no filtro de DNS. Ele é baseado no NxFilter e herda as suas principais funcionalidades. Basicamente, você pode criar sua própria nuvem de serviço de filtro DNS como o OpenDNS.

A seguir algumas das funcionalidade disponíveis apenas no NxCloud.

Administração em múltiplos níveis
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Se você quiser criar seu próprio serviço nas nuvens, um dos fatores principais seria ter a possibilidade de criar contas para seus clientes e estes estarem aptos a configurar suas próprias políticas em uma GUI.

No NxCloud há 3 tipos de usuários.

Admin > Operator > User

 - `Admin` - é o administrador da NxCloud. Ele tem praticamente a mesma GUI do NxFilter porém sendo administrador você pode criar as contas de operadores.
 - `Operator` - São as contas dos clientes e é algo como um sub-administrador na NxCloud. Podem criar e gerenciar suas próprias políticas.
 - `User` - São criados pelos `Operator`, são os usuários do cliente.

Criando um operador
^^^^^^^^^^^^^^^^^^^^^

Para criar um operador você precisará se autenticar na GUI do NxCloud com uma conta de administrador. Em ``Config > Operator`` você pode criar um operador. Quando você criar um operador NxCloud cria um usuário padrão e uma política padrão para este mesmo operador com o mesmo nome dele.

Você pode definir o número de usuários e políticas que o operador pode criar. Isto significa que você pode ter diversos níveis em seus serviço baseado nas permissões de um operador.

GUI do Operador
^^^^^^^^^^^^^^^^

No NxCloud cada operador tem sua própria GUI. Se você autenticar na GUI NxCloud com uma conta de operador você entrará em um GUI para Operador. Ele é um pouco mais limitado/restritivo se comparado a interface GUI do administrador e você poderá manipular somente os parâmetros do operador.

Operador e usuário
^^^^^^^^^^^^^^^^^^^

Operadores podem criar seus próprios usuários e aplicar uma política diferente baseada na autenticação do usuário. Usuários podem ser validados com base no endereço IP ou usando o NxClient.

Dashboard e relatório específicos para o operador
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Dashboard e relatórios do NxClound disponíveis na GUI do Operador.

Free-Time especifico do operador
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Cada operador pode definir seus próprios Free-Time ( horários livre ) e eles podem configurar uma política de hoário de trabalho e uma política de Free-Time para seus usuários.

Lista Branca e Negra específicas do Operador
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Você pode adicionar uma lista branca/negra específica baseada em nome de domínio. Porém você ainda terá uma lista branca/negra global para o admin. Então você pode ter maior flexibilidade para trabalhar com essas listas como um administrador.

Alertas por email específico para o operador
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxCloud envia um email de alerta sobre registros de bloqueios para cada operador. Os operadores podem definir seus endereços de email para receber esses alertas e definir os períodos em que os recebe em ``Config > Alert``.

.. note::

   Você precisa configurar antes um email que receberá os alertas gerais para comunicar a um operador específico. Você o define em ``Config > Alert``.

Página de bloqueio esepecífica do operador
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Cada operador pode ter sua própria página de bloqueio. Se não houver páginas de bloqueio definidas pelo operador o NxCloud irá exibir a página padrão configurada pelo Admin.


Autenticação nas nuvens
^^^^^^^^^^^^^^^^^^^^^^^^^^

NxClient se conecta no NxCloud. O que significa que você pode diferenciar os usuários em sua própria rede e você pode aplicar uma política diferente por usuário.

Atualizador de IP Dinâmico
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Muitos de seus clientes usuário o serviço de IP dinâmico. Você pode usar NxUpdate como um atualizador de IP dinâmico para seu serviço.

Associção de DNS Dinâmico
^^^^^^^^^^^^^^^^^^^^^^^^^^

Alguns dos seus usuários podem ter um domínio dinâmico para a rede deles. Você pode associar um domínio para um usuário em NxCloud.

Agente NxRelay para diferenciar os usuários de redes distintas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

NxCloud suporta NxRelay que é um servidor de DNS relay instalado por trás de um roteador e permite que você aplique diferentes políticas baseados em IP privado ou ranges de IP da rede do seu cliente.

Padronização/Customização da GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

É uma camda da GUI que é feita para uma fácil customização. A camada de visualização ou seja da GUI é separada da parte principal do software. 

Você só precisará mudar as páginas JSP em `/nxcloud/webapps`. Esses arquivos/páginas JSP seguem um padrão de nome correspondente a sua funcionalidade/estrutura descrita no menu da GUI. Então é fácil de encontrar a funcionalidade de cada arquivo que precisa ser modificado.


Ex.:: 

  Menu ( Operator > Operator - Edit )

  Arquivo operator,operator_edit.jsp
   

