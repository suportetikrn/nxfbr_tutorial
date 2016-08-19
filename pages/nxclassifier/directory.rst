***************************************
Jahaslist e sua estrutura de diretórios
***************************************

Jahaslist é o nome da lista que surgiu junto com o NxClassifier. Jahaslist é ativada quando você instala o NxFilter. O diretório '/nxfilter/jahaslist' armazena diversos arquivos nele.

 - categories.txt : As categorias do Jahaslist são definidas neste arquivo.
 
 - baselist.txt : As categorias do Jahaslist são armazenadas nele.

 - ruleset.txt : Aqui ficam armazenadas as regras padrão para o NxFilter.

.. note ::

  baselist.txt e ruleset.txt serão importados para a base de dados do NxFilter quando você inicializá-lo pela primeira vez.

  Tudo é armazenado exceto as regras de classificação que ficam em um arquivo de banco separado. Esse arquivo é o '/nxfilter/db/jahaslist.h3.db'. Quando houver interesse em reiniciar a Jahaslist - por algum motivo que pareça viável - você pode apagar este arquivo e reiniciar o NxFilter.

