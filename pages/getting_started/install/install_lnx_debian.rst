Instalando no Debian 
--------------------------------

É disponibilizado o pacote 'deb' para o Ubuntu/Debian Linux na área de Downloads.
Para instalá-lo, primeiro instale o Java e o Sudo. Baixo o pacote através do comando ``wget`` e então instale usando o comando ``dpkg``. Feito isso bastará iniciá-lo usando o script instalado através com o pacote.::

  $ su - root
  $ apt-get install openjdk-7-jre sudo
  $ wget http://www.nxfilter.org/download/nxfilter-3.4.2.deb
  $ sudo dpkg -i nxfilter-3.4.2.deb
  $ start nxfilter

Seu sistema Debian pode estar usando Systemd invés de Upstart. O script do Systemd também estará instalado. Execute os seguintes comandos para habilitar o script e parar/iniciar o serviço NxFilter.

   $ sudo systemctl enable nxfilter.service
   $ sudo systemctl start nxfilter.service


Para acessar a interface administrativa, abra o seu browser de preferëncia e entre o endereço "http://<ip_servidor_nx>/admin". Se, por exemplo, você instalou o servidor NxFilter em uma máquina com o IP '192.168.100.2' digite "http://192.168.100.2/admin". 

 .. note:: No primeiro login o usuário é ``admin`` e a senha ``admin``.

 Atualizando
 ^^^^^^^^^^^
 
O procedimento de atualização é bem simples, garanta que o serviço do NxFilter esteja parado.::

   $ sudo systemctl stop nxfilter.service
   $ sudo dpkg -i nxfilter-3.4.2.deb
   $ sudo systemctl start nxfilter.service

Seu sistema Debian pode estar usando Systemd invés de Upstart. O script do Systemd também estará instalado. Execute os seguintes comandos para habilitar o script e parar/iniciar o serviço NxFilter.::

   $ sudo systemctl enable nxfilter.service
   $ sudo systemctl start nxfilter.service

