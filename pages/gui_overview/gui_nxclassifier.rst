**********************************
GUI - NxClassifier
**********************************

O NxClassifier tem as seguintes opções nos submenus.

Setup > Classifier Setup
************************

.. envvar:: DNS Test Timeout
 
  NxClassifier só classifica os domínios existentes/válidos. Então ele primeiro testa o registro DNS antes de classficá-lo.

.. envvar:: HTTP Connection Timeout

  Após testar o registro DNS, a página é baixada no servidor para análise. Este parâmetro define o timeout para a conexão HTTP.

.. envvar:: HTTP Read Timeout
  
  Este parâmetro define o timeout para recebimento dos dados referentes a página, é medido após a conexão HTTP

 .. note::

  Se esses timeouts estiverem com valores muito altos você pode ter degradação na performance no momento da execução do NxClassifier.

.. envvar:: Classified Data Retention Days
 
  Este parâmetro define quanto tempo a classificação feita a um site pelo NxClassifier fica armazenada. O NxClassifier armazena os resultados da classificação para os sites mais recentes. O sistema não classifica domínios já categorizados ou que já estejam nos registros de classificação sem qualquer erro.

.. envvar:: Disable Domain Pattern Dic 

 O NxFilter tem um modelo de domínios baseado no processo de classificação

.. envvar:: Disable Classification 
 
 Desabilita a classificação dos domínios pelo NxClassifier.

Setup > Mass Import
*******************

Para importar um arquivo ruleset ou um arquivo Jahaslist exportado de outro sistema. Ele não remove nenhum registro existente mas sobrepõe caso os dados sejam iguais.

Ruleset
*********

Você pode definir sua própria ruleset. Ou modificar a ruleset pré-existente. Você pode exportar a ruleset e compartilhar com outros.

Classified
***********

Este é o log resultante da classificação feita pelo NxClassifier. Ele exibirá os domínios classificados recentemente e qual foi a classificação recebida ou não. Baseado no resultado da classificação você pode melhorar sua ruleset.

.. note::
  
  Com o botão 'VIEW' você pode visualizar detalhes do log e com o botão 'TEST' você saberá qual a classificação atual.

.. note:: Se deseja aplicar uma nova ruleset de classificação clique em 'RECLASSIFY-ALL' 

Excluded
*********

São os domínios que durante o processo de classificação apresentaram algum erro. Por exemplo, se for recebido o código 403 de um website em processo de classificação não há por que tentar classificá-lo pois se entende que o site está fora do ar. Ou se ao invés de receber um texto ou arquivo HTML receber arquivos que fogem desse padrão ele também será excluído.

.. warn:: 
  
 Os domínios excluídos não são removidos da lista, caso haja interesse que o NxClassifier tente classficar um domínio que tenha sido excluído é preciso removê-lo da lista antes.

Jahaslist
*********

 Permite que seja visualizado o conteúdo da Jahaslist e modifique a mesma diretamente.

.. warn::

  Apesar de haver a possibilidade de reclassificar um domínio diretamente na Jahaslist isso não é recomendado - exceto queira proceder com um importação em massa dos domínios. A Jahaslist é armazenada em uma tabela separada das demais, com isso o NxFilter não faz backup da mesma. Então é melhor fazer essa reclassificação em 'Category > System'.

.. note::

  Quando você executa a reclassificação em 'Logging > Request' ou 'NxClassifier > Classified' suas alteraçãoes ficam em 'Category > system'.
  
  Quando você exporta Jahaslist, o NxFilter faz a junção de suas personalizações de domínios em 'Category > System' com a Jahaslist e exporta essa lista em um único arquivo.

Test Run
*********

Após adicionar suas próprias regras de classificação você pode validar usando o 'Test Run' para verificar se o domínio se enquadra nas regras definidas.

.. note:: A simples execução de 'Test Run' não atualiza a classificação do domínio. Para que isso ocorra você precisa consultar o serviço de DNS do NxFilter para que este entre na lista de classificação.
