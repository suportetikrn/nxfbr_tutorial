Instalando em outras distribuições Linux
------------------------------------------------


 Em geral, quando se instala o NxFilter em sistemas Linux::

  * É preciso ter acesso como usuário ``root``
  * Ter o Java 7 ou superior instalado
  * Pode iniciar NxFilter em modo daemon usando o parâmetro '-d' ao executar o script ``startup.sh``

#. Baixe o arquivo ``nxfilter-x.y.z.zip`` a partir da área de Download.
#. Extraia o arquivo zip na pasta ``/nxfilter``
#. Entre na pasta ``/nxfilter/bin`` e execute ``chmod +x *.sh``
#. Execute ``startup.sh``

 .. image:: /images/linux_startup.png

#. Para acessar a GUI de administração, entre com o endereço ip do servidor NxFilter no browser, 'http://<ip_servidor>/admin'. Usuário e senha inicial são 'admin' e 'admin'.

.. note::
   Você pode inicializar o NxFilter automáticamente usando o arquivo '/etc/rc.local'. Considerando que o NxFilter fora instalando em '/nxfilter', basta adicionar a linha '/nxfilter/bin/startup.sh -d' no arquivo '/etc/rc.local'. Não esqueça do parâmetro '-d' pois ele coloca o serviço NxFilter como daemon.
