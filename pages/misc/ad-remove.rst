Removendo anúncios embutidos em páginas
****************************************

Há diversas páginas com anúncios embutidos vindos de outros domínios. Um dos problemas de bloquear esses anúncios com o NxFilter é que a página pode ficar completamente descaracterizada. Afinal sua página de bloqueio ficará embutida no lugar dos anúncios.

Para evitar esse tipo de problema, existem duas formas de remover anúncios com o NxFilter. 

1. Usando uma categoria especial em 'Category > Custom' chamado 'ad-remove'. Se você adicionar um domínio nesta categoria e bloquear essa categoria em qualquer lugar, o NxFilter bloqueia o domínio com uma página em branco.

2. O outro método é fazer o bloqueio usando a opção 'Ad-Remove' em uma política. Com esta opção o NxFilter bloqueia a categoria 'Ads' a partir da Jahaslist.

.. note::

  Após adicionar um domínio na categoria 'ad-remove' você precisa bloquear o domínio em uma lista ou outra política caso contrário ele não será bloqueado.

