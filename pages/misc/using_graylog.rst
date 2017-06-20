.. graylog:

*********************************
Gerar relatórios usando Graylog
*********************************

  Em ambientes com centenas de usuários pode ser interessante exportar os logs e
   gerar relatórios fora do NxFilter, pois essa pode se tornar uma operação pesada para o seus sistema. Existem diversas ferramentas especializadas na extração e geração de relatórios, aqui será
   demonstrado como fazê-lo usando o Graylog em conjunto com o NxFilter.

   1 . Faça o download do pacote para o Graylog no link:
   
   2 . Na GUI do Graylog, importe o arquivo existente no zip baixado anteriormente
      - System > Content Packs > Import Content Pack
   3 . Após a importação, deverá aparecer o content pack 'NxFilter'.
      - Clique em 'NxFilter',  selecione 'nxfilter-graylog-example' e então clique em 'Apply'.
   4 . Por padrão é usada a porta UD/1514 para o input do Graylog
   5 . Na GUI do NxFilter, vá em 'Config > Setup > Syslog' altere a 'Syslog Port' para 1514.
      - E altere também o parâmetro 'Syslog Host' informando o IP do servidor do Graylog que receberá os dados.
   6 . Reinicie o NxFilter e você vera o Dashboard sendo alimentado com as informações.
      - Escolha o Dashboard 'NxFilter 2 Hours' na GUI do Graylog.

.. image:: /images/graylog_nxfilter.png

.. note::

  Após fazer o seu próprio relatório no Graylog você pode desativar o logging/armazenamento do tráfego no banco do NxFilter.
  Para isso, em 'Log Retention Days' - no menu 'Config > Setup' defina o valor '0'.
  Se ainda usa o NxFilter v3, altere o arquivo '/nxfilter/conf/cfg.properties', adicionando o atributo 'syslog_only = 1'.
