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

Este é o log resultante da classificação feita pelo NxClassifier. Ele exibirá os domínios classificados recentemte e qual foi a classificação recebida ou não. Baseado no resultado da classificação você pode melhorar sua ruleset.

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

You can view the contents of Jahaslist and modify it directly here. But we don't recommend you to do the reclassification here unless it is a mass importation of domains. We keep Jahaslist in a separated DB file and NxFilter doesn't do auto-backup for it. So you would better use 'Category > System' for reclassification as it is in the main config DB.

 .. note::
  When you do the reclassification on 'Logging > Request' or 'NxClassifier > Classified' your reclassification data goes into 'Category > System'.
  When you export Jahaslist, NxFilter merges your custom classified domains from 'Category > System' into Jahaslist and then export the merged result into a file.

Test Run
*********

After you add your own classification rules you want to see the result. You can do a test run for your classification ruleset against a website here.

 .. note:: 'Test Run' doesn't do actual classification. If you want to classify a domain you need to make a query for the domain against NxFilter.
