*******************************************************
GUI - Estrutura de diretórios e padronização dos nomes
*******************************************************

A camada GUI do NxOEM foi desenhada de modo a facilitar sua personalização. É uma parte completamente separada do Core principal. E segue uma padronização, que a faz ser correspondente a estrutura de menus, facilitando localizar os arquivos desejados.

Por exemplo: se você quer modificar ''Policy & Rule > Free Time'', no menu do NxOEM, o arquivo a ser modificado será ''/nxfilter/webapps/policy,free_time.jsp''.

.. note::
  
   No NxCloud, ele tem um menu especifico para o operador. Se haverá um JSP específico para o menu do operador então ele deve ter o prefixo ''zop''.
    ex) zop,policy,free_time.jsp

Estrutura de diretórios da aplicação web
-----------------------------------------

Todos os arquivos JSP ficam em ''/nxfilter/webapps'' e não é usado nenhum sub-diretório para armazenar páginas JSP, isso para simplificar e facilitar o entendimento. Tudo que é necessário está no diretório ''/nxfilter/webapps''.

Segue a seguinte estrutura:

````
	/nxfilter/webapps
			- error
			- example
			- img
			- include
			- lib
			- WEB-INF
````

In 'webapps/error' directory we have the error pages for HTTP error codes. If you want to have an error page for a specific HTTP error code you can define it on '/webapps/WEB-INF/web.xml'.
* We use HTTP 400 error for special purpose. You shouldn't define any error page for HTTP 400 error.
In 'webapps/example' directory we have some example JSP pages for custom login module.
In 'webapps/img' we keep the image files for webpages.
In 'webapps/include' we have common JSP files to be included into the other JSP files. These are for library functions and navigation menus and initialization code for JSP pages.
* '/include/lib.jsp' is a common library file for all JSP files. It has some utility functions for web development and it executes the initialization code for JSP pages and does authentication checking as well.
* We don't include '/include/lib.jsp' directly. It gets included when we include '/include/top.jsp'.
In 'webapps/lib' we have CSS and javascript files.
We have 'WEB-INF' as we use an embedded Tomcat to be NxFilter's built-in webserver.
Separating your customized GUI into another directory
When you customize NxFilter's GUI it is not a good idea to modify the original files directly. You would better keep it for future reference and create another directory under the installaion directory of NxFilter and copy all the files inside '/nxfilter/webapps' into the new directory and then modify these copied files. To make things easier, NxFilter supports 'www_dir' option on '/nxfilter/conf/cfg.properties' file.
When you have your own custom GUI in '/nxfilter/myweb' directory and you want to use this directory as the root directory of NxFilter's webserver, you need to add the following line into your cfg.properties file.
    www_dir = myweb
Then restart your NxFilter.
