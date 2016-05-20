******************
Usando a Jahaslist
******************

 Jahaslist é a lista padrão do NxFilter e no ato da instalação do NxFilter a mesma pode ser utilizada por 30 dias para avaliação. Uma vez o NxFilter instalado você pode usar a Jahaslist e o NxClassifier sem nenhuma restrição por 30 dias.

Custo de licenciamento da lista
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 O licenciamento de uso da lista é de 1 dólar americano por usuário, ao ano. 

 ..note ::
   Há a possibilidade de desconto para organizações sem fins lucrativos e opções de licença ilimitada. 
   Caso haja interesse em algum desses modos favor entrar em contato no email 'suporte@kernel.inf.br'.

Ativando a licença
^^^^^^^^^^^^^^^^^^

Após a aquisição da licença para a Jahaslist você receberá um arquivo 'license.lic'. Siga os passos:

#. Copie o arquivo 'license.lic' na pasta 'conf' dentro do diretório de instalação do nxfilter, ex: ''/nxfilter/conf''. 

#. Selecione em 'Categoria > Sistema' a opção de uso da Jahaslist

#. Reinicie o NxFilter

Contando o número de usuários
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 NxFilter contabiliza o número de usuários autenticado ou o número de endereços IP registrados diariamente. Se um deles excede o número de licenças adquiridas aparecerá como um usuário bloqueado nos registros de log do sistema. E os domínios consultados por esses usuários sem licença serão registrados como 'Não Classificado'. Porém como essa é uma mensagem de alerta não ocorrerá o bloqueio no lado do usuário.

.. note ::
  Para idenficar quantos usuários tem em sua rede, acesse o relatório de uso dos últimos 30 dias em 'Relatório > Uso'.

