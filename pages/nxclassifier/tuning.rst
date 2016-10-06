****************************************
Ajustes de performance no NxClassifier
****************************************

Para ambientes grandes com muitos usuários pode ser que a velocidade de classificação do NxClassifier ( que é feito em sites ainda não qualificados ) esteja muito abaixo do esperado. Isso ocorre por que a configuração do NxFilter priorisa filtrar sites e não qualificá-los, até para evitar um consumo de recursos desnecessário o número de agentes do NxClassifier é de apenas 2 agentes por padrão.

Para aumentar o número de agentes, melhorando assim a resposta do NxClassifier, altera-se o parâmetro ''classifier_num'' em ''/nxfilter/conf/cfg.properties'.

.. code-block:: jproperties

  classifier_num = 8

E quando há um cluster NxFilter, o NxClassifier também fica em cluster. Com essa funcionalidade você também pode dedicar um nó só para trabalhar com classficação. Rodando 16 agentes para a classficaçào em um nó e nos demais definindo o parâmetro ''classifier_num'' para 0.

Outro ponto a ser observado é que quanto maior a 'ruleset'  maior o consumo de CPU.
