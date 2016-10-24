*************************************
NxForward para ocultar falhas no SSL
*************************************
 
 No filtro DNS, quando é bloqueado um site HTTPS é recebido um alerta de SSL não seguro.

 ..image:: /images/nxforward_ssl.png
 
 É um erro comum pois o browser tenta protegê-lo do que é chamado de ataque 'Man in the Middle'. De qualquer forma ainda é um processo irritante pois na verdade é causado pela politica de filtragem. Muitas pessoas já solicitaram que este alerta seja removido, a solução para esse problema - atualmente - só é aplicável no browser Google Chrome. 
 
 Ao instalar o NxFilter - que é uma extensão para o Google Chrome - as páginas HTTPS que forem bloqueadas serão redirecionadas para uma página HTTP novamente, permitindo assim a visualização da página de bloqueio em HTTP.

 O NxForward pode ser instalado a partir da Chrome Web Store. Baixe a partir do link.

    - `Download NxForward na Chrome Web Store`_

.. target-notes::
.. _`Download NxForward na Chrome Web Store`: https://chrome.google.com/webstore/detail/nxforward/ohhmhnionmgplhblinhpijfbaelmaojd 
