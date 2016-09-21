Propriedades OEM
********************

O arquivo 'oem.properties' para armazenar parâmetros específicos do  NxOEM e NxCloud. Se existir o arquivo 'oem.properties' em '/nxfilter/conf' com o seguinte valor.

.. code-block:: jproperties

   appname = MyFilter

1. NxOEM ou NxCloud adiciona o prefixo 'MYFILTER' nas mensagens Syslog.

2. Quando o NxOEM ou NxCloud envia um email de alerta para os usuários ele adiciona 'MyFilter' como prefixo do assunto.
