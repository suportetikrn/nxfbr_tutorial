Instalando no Alpine Linux 
----------------------------

A versão usada para exemplo é o Alpine Linux 3.4.0.

Para instalação no Alpine Linux será usado o pacote zip disponibilizado na área de Downloads.

Como pré-requisito é necessário instalar o OpenJDK, nesse caso instalaremos o OpenJDK 8.

No Alpine o pacote do OpenJDK é disponibolizado no repositório ``community``, entre em ``/etc/apk/repositories`` e deverá haver uma linha descomentada como a descrita: ``http://dl-2.alpinelinux.org/alpine/v3.4/community`` 

Após esse procedimento instale o OpenJDK JRE 8. ::

  $ su - root
  # apk --update add openjdk8-jre ca-certificates
  # update-ca-certificates

.. warning::

  O comando ''update-ca-certificates'' pode retornar uma mensagem de alerta 'Warning' porém isso não é prejudicial para o processo

Após a instalação do Java faça o download do pacote do NxFilter através do comando ``wget`` e então descompacte usando o comando ``unzip``. ::

  $ su - root
  # cd ~
  # wget -t0 -c http://www.nxfilter.org/download/nxfilter-4.0.6.zip
  # cd /
  # mkdir nxfilter
  # cd nxfilter
  # unzip ~/nxfilter-4.0.6.zip
  # chmod +x /nxfilter/bin/*.sh
  
Feito isso vamos criar os scripts para iniciar e parar o NxFilter, para que o mesmo fique como serviço e inicie/pare automaticamente no Alpine Linux. ::

  $ su - root
  # cd /etc/local.d
  # echo '/nxfilter/bin/startup.sh -d' > nxfilter.start
  # echo '/nxfilter/bin/shutdown.sh' > nxfilter.stop
  # chmod +x nxfilter*
  # rc-update add local

Agora vamos inicializar o sistema: ::
 
  $ su - root
  # service local start

Para saber se o mesmo está em execução, espere alguns segundos após inicializar e entre com o comando: ::
  
  $ /nxfilter/bin/ping.sh


Para acessar a interface administrativa, abra o seu browser de preferëncia e entre o endereço "http://<ip_servidor_nx>/admin". Se, por exemplo, você instalou o servidor NxFilter em uma máquina com o IP '192.168.100.2' digite "http://192.168.100.2/admin". 

 .. note:: No primeiro login o usuário é ``admin`` e a senha ``admin``.

Atualizando
^^^^^^^^^^^
 
O procedimento de atualização é bem simples, garanta que o serviço do NxFilter esteja parado.::

   $ su - root 
   # cd /nxfilter
   # /nxfilter/bin/shutdown.sh
   -- Aguarde alguns segundos
   # unzip ~/nxfilter-4.0.x.zip
   # /nxfilter/bin/startup.sh
   $ sudo start nxfilter
