Instalando o NxFilter no Windows manualmente
------------------------------------

Para instalar o NxFilter de forma manual, utilize o pacote `zip`. Ainda sim é possível executá-lo como um serviço Windows com um script batch incluso no pacote.

# Baixe o arquivo ``nxfilter-x.y.z.zip`` na área de `Downloads`.
# Extraia o arquivo zip na pasta `c:/nxfilter`.
# Acesse a pasta `c:/nxfilter/bin`.
# Execut o script `startup.bat`.

::

* Se deseja instalar o NxFilter como um serviço no Windows execute ``c:/nxfilter/bin/instsvc.bat``. Ele criará o serviço ``NxFilter``. Para remover o serviço rode ``c:/nxfilter/bin/unstsvc.bat``.
* Para rodar o NxFilter como um serviço ``net start NxFilter``.
* Parar o serviço ``net stop NxFilter``.
* Utilizando o serviço do NxCloud: 
  * Iniciar - `net start NxCloud`
  * Parar - `net stop NxCloud`


