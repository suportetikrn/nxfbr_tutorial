*******************************************************
GUI - Estrutura de diretórios e padronização dos nomes
*******************************************************

A camada GUI do NxOEM foi desenhada de modo a facilitar sua personalização. É uma parte completamente separada do Core principal. E segue uma padronização, que a faz ser correspondente a estrutura de menus, facilitando localizar os arquivos desejados.

Por exemplo: se você quer modificar ''Policy & Rule > Free Time'', no menu do NxOEM, o arquivo a ser modificado será ''/nxfilter/webapps/policy,free_time.jsp''.

.. note::
  
   No NxCloud há um menu especifico para o operador. Se haverá um JSP específico para o menu do operador então ele deve ter o prefixo ''zop''.
    ex) zop,policy,free_time.jsp

Estrutura de diretórios da aplicação web
-----------------------------------------

Todos os arquivos JSP ficam em ''/nxfilter/webapps'' e não é usado nenhum sub-diretório para armazenar páginas JSP, isso para simplificar e facilitar o entendimento. Tudo que é necessário está no diretório ''/nxfilter/webapps''.

Segue a seguinte estrutura dentro do diretório ''/nxfilter'':

+-------------------+--------------------------------------------------------------------------------------------------------+
|   Diretório       |              Função                                                                                    |
+============+======+========================================================================================================+
|                   | Páginas de erro para os códigos HTTP. 				                                     |
| webapps/error	    |                                                                                                        |
|                   | Para personalizar para um código específico defina em ''/webapps/WEB-INF/web.xml''       		     |
+-------------------+--------------------------------------------------------------------------------------------------------+
| webapps/example   | Páginas de exemplo para customizar o módulo de login                                                   |
+-------------------+--------------------------------------------------------------------------------------------------------+
| webapps/img       | Imagens para as páginas web                    			                                     |
+-------------------+--------------------------------------------------------------------------------------------------------+
| webapps/include   | Arquivos JSP comuns a outras páginas, que pode ser incluídas em outros arquivos JSP.                   |
+-------------------+--------------------------------------------------------------------------------------------------------+
| webapps/lib       | Contém arquivos CSS e Javascript                                                                       |
+-------------------+--------------------------------------------------------------------------------------------------------+
| webapps/WEB-INF   | Necessário para o servidor WEB Tomcat embutido                                                         |
+-------------------+--------------------------------------------------------------------------------------------------------+

.. warning::
 
 - Os erros HTTP 400 são usados para um propósito especial. Você não pode definir nenhuma página para o código de erro HTTP 400.

 - O arquivo '/include/lib.jsp' é uma biblioteca compartilhada por todos os arquivos JSP. Ele tem algumas funções, iniciliza todo o código e verifica a autenticação também.

 - Não incluímos diretamente o arquivo '/include/lib.jsp'. Ele é executado quando nós incluímos o arquivo '/include/top.jsp'


Separando a GUI personalizada em outro diretório
------------------------------------------------

Quando a GUI é personalizada, não é uma boa ideia modificar os arquivos originais. Você pode mantê-las para usar como referência e criar outro diretório dentro do /nxfilter e copiar todos os arquivos que estão dentro de ''/nxfilter/webapps' para o novo diretório e então modificar esses arquivos que foram copiados. Para facilitar mais ainda, NxOEM permite que se defina o parâmetro ''www_dir'' em '/nxfilter/conf/cfg.properties.

Se por exemplo você armazenou sua GUI personalizada em ''/nxfilter/myweb'' e quer usá-la como a raiz do servidor web do NxOEM, você irá adicionar a seguinte linha no arquivo `cfg.properties`.

.. code-block:: jproperties 

    www_dir = myweb

Então reinicie o NxOEM.
