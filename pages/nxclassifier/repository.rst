*****************************
Repositório
*****************************

O NxFilter executa atualizações da Jahaslist automaticamente. Ele faz o download dos arquivos a partir da Internet e atualiza a Jahaslist.

Você pode criar seu próprio repositório para esta atualização remota. Ele é prático para pessoas que desejam compartilhar suas lista ou fazer negócio criando uma lista própria.

1. O processo de atualização.

 Ao adicionar a URL indicando o arquivo de atualização em `NxClassifier > Setup > Jahaslist Repository`, o NxFilter fará o download e buscará atualizações para a Jahaslist. Esse processo será executado em dois momentos: ao reiniciar o NxFilter e uma vez a noite. O processo de atualização roda em paralelo com o NxFilter desde modo não haverá prejuízo para sua funcionalidade padrão ( os filtros de DNS ) enquanto ele executa a atualização.

 .. note::

  Você pode adicionar mais de um repositório separados por linhas.

2. O formato do arquivo.

 De modo geral o que é necessário é se ter o arquivo com a extensão '.txt'. Porém, se o arquivo for grande, é possível usar arquivos compactados no formato tarball com a extensão '.tgz' ou '.tar.gz', dentro desse arquivo haverá o arquivo texto.
 
 Dentro desse arquivo haverão registros com os domínios e suas categorias separados por virgulas, como a seguir:

  google.com,46

  yahoo.com,46

  nxfilter.org,9

Atualmente esse é o formato usado para arquivos importados ou exportados da Jahaslist na GUI. Então é permitido compartilhar esse arquivo exportado.

.. warning::
  
 - Arquivos texto podem conter ae 100.000 domínios.

 - Ao criar um arquivo `recatlist.tgz` para armazenar `recatlist.txt`, faça do seguinte modo:
   
    ex) tar cvzf recatlist.tgz recatlist.txt

3. O versionamento dos arquivos.

Para evitar que o mesmo arquivo seja baixado diversas vezes o NxFilter tem um sistema de controle de versões para os arquivos disponibilizados. Quando for gerado o arquivo na URL ''http://www.nxfilter.org/test/recatlist.txt'', o NxFilter tentará encontrar um arquivo de versão no mesmo endereço que tenha o seguinte formato ''http://www.nxfilter.org/test/recatlist.ver''

No arquivo de versão '.ver' você deverá registrar um número. Quando esse número for maior que a versão anterior, já baixada pelo NxFilter, o sistema fará um novo download do arquivo e atualiza a Jahaslist. Se o número for menor ou igual, o NxFilter ignora o arquivo.

.. note::

  A versão não pode ser menor que 1.

