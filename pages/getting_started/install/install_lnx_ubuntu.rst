Instalando o NxFilter no Ubuntu
--------------------------------

É disponibilizado o pacote 'deb' para o Ubuntu Linux na área de Downloads.
Para instalá-lo, primeiro instale o Java. Baixo o pacote através do comando ``wget`` e então instale usando o comando ``dpkg``. Feito isso bastará iniciá-lo usando o script instalado através com o pacote.

We have a 'deb' package for Ubuntu Linux.

To install it, install Java first. Download the package using 'wget', and then install it using 'dpkg'. Then start it from the upstart script which is installed with the package.::
  
  $ sudo apt-get install openjdk-8-jre
  $ wget http://www.nxfilter.org/download/nxfilter-3.1.6.deb
  $ sudo dpkg -i nxfilter-3.1.6.deb
  $ sudo start nxfilter

Para acessar a interface administrativa, abra o seu browser de preferëncia e entre o endereço "http://<ip_servidor_nx>/admin". Se, por exemplo, você instalou o servidor NxFilter em uma máquina com o IP '192.168.100.2' digite "http://192.168.100.2/admin". No primeiro login o usuário é ``admin`` e a senha ``admin``.

 Atualizando
 ^^^^^^^^^^^
 
O procedimento de atualização é bem simples, garanta que o serviço do NxFilter esteja parado.::

   $ sudo stop nxfilter
   $ sudo dpkg -i nxfilter-3.1.6.deb
   $ sudo start nxfilter
