Atualizando a Shallalist
*************************

NxFilter tem um script para atualização automática. Para proceder com a atualização da lista Shallalist pare o NxFilter e execute `/nxfilter/bin/update_sh.sh`. Dependendo da velocidade do seu link de internet esse processo pode levar um tempo maior para concluir todo o processo.

.. image:: /image/shalla_console.png

Caso seja preciso atualizar a lista no modo manual, baixe a mesma no endereço ``http://www.shallalist.de/Downloads/shallalist.tar.gzip`` e desompacte esse arquivo em ``/nxfilter/shallalist1/BL`` e execute o comando `update_sh.sh /nxfilter/shallalist1/BL`.

.. code-block:: bash

  cd /nxfilter/bin
  update_sh.sh /nxfilter/shallalist1/BL
